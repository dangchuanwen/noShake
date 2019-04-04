### 防抖与节流
防抖与节流是前端最基本的优化技巧，实现很简单，为了记录下，可供学习参考。
#### 防抖
##### 概念：
    > 防抖就是在持续触发事件的时候，只有当不触发事件一段时间后才会执行处理的函数，当触发一次事件后，在规定事件内再次触发，
    > 就会清除上次的定时任务，重新创建定时任务，下面看代码
##### 代码：
    //防抖
    function noShake (fn, delay) {
        var timer = null;
        return function () {
            clearTimeout(timer);
            timer = setTimeout(() => {
                fn();
            }, delay);
        }
    }
    //防抖测试 使劲的点击触发
    var clickFn = noShake(function () {
        console.log("I am clicking!");
    }, 300);
    window.addEventListener('click', function () {
        clickFn();
    })
##### 运行
    将该代码复制到一个 html 文件下即可，然后浏览器打开，使劲点击即可看到效果
##### 说明
    在此用到了闭包的概念，每次调用 noShake 函数会返回一个事件函数，每个返回的事件函数都会有一个独立的 闭包
#### 节流
##### 概念：
    > 节流就是在持续触发事件的时候，利用标志位进行控制处理函数是否执行，比如为 true 执行，为 false 不执行
    > 通过指定间隔时间修改标志位的值即可实现在指定时间内只触发一次处理函数
##### 代码：
    //节流
    function throttle (fn, delay) {
        var ing = false;
        return function () {
            if (!ing) {
                fn();
                ing = true;
                setTimeout(() => {
                    ing = false;
                }, delay);
            }
            else {

            }
        }
    }
    //节流测试   使劲的点击触发
    var hoverFn = throttle(function () {
        console.log("I am hover the window");
    }, 1000);
    window.addEventListener('click', function () {
        
        hoverFn();
    })
##### 运行
    将该代码复制到一个 html 文件下即可，然后浏览器打开，使劲点击即可看到效果
##### 说明
    在此用到了闭包的概念，每次调用 throttle 函数会返回一个事件函数，每个返回的事件函数都会有一个独立的 闭包
