---
title: JS跨浏览器的事件处理
categories: JavaScript
tags: [JavaScript, 浏览器兼容性处理]
---

JS中，事件是指用户或浏览器自身执行的某种动作。如click(点击事件)、mouse***(鼠标事件)。事件流是指页面中接收事件的顺序,也可理解为事件在页面中传播的顺序。


<!-- more -->


## 事件流

 1. 事件：用户或浏览器自身执行的某种动作。如click(点击事件)、mouse***(鼠标事件)。
 2. 事件流：页面中接收事件的顺序,也可理解为事件在页面中传播的顺序。

**DOM事件流包括三个阶段**：

 - 事件捕获阶段
 - 处于目标阶段
 - 事件冒泡阶段

*IE 采用事件冒泡的方式（**div-->body-->html-->Document**）
NetScape 采用事件捕获的方式（**Document-->html-->body-->div**）
DOM 采用先捕获后冒泡的方式*

## 事件处理程序
事件是用户或浏览器自身执行的某种动作，而响应某个事件的函数就叫做事件处理程序。事件处理程序的方式有以下4种：

### HTML事件处理程序

方法：使用一个与相应事件处理程序同名的HTML属性来指定，可以直接在属性中的js代码中通过event变量获取到event对象，代码中的this指的是事件的目标元素。
```
<input type="button" value="click" onclick="alert(event.type);alert(this.value);" />
```

### DOM0级事件处理程序

方法： 将一个函数赋值给一个事件处理程序属性。如下：
```
var btn = document.getElementById("btn")
btn.onclick = function (event) {
    console.log(event)
}
```
**优点： 跨浏览器。
缺点： 若绑定多个事件处理程序，会形成覆盖，只执行最后的函数。**

### DOM2级事件处理程序

DOM2级事件定义了两个方法，用于处理指定和删除事件程序的操作,该方法可以添加多个事件处理程序

 - [addEventListener(type, listener, isCapture)][1]
 - [removeEventListener(type,listener, isCapture)][2]

```
var btn = document.getElementById("btn")
function handler(event) {
    console.log(event)
}
btn.addEventListener("click", handler, false) // 添加事件
btn.removeEventListener("click", handler, false) // 移除事件
```

### IE事件处理程序

IE实现了与DOM中类似的两个方法：

 - attachEvent(type, listener)
 - detachEvent(type, listener)

其中type是on+事件名，如点击事件：**onclick**
```
btn.attachEvent("onclick", function (event){
    console.log(event)
})
```

## 《JavaScript高级程序设计》中跨浏览器事件绑定
```
var EventUtil = {

	//跨浏览器添加事件
    addHandler: function(element, type, handler){
        if (element.addEventListener){
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent){
            element.attachEvent("on" + type, handler);
        } else {
            element["on" + type] = handler;
        }
    },

	// 跨浏览器获得对象event
    getEvent: function(event){
        return event ? event : window.event;
    },

	// 跨浏览器获得对象event的目标
    getTarget: function(event){
        return event.target || event.srcElement;
    },

	// 跨浏览器阻止默认行为
    preventDefault: function(event){
        if (event.preventDefault){
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    },

	// 跨浏览器移除事件
    removeHandler: function(element, type, handler){
        if (element.removeEventListener){
            element.removeEventListener(type, handler, false);
        } else if (element.detachEvent){
            element.detachEvent("on" + type, handler);
        } else {
            element["on" + type] = null;
        }
    },

	// 跨浏览器阻止事件冒泡
    stopPropagation: function(event){
        if (event.stopPropagation){
            event.stopPropagation();
        } else {
            event.cancelBubble = true;
        }
    },

	// 跨浏览器检测鼠标按钮
    getButton: function(event){
        if (document.implementation.hasFeature("MouseEvents", "2.0")){
            return event.button;
        } else {
            switch(event.button){
                case 0:
                case 1:
                case 3:
                case 5:
                case 7:
                    return 0;
                case 2:
                case 6:
                    return 2;
                case 4: return 1;
            }
        }
    },

	// 跨浏览器获取键盘事件的键码
    getCharCode: function(event){
        if (typeof event.charCode == "number"){
            return event.charCode;
        } else {
            return event.keyCode;
        }
    },

	// 跨浏览器获得相关元素（仅对mouseover和mouseout有效）
    getRelatedTarget: function(event){
        if (event.relatedTarget){
            return event.relatedTarget;
        } else if (event.toElement){
            return event.toElement;
        } else if (event.fromElement){
            return event.fromElement;
        } else {
            return null;
        }
    },

	// 跨浏览器鼠标滚轮事件
    getWheelDelta: function(event){
        if (event.wheelDelta){
            return (client.engine.opera && client.engine.opera < 9.5 ? -event.wheelDelta : event.wheelDelta);
        } else {
            return -event.detail * 40;
        }
    }

};
```


  [1]: http://www.runoob.com/jsref/met-element-addeventlistener.html
  [2]: http://www.runoob.com/jsref/met-element-removeeventlistener.html