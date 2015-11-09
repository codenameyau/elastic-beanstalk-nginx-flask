# elastic-beanstalk-nginx-flask
This is a hello world **Flask** application that runs with AWS **Elastic Beanstalk**
behind **Nginx** and **uWSGI**. Just kidding.

After attempting this myself, I wanted to share my experience trying
to configure Elastic Beanstalk with Nginx. **It's terrible, don't do it.**
Until AWS officially supports Nginx as an alternative to Apache, it's
not worth the effort. You may be able to get away with it by hacking
the configuration files with `.ebextensions`, but in the end your
configuration files will be difficult to understand, and your
deployment process will face unexpected issues that will be
difficult to troubleshoot.

**Note:** Python applications are tied to Apache. If you decide to use
node.js, Elastic Beanstalk will run with nginx instead.

### Still wanna go for it?

If you really want to use Nginx instead of Apache on AWS (I want to too),
my suggestion is to skip EB and use **OpsWorks with Chef** for provisioning.

If for some reason, you still really want to use Nginx with EB,
then here are tutorials that I've tried. They worked up until a certain
point, but **automated deployments ended up failing** because EB ran
pre and post-deployment hooks that triggered unwanted Apache restarts.
If Apache isn't running, then everything breaks. If you're stuck,
SSH into the EC2 instance and examine your logs at `/var/log/eb-activity`,
`/var/log/http`, and `/var/log/nginx`. Good luck!

- [Nginx and EB with Django uWSGI](https://github.com/wolfg1969/elastic-beanstalk-nginx-uwsgi-django)
- [Replacing Apache with Nginx on AWS](http://www.nczonline.net/blog/2012/09/14/replacing-apache-with-nginx-on-elastic-beanstalk/)
- [Official AWS EB Flask Tutorial](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html)


### Running the application

uWSGI Locally:
```
uwsgi --http 127.0.0.1:8000 -w application:application
```

uWSGI Nginx:
```
uwsgi --socket 127.0.0.1:8000 -w application:application
```

Gunicorn:
```
gunicorn application:application
```
