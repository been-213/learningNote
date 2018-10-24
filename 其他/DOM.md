### DOM
|函数|参数|返回值|
|:--|:--|:--|
|获取元素|||
|document..getElementsById(element)|ID名|返回一个对象|
|document.getElementsByTagName(tagname)|只接受一个参数-标签名|返回一个对象数组|
|document.getElementsByClassName(classname)|只接受一个参数-类名|返回一个对象数组|
|获取和设置属性|||
|object.getAttribute(attribute)|只接受一个参数-属性名|返回属性值或者null|
|object.setAttribute(attribute,value)|两个参数，要修改的属性以及设置的值|
|nodeType|无参数|返回1-元素节点；2-属性节点；3-文本节点|
|nodeValue|无参数| = value更新节点值|
```js
function prepareGallery() {
  if(!document.getElementsByTagName) return false;
  if(!document.getElementById) return false;
  if(!document.getElmentById("id1")) return false;
  var id1 = document.getElmentById("id1");
  var links = gallery.getElementsByTagName("a");
  for ( var i=0; i< links.length; i++) {

    links[i].onclick = function() {
      return showPic(this) ? false : true;
    }
  }
}
function showPic(whichpic) {
  if(!document.getElementById("id2")) return false;
  var source = whichpic.getAttribute("href");
  var id2 = document.getElementById("id2");
  if(id2.nodeName !="IMG") return false;
  id2.setAttribute("src", source);
  if(document.getElementById("id3")) {
    var text = whichpic.getAttribute("title") ? whichpic.getAttribute("title") : "";
    var id3 = document.getElementById("id3");
    if (id3.firstChild.nodeType == 3) {
      id3.firstChild.nodeValue = text;
    }
  }
  return true;
}

}
```
|函数|参数|
|:--|:--|
|window.open(url,name,features)|三个可选参数url：省略就空白；features：窗口属性| 
|document.appendChild(child)|需要添加的子节点| 
|document.creatrTextNode(string)|添加文本节|
```js
window.onload = function() {
  var para = document.createElement("p");
  var text = document.createTextNode("string");
  para.appendChild(txt);
  var testdiv = document.getElementById("id1");
  testdiv.appendChild(para);
}
```

