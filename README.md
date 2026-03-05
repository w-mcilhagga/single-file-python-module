# Installing a single file python module

Suppose you have a single file python module `mymodule.py`. Maybe like this:

##### `mymodule.py`:
```python
def hello():
    print("Hello from my simple module")
```

How can you
1. Install it on your own computer so you can just import it into all your other projects?
2. Distribute it to others without going through PyPI (because let's face it, it isn't really all that great)?

## 1. Installing it on your own computer.
A google for how to install a python script brings up a whole lot about `pyproject.toml`, packages, `__init__.py` and so on. 
**Not necessary**, and overkill for a single file. All you need is a simple `setup.py` file in the same folder as your `mymodule.py` file:

##### `setup.py`:
```python
from setuptools import setup

setup(name="mymodule", version="0.0", author="me", py_modules=["mymodule"])
```
(Here, and everywhere else, replace the name "mymodule" with whatever your module is actually called.) 
Then in a terminal, go to the folder holding both the `mymodule.py` and `setup.py` files and type (on windows):

```
py -m pip install .
```
or
```
py -m pip install -e .
```
The `-e` makes an "editable" install, which allows you to change and edit the module without needing to reinstall it.  Whichever install you do, you
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

To distribute your module, you just need to host it on github (like `mymodule` is) and tell people to install it from a URL. 
If you want to install `mymodule` from **this** repository, the command is:
```
py -m pip install git+https://github.com/w-mcilhagga/single-file-python-module.git
```
For your own module, just replace the `w-mcilhagga/single-file-python-module` with the repo you want.

## Dependencies.

What if your single file python module imports some package outside of the standard library, and maybe needs a specific
python version? Then you need to change your `setup.py` to 
include this information. For example, if you need python version 3.10 or later, and say, the [wikipedia](https://pypi.org/project/wikipedia/) package, 
then your `setup.py` file should look like this:

```python
from setuptools import setup

setup(
    name="mymodule",
    version="0.0",
    author="me",
    py_modules=["mymodule"],
    python_requires=">=3.10",
    install_requires=["wikipedia"],
)
```
Again, you can get involved with `pypackage.toml`, `setup.cfg` and whatnot, but it's only a single file module, so why would you want to cause
yourself so much pain? 

More details about these
options can be found on the [setuptools page](https://setuptools.pypa.io/en/latest/userguide/dependency_management.html#declaring-dependencies).

## References.
I originally found this information on [George Shuklin's blog](https://medium.com/opsops/packaging-a-single-module-in-python-e8d4388c4664)
so :thumbsup: to him. 
The official documentation for this is at [Setuptools](https://setuptools.pypa.io/en/latest/deprecated/distutils/setupscript.html) which
is "deprecated" but only because more up to date information isn't yet available.


