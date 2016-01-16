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

### deploy to aws [elastic beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-apps.html)
```
pip install awsebcli
np
```

`eb init`
ERROR: The current user does not have the correct permissions. Reason: Operation Denied. The security token included in the request is invalid.
```
Next, provide your access key and secret key so that the EB CLI can manage resources for you. Access keys are created in the AWS Identity and Access Management management console. If you don't have keys, see How Do I Get Security Credentials? in the Amazon Web Services General Reference.
```
IAM > Users > Security Credentials > Access Keys

```
eb create (User need createRole policy)
eb status
eb deploy
eb open
```
