```
fron flask import Flask, render_template, redirect, Response

# 导出json数据
import json
Renponse(json.duos())

# 路由
@app.route('/login', methods=["GET", "POST"])

@app.route('/art/edit/<int:id>/', methods=["GET"])
def art_edit(id):
	mdict = dict(id = id)
	return render_template("art_edit.html", mkdict = mdict) 
	# 获取数据 mkdict.id  mkdict["id"]
	
app.run(debug=True, port=8888, host='0.0.0.0')
```

