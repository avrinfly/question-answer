<!--
 * @Description: 实现一个EventEmitter类
 * @Author: hetengfei
 * @Github: https://github.com/avrinfly
 * @Date: 2019-08-28 00:47:42
 * @LastEditors: hetengfei
 * @LastEditTime: 2019-08-28 00:47:43
 -->
#### 实现一个EventEmitter类
包含on（监听事件，该事件可以被触发多次）- once（也是监听事件，但只能被触发一次）- fire(emit)（触发指定的事件）- off（移除指定事件的某个回调方法或者所有回调方法）
```
class EventEmitter {
    // code
}
const event = new EventEmitter();

event.on('drink', (person) => {
    console.log(person + '喝水');
});
event.on('eat', (person) => {
    console.log(person + '吃东西'); 
});
event.once('buy', (person) => {
    console.log(person + '买东西'); 
});
event.fire('drank','我'); //我喝水
event.fire('drank','我'); //我喝水
event.fire('eat','你'); //你吃东西
event.fire('eat','你'); //你吃东西
event.fire('buy','其他人'); //其他人买东西
event.fire('buy','其他人'); //不会再触发buy事件，因为once只能触发一次
event.off('eat'); //移除eat事件
event.fire('eat','其他人'); //不会触发eat事件，因为已经被移除
```
1. eventEmitter是nodejs中比较基础的一个类
```
class EventEmitter {
    constructor() {
        this.messageBox = {};
    }

    on(eventName, func) {
        const callbacks = this.messageBox[eventName] || [];
        callbacks.push(func);
        this.messageBox[eventName] = callbacks;
    }

    emit(eventName, ...args) {
        const callbacks = this.messageBox[eventName];
        if (callbacks.length > 0) {
            callbacks.forEach((callback) => {
                callback(...args);
            });
        }
    }

    off(eventName, func) {
        const callbacks = this.messageBox[eventName];
        const index = callbacks.indexOf(func);
        if (index !== -1) {
            callbacks.splice(index, 1);
        }
    }
}
```
2. 核心思路是酱紫的,创建一个列表缓存回调函数;当发布者发布时,遍历缓存列表,依次触发回调函数;
```
class EventEmitter {
    constructor() {
        this.eventList = {};
    }
    on(key,fnc) {
        if(!this.eventList[key]) {
            this.eventList[key] = [];
        }
        this.eventList[key].push(fnc);
    }
    emit() {
        let key = Array.prototype.shift.call(arguments),
        fns = this.eventList[key];
        fns.forEach(fn => {
            fn.apply(null,arguments);
        })
    }
    off(key, fn) {
        let fns = this.eventList[key];
        if(!fns) {
            return false;
        }
        else {
            fns.forEach((_fn, index) => {
                if(_fn === fn) {
                    fns.splice(index,1);
                }
            })
        }
    }
}
```