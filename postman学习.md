# postman
[toc]
## 接口关联
### json提取器
```js
var del_userid=JSON.parse(responseBody)
// console.log(del_userid.userlist[1].userid)
//设为全局变量
pm.globals.set("del_userid", del_userid.userlist[1].userid);
```
### 正则提取器
```js
var jsdate=responseBody.match(new RegExp('"sdfhdj(.+?),'))
pm.globals.set("del_userid", del_userid.userlist[1].userid)
```
### cookies提取器
```js
var token=postman.getresponseCookie("token")
pm.globals.set("token",token)
```
## 动态参数
### 内置动态参数
```postman
{{$timestamp}} //获得时间戳
{{$randint}}	//获得0-100随机数（局限）
{{$guid}}	//获得guid字符串（较长）
```
### 自定义动态参数
```js
在pre-request script中自定义变量，然后设置为全局变量

```
自定义函数；接口加密、接口签名、限时请求（3s）
接口加密：可以先在pre-request script中使用js解密
## 接口断言
### 状态断言
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
### 自定义断言
```js
pm.test("返回体有对应字符串", function () {
    pm.response.to.have.body("response_body_string");
});
pm.test("返回json文件有对应字段且正确", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.value).to.eql(100);
});
pm.test("返回有对应字符串", function () {
    pm.expect(pm.response.text()).to.include("string_you_want_to_search");
});
```

## 环境变量
设置好环境变量IP
使用全局变量方式进行调用
在environment中设置一个变量ip，然后可以使用ip，方便切换环境

## mock服务
1. 创建mock服务
2. 查看环境变量
3. 重新修改mock接口返回值以及请求
面试题：
1. 数据交互必有接口
## 接口加密
异步请求：x-requested-with	
请求前sleep4s
在pre-request script中加上代码
```
// //自定义函数，作用是让接口在请求之前先停4s
// const sleep =(milliseconds) => {
// const start =Date.now();
// while (Date.now() <= start +milliseconds){}
// };
// sleep(4000);
```
```
//md5加密
s=CryptoJS.MD5("admin").toString().toUpperCase();
console.log(s)
```
js、接口签名、自定义函数、cookie、session、token；接口类型

