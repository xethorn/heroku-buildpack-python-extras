Heroku buildpack: Python Extras
===============================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps with added support for Gem and Node package dependencies.

It uses:

* [virtualenv](http://www.virtualenv.org/)
* [pip](http://www.pip-installer.org/)
* [bundler](http://gembundler.com/)
* [npm](https://npmjs.org/) (Coming soon...)

Usage
-----

Example usage:

``` bash
$ ls
Procfile  requirements.txt  Gemfile Gemfile.lock web.py
$ heroku create --buildpack git://github.com/LocalMed/heroku-buildpack-python-extras.git
$ git push heroku master
-----> Heroku receiving push
-----> Fetching custom build pack... done
-----> Python app detected
-----> Preparing virtualenv version 1.7.2
       ...
-----> Installing dependencies using pip version 1.1
       ...
-----> Installing gem dependencies using bundler version 1.2.1
       ...
```

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/LocalMed/heroku-buildpack-python-extras.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. It will detect your app as Python/Django if there is an additional `settings.py` in a project subdirectory.

It will use virtualenv and pip to install your dependencies, vendoring a copy of the Python runtime into your slug.  The `bin/`, `include/` and `lib/` directories will be cached between builds to allow for faster pip install time.

It will also detect gem dependencies (maybe you're using Sass) and install them using bundler.

Hacking
-------

To use this buildpack, fork it on Github.  Push up changes to your fork, then create a test app with `--buildpack <your-github-url>` and push to it.

To change the vendored virtualenv, unpack the desired version to the `src/` folder, and update the virtualenv() function in `bin/compile` to prepend the virtualenv module directory to the path. The virtualenv release vendors its own versions of pip and setuptools.
