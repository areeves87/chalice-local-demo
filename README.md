Create a virtual environment for installing the requirements-dev.txt
```
$ /usr/local/opt/python@3.8/bin/python3 -m venv venv/python38
$ source venv/python38/bin/activate
$ python --version
> Python 3.8.3
```

Install the requirements
```
$ pip install -r requirements-dev.txt
```

Make a new chalice project
```
chalice new-project helloworld
```

In a separate terminal window, start localstack with
```
localstack start
```

Test helloworld app with local server for correct response. Change into helloworld directory and run `chalice local`. 
```
cd helloworld
chalice local # or chalice-local local
```

In a separate terminal window, `curl localhost:8000/` to get `{"hello":"world"}` 200 response. We can also verify correct response with the local server started by the `chalice-local local` command.
```
curl localhost:8000/
> {"hello":"world"}

```

Deploy helloworld app to localstack with
```
chalice-local deploy
> Creating deployment package.
> Creating IAM role: helloworld-dev
> Creating lambda function: helloworld-dev
> Creating Rest API
> Resources deployed:
>   - Lambda ARN: arn:aws:lambda:us-east-1:000000000000:function:helloworld-dev
>   - Rest API URL: https://xj0gy9hra9.execute-api.us-east-1.amazonaws.com/api/

```

In a separate terminal window, curl the rest api
```
curl http://localhost:4566/restapis/xj0gy9hra9/api/_user_request_/
> {"Code":"InternalServerError","Message":"Unknown request."}
```

Uh-oh! We have a 500 error. See https://github.com/localstack/chalice-local/issues/4 for status on this issue.