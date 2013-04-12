Heroku buildpack: Python Extras
===============================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps with added support for Gem and Node package dependencies.

It uses:

* [pip](http://www.pip-installer.org/)
* [bundler](http://gembundler.com/)
* [npm](https://npmjs.org/)

Additional (optionally) included libraries:

* [libmemcached](http://libmemcached.org/libMemcached.html)
* [GEOS](http://trac.osgeo.org/geos/)

Installation
------------

Use [heroku-buildpacks](https://github.com/heroku/heroku-buildpacks):

``` bash
$ heroku plugins:install https://github.com/heroku/heroku-buildpacks
$ heroku buildpacks:set localmed/python-extras
```

Usage
-----

``` bash
$ ls
Procfile  requirements.txt  Gemfile  Gemfile.lock  web.py

$ git push heroku master
...
-----> Fetching custom tar buildpack... done
-----> Python app detected
-----> No runtime.txt provided; assuming python-2.7.4.
-----> Preparing Python runtime (python-2.7.4)
-----> Installing Distribute (0.6.36)
-----> Installing Pip (1.3.1)
-----> Installing dependencies using Pip (1.3.1)
       ...
-----> Installing gem dependencies using bundler version 1.2.1
       ...
-----> Installing node packages using npm version 1.0.106
       ...
```

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. 

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug.

### Gem Dependencies

If your project contains a `Gemfile`, bundler will be used to install Gem dependencies.

### Node Dependencies

If your project contains a `package.json`, npm will be used install Node dependencies.

### Specify a Runtime

You can also provide arbitrary releases Python with a `runtime.txt` file.

``` bash
$ cat runtime.txt
python-3.3.0
```
    
Runtime options include:

- python-2.7.3
- python-3.3.0
- pypy-1.9 (experimental)
