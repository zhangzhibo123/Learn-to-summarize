```
<form 
    name="test" 
    action="form_action.action" 
    method="get">
</form>
```

```
1. name：表单提交时的名称
2. action：提交到的地址
3. method：规定用于发送 form-data 的 HTTP 方法，提交方式：get和post
4. enctype：规定在发送表单数据之前如何对其进行编码
   - application/x-www-form-urlencoded：在发送前编码所有字符（默认）
   - text/plain：空格转换为 "+" 加号，但不对特殊字符编码
   - multipart/form-data：使用包含文件上传控件的表单时，必须使用该值
```

文件上传

```
单文件上传<input type="file"/>
多文件上传<input type="file" multiple/>
只上传图片<input type="file" accept="image/*"> <!--accept属性指定上传文件的类型-->
```

