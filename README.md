# Installing a single file python module

Suppose you have a single file python module `mymodule.py`, in a folder `mymodule` (althought the folder name doesn't matter).
Maybe like this:

```python
def hello():
    print("Hello from my simple module")
```

How can you
1. Install it on your own computer so you can just import it into all your other projects?
2. Distribute it to others without going through PyPI (because let's face it, it isn't a really good module)?

## 1. Installing it on your own computer.

All you need is a simple `setup.py` file in the same folder as your `mymodule.py` file:

```python
from setuptools import setup

setup(name="mymodule", version="0.0", author="me", py_modules=["mymodule"])
```
(Here, and everywhere else, replace the name "mymodule" with whatever your module is actually called.) 
Then, in a terminal open inside the folder holding both the `mymodule.py` and `setup.py` files and type

```
py -m pip install ./
```
or
```
py -m pip install -e ./
```
The second case makes an editable install, which allows you to work on the module without reinstalling it.  Whichever install you do, you
can now import `mymodule` and use it, anywhere, e.g

```python
from mymodule import hello

hello()
```
That's it!

If you decide your module sucks, just ininstall it with
```
py -m pip uninstall mymodule
```

## 2. Distributing it without PyPI.

You just need to host your module on github and tell people to install it from the URL. If you want to install `mymodule` the command is:
```
py -m pip install pip install git+https://github.com/w-mcilhagga/single-file-python-module.git
```
**NB this still doesn't work, fixing it**

## References.
I originally found this on [George Shuklin's Medium site](https://medium.com/opsops/packaging-a-single-module-in-python-e8d4388c4664). 
The official documentation for this is at [Setuptools](https://setuptools.pypa.io/en/latest/deprecated/distutils/setupscript.html) which
is "deprecated" but only because more up to date information isn't yet available.


