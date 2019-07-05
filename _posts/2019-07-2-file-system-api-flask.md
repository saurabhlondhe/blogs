---
title:  "Explore file System with Flask"
author: "Saurabh Londhe"
avatar: "img/authors/saurabh.jpg"
image: "img/flask/banner.jpg"
date:   2019-07-02
categories: [Python,Linux,Project]
---

Flask is a microframework for Python based on Werkzeug, Jinja 2 and good intentions. And before you ask: It's BSD licensed[[1]](http://flask.pocoo.org/)

Jinja2 is just a teplating language, means we can keep HTML templates to reuse then and by using its features we can iterate the objects and parse data in HTML.
If you want to know about opensource licenses please check out [here](https://opensource.org/licenses)

So we can create APIs and by using Jinja2 we can create web pages too, But for now just focus on Flask APIs.

## Installed flask? :flushed:

If yes skip to next else here :point_down: is the command
```sh
pip install flask
```
and now you are ready to go.

## Writing first *Hello World* api
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == '__main__':
    app.run(debug=True)
```
Here  `@app.route("/")` is defining a path on which the below method `hello` will be called. We are running app in debug mode so after running program a temporary http server will be created and as you go on changing the code the server will auto detect the changes and restart itself.

 To get the output hit the api call using ```curl``` and get response in JSON,
You can use any approch for api call, either from browser or [Postman](https://www.getpostman.com/downloads/).

In flask `GET` method is by default for any function but we can specify other if we need :+1:

```sh
$ curl -i -H "Accept: application/json" -H "Content-Type: application/json" -X GET http://localhost:5000/

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 12
Server: Werkzeug/0.15.4 Python/3.7.2
Date: Tue, 02 Jul 2019 12:40:21 GMT

Hello World!
```
API responces can of two types either XML or JSON, Here we are expecting a JSON as we have mentioned in curl command.

---

So now lets move to create the actual File System API.
Following libraries will be used for same

-   Flask
-   os
-   errno

### Writing just a path api
This path API will take a argument of filename from route and return it.
In further steps we'll be processing the path :simple_smile:
- Adding parameters in route
  - We can pass parameters in routes such as `/file/<filename>` where `filename` will be considered as an argumant to below function.
  - Here we'll be passisng path of the file so `/files/<path:path>`, here <`path`:path> the first one is datatype and the <path:`path`> is variable name.

```python
#!flask/bin/python
from flask import Flask,jsonify
import os
import errno

app = Flask(__name__)

@app.route('/files/<path:path>')
def index(path):
	return jsonify(path)

if __name__ == '__main__':
    app.run(debug=True)
```

This api will take a input from route and returns it.

![Basic Path API](img/flask/1.png)

### Create a modal that will repesent the data

```python
hierarchy = {
        'type': 'folder',     # type of file (folder/file)
        'name': os.path.basename(path),   # name of file with extension
        'path': path,
    }
```

### Using recursion for nested files :confused:
> For now ignore the recursoin, it'll be clear later. If you don't know what it's checkout [:point_right: :confused:](https://www.google.com/search?q=recursion)
```python
def path_hierarchy(path):
    path_hierarchy(os.path.join(path, contents))
```

### Complete Source code


```python
#!flask/bin/python
from flask import Flask,jsonify
import os
import errno

app = Flask(__name__)

@app.route('/files/<path:path>')
def index(path):
    response = path_hierarchy(path,True)
    return jsonify(response)

def path_hierarchy(path,flag):
    hierarchy = {
        'type': 'folder',
        'name': os.path.basename(path),
        'path': path,
    }
    if flag:
        try:
            hierarchy['children'] = [
                path_hierarchy(os.path.join(path, contents),False)
                for contents in os.listdir(path)
            ]
        except OSError as e:
            if e.errno != errno.ENOTDIR:
                raise
            hierarchy['type'] = 'file'

    return hierarchy


if __name__ == '__main__':
    app.run(debug=True)
```

### Output
Hit the following URL
[http://127.0.0.1:5000/files/c:/](http://127.0.0.1:5000/files/c:/)

output will be similar to the following one.

```json
{
  "children": [
    {
      "name": "$Recycle.Bin", 
      "path": "c:/$Recycle.Bin", 
      "type": "folder"
    },
    {
      "name": "PerfLogs", 
      "path": "c:/PerfLogs", 
      "type": "folder"
    }, 
    {
      "name": "Program Files", 
      "path": "c:/Program Files", 
      "type": "folder"
    }, 
    {
      "name": "Program Files (x86)", 
      "path": "c:/Program Files (x86)", 
      "type": "folder"
    }, 
    {
      "name": "ProgramData", 
      "path": "c:/ProgramData", 
      "type": "folder"
    },
    {
      "name": "System Volume Information", 
      "path": "c:/System Volume Information", 
      "type": "folder"
    }, 
    {
      "name": "Users", 
      "path": "c:/Users", 
      "type": "folder"
    }, 
    {
      "name": "Windows", 
      "path": "c:/Windows", 
      "type": "folder"
    }
  ], 
  "name": "", 
  "path": "c:/", 
  "type": "folder"
}
```