---
date: 2020-12-11
title: Packaging, ```setuptools``` and imports
---

## ```__init__.py``` files help reduce redundancy in ```import```
https://stackoverflow.com/questions/17457782/how-to-structure-python-packages-without-repeating-top-level-name-for-import

## extra to be added
from keynote
## cookiecutter
## tox
## travis CI
## setuptools
```python setup.py install``` install into site-package directory
```python setup.py develop``` create symlinks to site-package directory(The same as things I did before)
### ```setup.py``` arguments in ```setup()```
#### ```py_modules``` list of single python modules.
#### ```packages``` list of folders that contain the modules
#### ```./setup.py develop``` or ```pip install -e .``` Develope mode
Creates symlinks in site-package path so that reinstallation is not neede when code changes
### data files
#### MANIFEST.in add files to soure distribution. So NOT in wheel but in source. useful when data is used in build time.
#### include_package_data = True + MANIFEST.in include data file into the final package directory. Useful when data is used in the runtime
#### only package_data include data into both source distribution and final package directory
```python
setup(
    ...
    package_data = {
    dir_of_data: [data_if_self], # the data's location is relative to setup.py
    },
)
```
