## Asyn JavaScript

we should start reading (ecma specs)[https://www.ecma-international.org/ecma-262/6.0/]


#### Differnet b/w compiled and interprited language
....donsent converts onto binary
when we write 
`var name = 'ramesh'` there are two different things which are happening,and they are happening at 
completely different timeffame,i.e declaration and assignment.


JavaScript compiler runs all the declaration once
so if we do `var name = 'ramesh'` a 100 times new variable will not be created everytime,it will only
be created once and assgned later.




##### Leakeage of Variables

```
    var bar = 'my drink';

    function foo(bar){
        bar = 'my place';
        buz = 'should up';
    }


```
 when we come to last line in the function `buz = 'should up'`,the  function foo  dosent have this variable in 
 its local scope,so it goes to global scope,and global dosent have this,but it creates this variable
 and this is where variable Leakeage comes,if we dont use strict mode.



#### asynchronusity


1.Event loop
A event loop is never ending loop which runs the single chunk of programme.he JS engine itself has never done 
anything more than execute a single chunk of your program at any given moment, when asked to.

so when we do a `setTimeout`,it sets a timer in the execution enviornment(mainly browser or node),and that 
execution enviornment gets a function to be called when the time is over,now as soon as the time gets
over it puts that function inside event loop and event loops executes that function.
if there are already other items in the event loop at that moment,the callback waits. It gets in line behind the others 



1.Parellel vs Async

 Parellelism is completely different from asynchronusity.
 Parellelism means runnig multiple threads 
 
1. CallBack

They are the most commonly used way to achive asynchronusity in JavaScript code,
* Very Much trust issue->Call back can break anytime,depends upon external service giving responces.
such as what will happen if the callback is called multiple times,too fewtimes error callback called first.


````
listen( "click", function handler(evt){
    setTimeout( function request(){
        ajax( "http://some.url.1", function response(text){
            if (text == "hello") {
                handler();
            }
            else if (text == "world") {
                request();
            }
        } );
    }, 500) ;
} );



````

Why callbacks are hell?
A simple scenerio to call three urls and printing the results simultanoulsy 

````
function fakeAjax(url,cb) {
    var fake_responses = {
        "file1": "The first text",
        "file2": "The middle text",
        "file3": "The last text"
    };
    var randomDelay = (Math.round(Math.random() * 1E4) % 8000) + 1000;

    console.log("Requesting: " + url);

    setTimeout(function(){
        cb(fake_responses[url]);
    },randomDelay);
}

function output(text) {
    console.log(text);
}

// **************************************
// The old-n-busted callback way

function getFile(file) {
    fakeAjax(file,function(text){
        fileReceived(file,text);
    });
}

function fileReceived(file,text) {
    // haven't received this text yet?
    if (!responses[file]) {
        responses[file] = text;
    }

    var files = ["file1","file2","file3"];

    // loop through responses in order for rendering
    for (var i=0; i<files.length; i++) {
        // response received?
        if (files[i] in responses) {
            // response needs to be rendered?
            if (responses[files[i]] !== true) {
                output(responses[files[i]]);
                responses[files[i]] = true;
            }
        }
        // can't render yet
        else {
            // not complete!
            return false;
        }
    }

    output("Complete!");
}

// hold responses in whatever order they come back
var responses = {};

// request all files at once in "parallel"
getFile("file1");
getFile("file2");
getFile("file3");

````






* Achiving very Simpilar Scenerios could be difficult->




1. Thunk

####Synchronous

A thunk is a function which has everything in it to produce the result.


#### Async Thunk->It is a function which requires only a callback function to produce result.


```

function fake_async(cb){
    setTimeout(function(){
        cb(10+20)
    },1000)
}


var thunk = function(cb){
    fake_async(cb);
}



thunk(function(sum){
    console.log(sum)
})





refer to kyle ex 2


1. Promises

It is value which will produce some result in future.

###### States of promise
* `pending`: initial state, not fulfilled or rejected.
* `fulfilled`: meaning that the operation completed successfully.
* `rejected`: meaning that the operation failed.

####### Basic Usage

````
var p = new Promise(function(resolve, reject) {
    
    // Do an async task async task and then...

    if(/* good condition */) {
        resolve('Success!');
    }
    else {
        reject('Failure!');
    }
});

p.then(function() { 
    /* do something with the result */
}).catch(function() {
    /* error :( */
})

Three files example

````

function fakeAjax(url,cb) {
    var fake_responses = {
        "file1": "The first text",
        "file2": "The middle text",
        "file3": "The last text"
    };
    var randomDelay = (Math.round(Math.random() * 1E4) % 8000) + 1000;

    console.log("Requesting: " + url);

    setTimeout(function(){
        cb(fake_responses[url]);
    },randomDelay);
}

function output(text) {
    console.log(text);
}

// **************************************

function getFile(file) {
    return new Promise(function(resolve){
        fakeAjax(file,resolve);
    });
}

// Request all files at once in
// "parallel" via `getFile(..)`.
var p1 = getFile("file1");
var p2 = getFile("file2");
var p3 = getFile("file3");

// Render as each one finishes,
// but only once previous rendering
// is done.
p1
.then(output)
.then(function(){
    return p2;
})
.then(output)
.then(function(){
    return p3;
})
.then(output)
.then(function(){
    output("Complete!");
});


````

#### `catch` ->Executed when a promise is rejected

new Promise(function(resolve, reject) {
    // A mock async action using setTimeout
    setTimeout(function() { reject('Done!'); }, 3000);
})
.then(function(e) { console.log('done', e); })
.catch(function(e) { console.log('catch: ', e); });












A api which  solves inversion of cnotrol and callback problems.
refer to keyls ext4 example an implemetation of promise.all
```promise.race```

1.Genetators

In JavaScript normal function runs Sequencely i.e we can't stop the execution of 
function in between. This this is possible with JavaScript Genetators.
Genetators can pause execution of any expression,in between.



```
function *gen(){
    console.log("Hello");
    yield;
    console.log("World);
}



var it = gen();
it.next();
it.next();



```


promise in a generator

async await


button clicking of promises






