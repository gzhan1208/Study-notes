### `Event Loop`
***
`js` 为单线程，执行同步任务时候，直接推入调用栈中执行，遇见异步任务时，先将异步任务挂起，
直到异步任务有返回再推入执行队列中，当调用栈中同步任务执行完毕后，调用栈从执行队列中获取异步任务执行，这个循环过程叫做事件循环 `eventLoops` 。

### 微任务和宏任务
***
微任务和宏任务都属于异步任务。微任务优先级高于宏任务，因此每一次都会先执行完微任务再执行宏任务。    

宏任务：执行 `script` 标签内部代码、`setTimeout/setInterval`、`ajax` 请求、`postMessageMessageChannel`、`setImmediate`，`I/O（Node.js）`  
微任务有：`Promise`、`MutonObserver`、`Object.observe`、`process.nextTick（Node.js）`
