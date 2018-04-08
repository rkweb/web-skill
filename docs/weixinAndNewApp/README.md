## 微信授权问题
>后台会给你提供:
>* 一个微信授权链接类似这种（authorize_url）：
https://open.weixin.qq.com/connect/oauth2/authorize?appid=wx41cc878a253b1ba2&redirect_uri=http%3A%2F%2Fgo.163.com%2F2017%2F0721%2Fsiemens%2Findex.html&response_type=code&scope=snsapi_userinfo&state=1#wechat_redirect
>* 一个提交code值的接口如:common.php?act=getUserInfo

1. 判断是不是微信端打开h5;
2. 判断h5 url中是否含有 code 参数;
3. 如果不含有code参数,则页面跳转微信授权链接authorize_url;
&nbsp;&nbsp;&nbsp;如果含有code参数获取到code参数值，并把code值通过接口提交给后台，后台会返回微信用户的信息;

>*tips*:如果分享出去的链接带code参数的话，那就需要判断下h5 url中的code 参数是微信授权返回的code还是分享出去的code;如果是微信授权返回的code，则可以提交后台，如果不是则跳转微信授权链接;（可在分享链接时，在后面加一个flag参数，用来标记code参数是分享出去)~

>微信授权演示代码：
```javascript
 if(netease.ua.weixin){ 
    if(window.location.search.indexOf('code') > -1){
        var code = netease.getPara('code'); //自行获取URL参数code
        $.ajax({
            url:'', //后台提供getUserInfo接口地址
            type:'POST',
            dataType:'json',
            data:{
                'code':code
            },
            success:function(data){
                if(data.retCode==1){
                    // 返回 昵称、头像等信息 
                }
            },
            error:function(){
            }
        });
    }else if(window.location.search.indexOf('code') == -1) {
        setTimeout(function(){
            window.location.href = 'https://open.weixin.qq.com/connect/oauth2/authorize?appid=wx41cc878a253b1ba2&redirect_uri=http%3A%2F%2Fgo.163.com%2F2018%2F0115%2FHongKong%2Findex.html&response_type=code&scope=snsapi_userinfo&state=1#wechat_redirect';  // 授权链接后台提供，需要自行替换
        }, 20)
    }
}
```
## 网易新闻客户端登录问题

* 客户端支持协议『userinfo://』，用来获取用户信息。客户端会回调『__newsapp_userinfo_done(info)』来返回用户信息,其中info是一个字典，格式{name:"用户名",nickname:"昵称",head:"头像url",loginType:"netease"}

* 客户端支持协议『login://』，客户端会通过该协议为活动页面提供用户登录信息（若客户端当前未登录将调用原生登录界面），登录验证成功后，客户端会回调『__newsapp_login_done(info)』来返回用户信息,其中info是一个字典，格式{name:"用户名",nickname:"昵称",head:"头像url",loginType:"netease"}。

> 以下代码必须放在全局作用域下才能生效，新闻客户端演示代码：
```javascript
window.addEventListener("load",function(){
    if(netease.ua.newsapp){
        window.location="userinfo://";    
    }
},false);

var isLogin = false; //判断是否登录状态
//跳转 userinfo://协议时，新闻客户端会自动的回调
function __newsapp_userinfo_done(info){         
    if(info && info.name){
        // info.nickname 返回昵称，info.head 返回头像url
        isLogin = true;
        window.location="login://";  //这行必须要用，后台通过此行取用户登录信息  
    }
}

//跳转 login:// 协议时，新闻客户端会自动的回调
function __newsapp_login_done(info){  //登录完成后
   //跳转'login://' 协议的回调
    if(info && info.name){
        // info.nickname 返回昵称，info.head 返回头像url
        isLogin = true;
    }else{
        isLogin = false;
    }
}

//当页面需要弹出登录框时,通过isLogin 状态去判断
if(!isLogin){
    window.location  = "login://"   // 如果位未登录，会唤起新闻客户端的登录页面，登录成功后会自动回调 __newsapp_login_done 函数
}
```






