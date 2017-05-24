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


1.Parellel vs Async

 Parellelism is completely different from asynchronusity.
 Parellelism means runnig multiple threads 
 
1. CalBack
* Very Much trust issue->Call back can break anytime,depends upon external service giving responces.
such as what will happen if the callback is called multiple times,too fewtimes error callback called first.


* Achiving very Simpilar Scenerios could be difficult->
A very simple problem like calling 3 files and displaying their content sequencely  could be 
tipical to solve.....gist example.



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
A api which  solves inversion of cnotrol and callback problems.
refer to keyls ext4 example an implemetation of promise.all
```promise.race```

1.













