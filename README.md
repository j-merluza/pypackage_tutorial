# 📂 Packaging Python and using GitHub as a private (PyPI) server

This tutorial is a summarization of the following resources:

- https://medium.com/network-letters/using-github-as-a-private-python-package-index-server-798a6e1cfdef
- https://packaging.python.org/en/latest/tutorials/packaging-projects/#generating-distribution-archives
- https://packaging.python.org/en/latest/guides/writing-pyproject-toml/
- https://packaging.python.org/en/latest/specifications/pypirc/
- https://stackoverflow.com/questions/9727673/list-directory-tree-structure-in-python

---

## Set up project directory
Let's take this project directory for example:
```
pypackage_tutorial
└── MyPackage
    ├── example.py
    └── __init__.py
```

- `MyPackage` - is the folder name that would contain the python modules. Keep in mind, this is name you will be importing. Example: `import MyPackage`
- `__init__.py` - is always recommended to have so you can import as a regular package. 
- `example.py` - is the python module containing the below function:

```
def add_one(num):
  return num + 1
```

---

## Creating package files
There are additional files you would need to create in the root folder which are required for preparing your python project for distribution. 

- `README.md` - a read me document is required to provide details about what your project is, how to install it and use it. It’s recommended to have this document. 
- `pyproject.toml` - this file is basically the configuration file that contains requirements, version and meta data information for the building process. 
- `LICENSE` - It’s important for every package published to pypi should have a license. HOWEVER, the package in this scenario is only to be used within an organization. So, in this case, we do not need a license. For help choosing a license, you can go here: Choose an open source license | Choose a License

After creating these files, your directory should now look like this:

```
pypackage_tutorial
├── LICENSE
├── MyPackage
│   ├── example.py
│   └── __init__.py
├── pyproject.toml
└── README.md
```

## Configurating your pyproject.toml file
For this section, I figured it would be best to following along the python documentation that outlines what to put into this file and how. https://packaging.python.org/en/latest/guides/writing-pyproject-toml/

Note: there are some configurations that are not listed here, for example, adding data files as part of your package, but you can find resources online like the link here: https://stackoverflow.com/questions/69647590/specifying-package-data-in-pyproject-toml

## Generate distribution files
After you have all files created and your `pyproject.toml` file set up, you can proceed with the pip build process which generates the distribution files required. 

Make sure to have the latest version of the build.
```
python -m pip install --upgrade build
```
In the same directory as the pyproject.toml file, run the below command.
```
python -m build
```

This will generate a lot of lines in your terminal and in the end it will generate a dist folder. 

## Publish
In the last section of the python resource of packaging, it explains how to upload to PyPi for all to see, but in our case, we do not want to publish here since the packages we are developing is only meant to be used within our organization. 

So, instead, we just git commit our project to our GitHub repository. You can `.gitignore` the `pyproject.toml` file and various dist folders.

## Installation
Now, everyone can follow the below code to install your package!

```
pip install git+https://github.com/j-merluza/pypackage_tutorial.git
```