#node.js-stream
### 基本知识
##### 四种流类型
| 序号 | 名称 | 操作|
| :-- | :-- | :-- |
|1|Readable|可读操作|
|2|Writable|可写操作|
|3|Duplex|可读可写操作|
|4|Transform|操作被写入数据，然后读出信息|
所有的Stream对象都是EventEmitter的实例。常用的事件：
| 序号 | 名称 | 操作|
| :-- | :-- | :-- |
|1|data|当有数据在可读时触发|
|2|end|没有更多的数据可读时触发|
|3|error|在接收和写入过程中发生错误时触发|
|4|finish|所有数据已被写入到底层系统时触发|
### 从流中读取数据
```js
var fs = require('fs');
var data = ' ';

//创建可读流
var readerStream = fs.createReadStream('input.txt');

//设置编码为'utf8
readerStream.setEncoding('utf8');

//处理流事件 -->data, end, and error
readerStream.on('data',function (chunk) {
    data += chunk;
});

readerStream.on('end',function ( ) {
    console.log(data);
});

readerStream.on('error',function (err) {
    console.log(err.stack);
});

console.log("程序执行完毕");
```
### 写入流
```js
var fs = require('fs');
var data = '索拉卡大家拉克斯基的拉萨看得见啊离开家';

//创建一个可以写入的流，写到文件 output.txt中
var writeStream = fs.createWriteStream('output.txt');

//使用utf8编码写入数据
writeStream.write(data,'UTF8');

//标记文件末尾
writeStream.end();

//处理流事件 
writeStream.on('finish',function( ) {
    console.log("写入完成");
});

writeStream.on('error',function(err) {
    console.log(err.stack);
});

console.log("程序执行完毕");
```
### 管道流
```js
var fs = require('fs');

//创建一个可读流
var readerStream = fs.createReadStream('input.txt');

//创建一个可写流
var writeStream = fs.createWriteStream('output.txt');

//管道读写操作
//读取input.txt 文件内容，并将内容写入到output文件中
readerStream.pipe(writeStream);

console.log("程序执行完毕");
```
### 链式流
链式是通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作。
##### 压缩文件
```js
var fs = require('fs');
var zlib = require('zlib');

//压缩input.txt文件为input.txt.gz
fs.createReadStream('input.txt')
    .pipe(zlib.createGzip( ))
    .pipe(fs.createWriteStream('inpuit.txt.gz'));

console.log('文件压缩完成');
```
##### 解压文件
```js
var fs = require('fs');
var zlib = require('zlib');

//解压input.txt.gz文件为input.txt
fs.createReadStream('input.txt.gz')
    .pipe(zlib.createGunzip( ))
    .pipe(fs.createWriteStream('input.txt'));

console.log("文件解压完成");

```