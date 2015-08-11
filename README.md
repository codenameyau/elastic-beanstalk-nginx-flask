# elastic-beanstalk-nginx-flask
This is a hello world **Flask** application that runs with AWS **Elastic Beanstalk**
behind **Nginx** and **uWSGI**.

### Running the application

Locally:
```
uwsgi --http 127.0.0.1:8000 -w wsgi:app
```

Nginx:
```
uwsgi --socket 127.0.0.1:8000 -w wsgi:app
```
