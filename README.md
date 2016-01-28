#### obevenfastwebsi

- cp4
browsers can download scripts in parallel but not execute them in parallel.

xhr eval:
```js
var xhrObj = new XMLHttpRequest();
xhrObj.onreadystatechange=function(){
  if(xhrObj.readyState==4 && xhrObj.status==200){
  eval(xhrObj.responseText);
  }
}
xhrObj.open('GET','A.js',true);
xhrObj.send();
```

A faster approach is xhr injection.
```js
var xhrObj = new XMLHttpRequest();
xhrObj.onreadystatechange=function(){
  if(xhrObj.readyState==4){
  var elem = document.createElement('script');
  document.getElementByTagName('head')[0].appendChild(elem);
  elem.text=xhrObj.responseText;
  }
}
xhrObj.open('GET','A.js',true);
xhrObj.send();
```
