[參考網站](http://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask)


### Configuration: pyenv, flask

```
brew update
brew install pyenv
pyenv init
pip install flask
```

sample code => hello world 成功


### first entry point of our web service: a get

```
@app.route('/miro/api/v1.0/music/<string:sentence>', methods=['GET'])
def get_music(sentence):
    return sentence
```

testing by curl
`$ curl -i http://localhost:5000/todo/api/v1.0/tasks`

```
YestekiMacBook-Pro:src Yes$ curl -i http://localhost:5000/miro/api/v1.0/music/gg
HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 2
Server: Werkzeug/0.11.3 Python/3.5.1
Date: Sat, 16 Jan 2016 03:06:27 GMT
gg
```
