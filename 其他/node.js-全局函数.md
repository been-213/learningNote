#node.js-全局函数
#### __filename
当前执行的文件名，输出绝对路劲。如果在模块中，返回的值时模块文件的路径。
```js
//输出全局变量__filename的值
console.log(__filename);
```
#### __dirname
当前执行脚本所在的目录
```js
//输出全局变量__dirname的值
console.log(__dirname);
```
#### setTimeout(cb,ms)
在（ms）毫秒后执行指定函数（cb）。：setTimeout()只执行一次指定函数。
返回一个代表定时器的句柄值。
```js
function  printHello () {
  console.log("hello world");
}
//两秒后执行以上函数
setTimeout(printHello,2000);
```
#### clearTimeout(t)
清除之前通过setTimeout创建的定时器。参数t是通过setTimeout()函数创建的定时器
```js
function printHello () {
      console.log("hello world!");
}
//两秒后执行以上函数
var t = setTimeout(prrintHello,2000);
//清除定时器
clearTimeout(t);
```
#### setlnterval(cb,ms)
setInterval(cb, ms) 全局函数在指定的毫秒(ms)数后执行指定函数(cb)。
返回一个代表定时器的句柄值。可以使用 clearInterval(t) 函数来清除定时器。
setInterval() 方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。
```js
function printHello(){
  console.log("Hello World");
}
//两秒后执行以上函数
setInterval(printHello,2000);
```
#### console方法
| 序号 | 方法 | 描述 |
| :-- | :-- | :-- |
|1|console.log()|标准输出流|
|2|sonsole.info()|该命令的作用是返回信息性消息，这个命令与console.log差别并不大，除了在chrome中只会输出文字外，其余的会显示一个蓝色的惊叹号。|
|3|console.error()|输出错误消息。|
|4|console.warn()|输出警告消息|
|5|console.dir()|用来对一个对象进行检查（inspect），并且易于阅读和打印的格式显示|
|6|console.time()|输出时间，表示计时开始|
|7|console.timeEnd()|结束时间，表示计时结束。|
|8|console.trace(message[,....])|用于判断某个表达式或变量是否为真，接收两个参数，第一个是表达式，第二个是参数字符串。只有当第一个参数为false，才会输出第二个参数，否则不会有任何结果|
#### process
| 序号 | 方法 | 描述 |
| :-- | :-- | :-- |
|1|exit|当前进程准备退出时触发|
|2|beforeExit|当时Node清空事件循环，并且没有其他安排时触发这个事件。通常来说，当没有进程安排时node退出，但是beforeExit的监听器可以异步调用，这样node就会继续执行|
|3|uncaughException|当一个异常冒泡回到事件循环，触发这个事件。如果给异常添加了监视器，默认的操作（打印堆栈跟踪信息并退出）就不会发生|
|4|signal事件|当进程接收到信号时就触发。信号列表详见标准的 POSIX 信号名，如 SIGINT、SIGUSR1 等。|
