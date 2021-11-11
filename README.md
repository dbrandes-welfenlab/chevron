Modifications of this Fork
--------------------------

This is a modfied version of Mustache, `chevron_strict`. The following changes are made

- force error if key not found and template is no {{#...}} or {{^...}}
- do not look in scopes over actl. scope to find variables
- force error if partial is not found
- default do no html escaping!
- fixes internal tests
- changed to forked version of specs that are compatible with changes above.


Original Readme
---------------

A python implementation of the [mustache templating language](http://mustache.github.io).

Why chevron?
------------

I'm glad you asked!

### chevron is fast ###

Chevron runs in less than half the time of [pystache](http://github.com/defunkt/pystache) (Which is not even up to date on the spec).
And in about 70% the time of [Stache](https://github.com/hyperturtle/Stache) (A 'trimmed' version of mustache, also not spec compliant).

### chevron is pep8 ###

The flake8 command is run by [travis](https://travis-ci.org/noahmorrison/chevron) to ensure consistency.

### chevron is spec compliant ###

Chevron passes all the unittests provided by the [spec](https://github.com/mustache/spec) (in every version listed below).

If you find a test that chevron does not pass, please [report it.](https://github.com/noahmorrison/chevron/issues/new)

### chevron is Python 2 and 3 compatible ###

Python 2.6, 2.7, 3.2, 3.3, 3.4, 3.5, and 3.6 are all tested by travis.



USAGE
-----

Commandline usage: (if installed via pypi)
```
usage: chevron [-h] [-v] [-d DATA] [-p PARTIALS_PATHS] [-e PARTIALS_EXT]
               [-l DEF_LDEL] [-r DEF_RDEL]
               template

positional arguments:
  template              The mustache file

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -d DATA, --data DATA  The json data file
  -p PARTIALS_PATHS, --paths PARTIALS_PATHS
                        The directories where your partials reside
  -e PARTIALS_EXT, --ext PARTIALS_EXT
                        The extension for your mustache partials, 'mustache'
                        by default
  -l DEF_LDEL, --left-delimiter DEF_LDEL
                        The default left delimiter, "{{" by default.
  -r DEF_RDEL, --right-delimiter DEF_RDEL
                        The default right delimiter, "}}" by default.
```

Python usage with strings
```python
import chevron

chevron.render('Hello, {{ mustache }}!', {'mustache': 'World'})
```

Python usage with file
```python
import chevron

with open('file.mustache', 'r') as f:
    chevron.render(f, {'mustache': 'World'})
```

Python usage with unpacking
```python
import chevron

args = {
  'template': 'Hello, {{ mustache }}!',

  'data': {
    'mustache': 'World'
  }
}

chevron.render(**args)
```

chevron supports partials (via dictionaries)
```python
import chevron

args = {
    'template': 'Hello, {{> thing }}!',

    'partials_dict': {
        'thing': 'World'
    }
}

chevron.render(**args)
```

chevron supports partials (via the filesystem)
```python
import chevron

args = {
    'template': 'Hello, {{> thing }}!',

    # defaults to .
    'partials_paths': ['partials/'],

    # defaults to mustache
    'partials_ext': 'ms',
}

# ./partials/thing.ms will be read and rendered
chevron.render(**args)
```

chevron supports lambdas
```python
import chevron

def first(text, render):
    # return only first occurance of items
    result = render(text)
    return [ x.strip() for x in result.split(" || ") if x.strip() ][0]

def inject_x(text, render):
    # inject data into scope
    return render(text, {'x': 'data'})

args = {
    'template': 'Hello, {{# first}} {{x}} || {{y}} || {{z}} {{/ first}}!  {{# inject_x}} {{x}} {{/ inject_x}}',

    'data': {
        'y': 'foo',
        'z': 'bar',
        'first': first,
        'inject_x': inject_x
    }
}

chevron.render(**args)
```

INSTALL
-------

- with git
```
$ git clone https://github.com/noahmorrison/chevron.git
```

or using submodules
```
$ git submodules add https://github.com/noahmorrison/chevron.git
```

Also available on pypi!

- with pip
```
$ pip install chevron
```



TODO
---

* get popular
* have people complain
* fix those complaints
