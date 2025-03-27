# Flask Cheat Sheet
## Import
`from flask import Flask`

Other modules include: `render_template`, `request`, `redirect`, `session`, and more
## Create an App
`app = Flask(__name__)`
## Run an App
`app.run()`
## Defining Routes
### The "Root" Route
```
@app.route('/')
def route_function():
  return 'HTML content'
```
### Other Routes
```
@app.route('/route')
def route_function():
  return 'HTML content'
```
### Returns
Routes must **ALWAYS** return something.

`return 'HTML content'`

`return render_template('index.html')`

`return render_template('index.html', t_var='value')`

`return redirect('/')`
## Route Variables
### String
```
@app.route('/route/<route_variable>')
def route_function(route_variable):
  return 'HTML content'
```
### Int
```
@app.route('/route/<int:route_variable>')
def route_function(route_variable):
  return 'HTML content'
```
### Multiple
```
@app.route('/route/<route_variable1>/<route_variable2>')
def route_function(route_variable1, route_variable2):
  return 'HTML content'
```
## Methods and Requests
```
@app.route('/route', methods=['GET', 'POST'])
def route_function():
  if request.method == 'GET':
    return 'HTML content'
  else:
    return 'HTML content'
```
## Forms
### Route Receiving Form Data
`@app.route('/route', methods=['POST'])`
### Get a Form Field Value
`request.form.get('name_attribute')`
## Templates
HTML templates should be placed inside a templates directory. This is where Flask will look for the files you tell it to render.

`return render_template('index.html')`
### Template Variables
**python**
```
return render_template('index.html', t_var='value')
```

**html**
```
<p>{{tvar}}</p>
```
### Template Logic
#### If Statements
**python**
```
return render_template('index.html', t_var='value')
```

**html**
```
{% if t_var == 'value' %}
  <p>{{t_var}}</p>
{% else %}
  <p>Other value.</p>
{% endif %}
```
#### Loops
**python**
```
my_list = ["a", "b", "c", "d"]
return render_template('index.html', t_var=my_list)
```

**html**
```
{% for item in t_var %}
  <p>{{item}}</p>
{% endfor %}
```

---

**python**
```
my_list = [ ["a", "b", "c"], ["a", "b", "c"], ["a", "b", "c"] ]
return render_template('index.html', t_var=my_list)
```

**html**
```
{% for item in t_var %}
  <p>{{item[0]}} {{item[1]}} {{item[2]}}</p>
{% endfor %}
```

---

**python**
```
my_list = [ {"name": "a"}, {"name": "b"}, {"name": "c"} ]
return render_template('index.html', t_var=my_list)
```

**html**
```
{% for item in t_var %}
  <p>{{item['name']}}</p>
{% endfor %}
```
### Template Inheritance
**python**
```
return render_template('index.html')
```
**Parent Template**: layout.html
```
<html>
<body>
...
{% block content %}
{% endblock %}
...
</body>
</html>
```

**Child Template**: index.html
```
{% extends "layout.html" %}
{% block content %}
  <p>Content!</p>
{% endblock %}
```
## Responses
`from flask import make_response`

```
resp = make_response(redirect('/'))
return resp
```
