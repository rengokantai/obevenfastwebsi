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

iframe
in html
```html
<iframe width=0 height=0 frameborder=0 src='a.html' id=xx></iframe>
```

js:
```js
window.frames[0].createNewDiv();
document.getElementById('xx').contentWindow.createNewDiv();

function createDiv(){
var newd = parent.document.createElement('div');
parent.document.body.appendChild(newd);
```


script DOM
```js
var elem = document.createElement('script');
elem.src='a.js';
document.getElememtByTagName('head')[0].appendChild(elem);
```

