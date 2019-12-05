Flask

`from flask import Flask, url_for, request, redirect, abort, session`

`redirect` 重定向 `redirect(url_for('login'))`

`abort(401)` 放弃请求并返回错误代码

`session` 

+ `session.pop(key, None)`
+ `session[name]`

`escape（）`  解析编译后的变量

`app = Flask(__name__)`

+ app.logger
  + debug(str)
  + waring(str)
  + error(str)
+ `app.config`
  + from_object( str | dict) 从对象中获取配置
  + form_envvar() 从文件获取配置
+ `@app.route(path)`
  + `/path/<int | path | uuid | string | float>`
    + uuid  接收uuid字符串
    + path 可以包含/的字符串
  + 结尾是否有`/` ，
+ `app.teardown_appcontext()` 告诉Flask在返回响应后进行清理的时候调用此函数
+ `app.cli.add_command()` 添加一个新的可以与flask一起工作的命令

`make_response()` 

`jsonify()` 创建特殊的JSON返回

`request`

+ method
+ files
  + save() 保存到文件系统
  + filename 文件名
+ cookies
  + get(key)
  + set_cookie(key, value)
+ `path`
+ `full_path`
+ `script_root`
+ `url`
+ `base_url`
+ `url_root`
+ `args`
+ `headers`
+ `json`  获取post的数据

```python
@app.route('/login', methods=['POST','GET'])
def login():
	error = None
  if request.method == 'POST':
    if valid_login(request.form['username'], request.form['password']):
      return log_the_user_in(request.form['usernmae'])
    else:
      error = 'Invalid username/password'
      return render_template('login.html', eror=error)
```

`current_app` 当前app

+ `open_resource()` 打开一个文件



## flask shell 

自定义flask shell的全局变量

```python
@app.shell_context_processor:
def make_shell_context():
	return dict(
		db = db
		Note = Note
	)
```

