---
published: true
---
## Anaconda

### Introduction
We are using Anaconda to manage packages and environments for use with Python. With Anaconda, it's simple to install the
packages you'll often use in data science work. You'll also use it to create virtual environments that make working on
multiple projects much less mind-twisting. Anaconda has simplified my workflow and solved a lot of issues I had dealing 
with packages and multiple Python versions.


Conda is also a virtual environment manager. It's similar to virtualenv and pyenv, other popular environment managers.

[Installation instructions for Anaconda](https://www.continuum.io/downloads)

***
### Managing Packages
Once you have Anaconda installed, managing packages is fairly straightforward. To install a package, 
type in your terminal. 
***conda install package_name***
For example, to install numpy 
```bash
conda install numpy
```
You can install multiple packages at the same time. Something like 
```bash
conda install numpy scipy pandas
``` 
will install all those packages simultaneously. 
It's also possible to specify which version of a package you want by adding the version number such as 
```bash
conda install numpy=1.10
```

Conda also ___automatically installs___ dependencies for you. For example scipy depends on numpy, it uses and requires 
numpy. If you install just scipy Conda will also install numpy if it isn't already installed. 
```bash
conda install scipy
``` 


Most of the commands are pretty intuitive. To uninstall, use ***conda remove package_name***. 
To update a package ***conda update package_name***. If you want to update all packages in an environment, 
which is often useful, use 
```bash
conda update --all.
```
And finally, to list installed packages, it's 
```bash
conda list
```

If you don't know the exact name of the package you're looking for, you can try searching with 
***conda search search_term***. For example, I know I want to install Beautiful Soup, but I'm not 
sure of the exact package name. So, I try 
```bash
conda search beautifulsoup.
```
It returns a list of the Beautiful Soup packages available with the appropriate package name, beautifulsoup4.

***

### Managing environments
Conda can be used to create environments to isolate your porjects


Creating conda environment  (-n for name)
```bash
conda create -n env_name list of packages
```

Example
```bash
conda create -n my_env numpy
```

 
To create an environment with a specific Python version, do something like conda 
```bash
create -n py3 python=3 
or 
conda create -n py2 python=2
```


***
### Entering an environment

Activating conda environment
```bash
source activate my_env
```
Checking installed package list in conda env
```bash
conda list
```

Deactivating conda environment
```bash
source deactivate
 ```
 
***
### Saving and loading environments

A really useful feature is sharing environments so others can install all the packages used in your code, with the 
correct versions. You can save the packages to a YAML file with 
```bash
conda env export > environment.yaml
```

The first part ***conda env export*** writes out all the packages in the environment, including the Python version.
The second part of the export command, ***> environment.yaml*** writes the exported text to a 
YAML file ***environment.yaml***


***Listing environments***
```bash
conda env list
```

***Removing environments***
```bash
conda env remove -n env_name
```
