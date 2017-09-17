---

layout:     post
title:      "Promise 对象"
subtitle:   ""
date:       2017-09-17 20:09:00
author:     "Mariano"
header-img: "img/promise.jpg"
tags:  

    - ES6
    - Promise 对象
 
---
 > 最近在看 ES6 标准入门，看到 Promise 对象这一章，顺手总结一下（实际上我已经很久没有写博客了）  
     
     
# Promise 的含义  
  
  Promise 就是一个对象，用来传递一部操作的信息，它代表了某个未来才会知道结果的事件（通常是一个异步操作）。
  Promise 对象有两个特点：  
  
  * 对象的状态不受外界影响。Promise 有三种状态：Pending (进行中)、Resolve（已完成）、Rejected(已失败)  
  * 一旦状态改变就不会再改变，任何时候都可以获得这3G结果  

   既然有了 Promise 对象，这样就避免了我们层层嵌套回调函数，而且，Promise 对象提供了统一的接口，使得控制异步操作变得容易。  
     
# Promise 基本用法  
    
  ES6 规定，Promise 对象是一个构造函数，用来生成 Promise 实例，用法如下:  
    
```javascript
var Promise = new Promise(function(resolve,reject){
  // somecode
 if(/*异步操作成功*/){
  resovle(value);
 }else{
  reject(error);
  }
 });
```  
    
  Promise 构造函数接受一个函数作为参数，改函数的两个参数分别是 resovle 和 reject.它们是两个函数，由 JavaScript 引擎提供，不用自己部署。  
    
  resolve 函数的作用是，将 Promise 对象状态由'未完成'变成'成功';reject 函数的作用是，将 Promise 对象的状态从'未完成'变成'失败'。  
    
  Promise 实例生成以后，可以用 then 方法分别指定 Resolve 状态和 Rejected 状态的回调函数。    
  
```javascript
Promise.then(function(value){
  //成功
 },function(error){
  //失败
 });
```  
    
    
  then 的方法也接受两个回调函数作为参数。第一个回调函数是 Promise 对象的状态从'未完成'编程'成功'时调用，第二个则是把状态从'未完成'变成'失败'时调用，其中，第二个是可选的，不一定需要提供。  
    
  一个简单的 Promise 对象的简单例子   
   
```javascript
function timeout(ms){
   	 return new Promise((resolve,reject) => {
   	 	setTimeout(resolve,ms,'done');
   	 });
   }
   
   timeout(100).then((value) => {
   		console.log(value);
   })
```  
     
   
  
 