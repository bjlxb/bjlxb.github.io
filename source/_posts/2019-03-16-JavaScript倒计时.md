---
layout: photo
title: JavaScript倒计时
tags:
  - JavaScript
date: 2019-03-16 22:34:27
categories: JavaScript
photos:
---
记录一下之前项目中用到的倒计时功能。

<!--more-->
## 1.传入一个结束时间的时间戳，实现倒计时。
```javascript
function leftTime(datetime_expire) {
    maxtime = parseInt(parseInt(datetime_expire) - (parseInt(new Date().getTime())/1000));

    function CountDown() {
        --maxtime;
        if (maxtime >= 0) {
            minutes = Math.floor(maxtime / 60);
            seconds = Math.floor(maxtime % 60);
            document.getElementById("i").innerHTML = minutes;
            document.getElementById("s").innerHTML = seconds;
            console.log(minutes + "分钟" + seconds + "秒");
        } else {
            document.getElementById("i").innerHTML = "00";
            document.getElementById("s").innerHTML = "00";
            clearInterval(timer);
            alert("时间到，结束!");
        }
    }
    timer = setInterval(CountDown, 1000);
}
```
## 2.短信倒计时功能。
```javascript
//val为需要修改为显示倒计时的按钮，一般为this
//countdown为倒计时时间，单位为秒，一般为60或120
//is_clear为是否将Timeout清除，用于后台请求返回错误时，可以让用户无需等待重新发送验证码。
function settime(val, countdown,is_clear=false) {
    if (countdown == 0) {
        val.removeAttribute("disabled");
        val.innerHTML="重新发送";
        countdown = 60;
    } else {
        val.setAttribute("disabled", true);
        val.innerHTML="重新发送(" + countdown + "s)";
        countdown--;
        setTimeout(function() {
            settime(val, countdown);
        },1000)
    }
    if(is_claer == true){
        clearTimeout(param);
    }
}
```