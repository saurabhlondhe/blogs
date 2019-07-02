---
title:  "Explore file System with Flask"
author: "Saurabh Londhe"
avatar: "img/authors/saurabh.jpg"
image: "img/flask/banner.jpg"
date:   2019-07-02
categories: [Python,Linux,Project]
---

Flask is a microframework for Python based on Werkzeug, Jinja 2 and good intentions. And before you ask: It's BSD licensed[[1]](http://flask.pocoo.org/)

So we can create APIs and by using Jinja2 we can create web pages too, But for now just focus on Flask APIs.

## Installed flask?

If yes skip to next else here is the command
```sh
pip install flask
```
and now you are ready to go.

## Writing first *_Hello World_* api
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == '__main__':
    app.run(debug=True)
```
Hit the api call using ```curl``` and get response in JSON
```sh
$ curl -i -H "Accept: application/json" -H "Content-Type: application/json" -X GET http://localhost:5000/

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 12
Server: Werkzeug/0.15.4 Python/3.7.2
Date: Tue, 02 Jul 2019 12:40:21 GMT

Hello World!
```