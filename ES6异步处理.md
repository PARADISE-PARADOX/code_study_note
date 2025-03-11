# ES6异步处理

## Promise

常见的异步：定时器、Ajax。

```javascript
console.log("同步1")
console.log("同步1")
setTimeout(()=>{
	console.log("异步1")
})
console.log("同步4")
```

Promise用于解决异步嵌套的问题。

### 使用

```javascript
const p1 = new Promise((resolve, reject) => {
  //   resolve("1111111成功");
  reject("1111111失败");
})
  .then((data) => {
    console.log(data);
    console.log("调用then");
  })
  .catch((err) => {
    console.log(err);
    console.log("调用catch");
  })
  .finally(() => {
    console.log("无论成功还是失败，调用finally");
  });
```

代码中`Promise`是一个构造函数，其中的两个参数，`resolve`表示将对象的状态从未完成变为成功；`reject`将对象的状态从未完成变为失败。`then`方法中的参数接收的就是`resolve`的回调函数，`catch`方法参数接收的是`reject`中的回调函数；`finally`方法表示无论成功还是失败，都会被调用。即结构为`Promise().then().catch().finally()`

当存在多个异步操作的任务时，其结构应该为`Promise().then().then() …… .catch().finally()`，并且上一个`then`的返回值为第二个任务的`Promise`：

```javascript
const p1 = new Promise((resolve, reject) => {
  // resolve("1111111成功");
  reject("1111111失败");
})
  .then(
    (data) => {
      console.log(data);
      console.log("调用第一个then");
      return new Promise((resolve, reject) => {
        resolve("2222222成功");
      });
    },
    (error) => {
      console.log(error);
      console.log("222222失败");
      throw new Error("222222失败");
    }
  )
  .then(
    (data) => {
      console.log(data);
      console.log("调用第二个then");
      return new Promise((resolve, reject) => {
        resolve("3333333成功");
      });
    },
    (error) => {
      // 这里需要将错误处理回调函数放在then的第二个参数位置
      throw new Error("333333失败");
    }
  )
  .then((data) => {
    console.log(data);
    console.log("调用第三个then");
  })
  .catch((err) => {
    console.log(err);
    console.log("调用catch");
  })
  .finally(() => {
    console.log("无论成功还是失败，调用finally");
  });


```

