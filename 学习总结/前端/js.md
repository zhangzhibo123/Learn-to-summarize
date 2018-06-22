```javascript
for (var i = 0; i <= arr.length; i++){
    var obj = arr[i]
}
```

```javascript
for (var index in  arr) {
        var obj = arr[index];
        alert(obj)
    }
```

http协议 请求方式

```
get  post ,put ,delete
```

````
请求方式
	get  post ,put ,delete
	get
		浏览器上面直接把参数放到?后面
	post
		application/x-www-form-urlencoded 跟get请求没太多区别,唯一的区别是post请求的数据放在请求体里面
		multipart/form-data
	如果说要传文件 必须条件
		post
		multipart/form-data
````

