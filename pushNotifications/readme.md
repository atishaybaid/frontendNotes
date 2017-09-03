## Implementing push Notifications
​
##### KeyPoints
​
1. Only works if your site supports https
2. We have to setup a project in [fireBase](https://firebase.google.com/)
3. Then a server key and public api key would be generated,whic will be used in frontend manifest
​
​
#### Flow
1. It has to be checked if service worker are supported in browser.
`'serviceWorker' in navigator` 
2. Then registrer the service worker,it returns a promise,which can be used to initilize the ui.
` navigator.serviceWorker.register('sw.js').then(intializeState);`
3. Now,we have to check if push notifications are supported,
we check them in `ServiceWorkerRegistration.prototype`
`'showNotification' in ServiceWorkerRegistration.prototype`
​
4. Now,we check if user is already subcribed,the following steps are taken
   1. when service worker becomes ready,all callback is recieved,it contains pushManager method
       ```
          navigator.serviceWorker.ready.then(function(serviceWorkerRegistration){
          console.log("serviceWorker registered");
           serviceWorkerRegistration.pushManager.getSubscription().then(function(subscription){
    ```
     
   2. The subscription tells if a user is subscribed or not.
    ```
      if(subscription){
                      // to do
                      console.log("user is subscribed");
                      updateSubscriptionOnServer(subscription);
​
                  } else{
                        console.log("push notification not supported");
                        subscribeUser(serviceWorkerRegistration);
                  }
​
    ```
​
        here,we check if a user is subscribed or not,if not we subscribe the user.
​
​
​
    3. For subscribing a user,we call the follwing method
       ```
            serviceWorkerRegistration.pushManager.subscribe(options).then(function(subscription){
          updateSubscriptionOnServer(subscription);
         })
   
      ```
      here,the subscription callback reurns the a endpoint key which we store on our backend            db,and      it is used to send
        pushmessages.
​
5. Write the serive worker code,for listining to push event,this is where the push message is recieved
```
  self.addEventListener('push',(event)=>{
      var data =  {};
      if(event.data){
          data = event.data;
      }
      var title = data.title || 'Msg Title';
      var message = data.message || 'Message';
      var tag = 'simple-push-demo-notification-tag';
​
      //const icon; icon to be added
​
      event.waitUntil(  
      self.registration.showNotification(title, {  
        body: message,  
        tag: tag  
      })  
    );  
​
​
​
​
```
​
    **Must reads**
    1.[codeLab](https://developers.google.com/web/updates/2015/03/push-notifications-on-the-open-web?hl=en)
    2.[codeLab](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/?hl=en)
    3.[serviceWorker Lifecycle](https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/lifecycle)
​