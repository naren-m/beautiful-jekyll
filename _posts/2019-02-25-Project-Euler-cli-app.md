---
layout: post
title: Project Euler Cli app
subtitle: Simple Cli app for accessing Project Euler problems in terminal
published: true
---

# Project Euler Cli app
A simple cli app to show the problems from Project Euler.

Key learning points
1. Building a cil app in python using Fire
2. Making our app pip installable.

Modules used requests and BeautifulSoup.
Code is straight forward, `requests` to get the html content and use `BeautifulSoup` to read the problem form the response which is in `Div problem_content`.

getProblem returns the problem and the url to the problem.

**euler.py**
```python
import requests
import re
from bs4 import BeautifulSoup


class Euler:
    def __init__(self):
        self.baseUrl = 'https://projecteuler.net'
        self.problemUrl = self.baseUrl + '/problem=%s'

    def _generateProblemUrl(self, number):
        if number == None or number == 0 or number == '0':
            return None

        return self.problemUrl % number

    def _getUrlContent(self, url):
        if url == None:
            return None

        r = requests.get(url)
        if r.status_code != requests.codes.ok:
            return None
        return r.content

    def _getProblemFromHtml(self, htmlContent):
        if htmlContent in [None, '']:
            return None

        soup = BeautifulSoup(htmlContent, 'html.parser')

        probNotAvail = soup.findAll(text=re.compile('Problem not accessible'))
        if len(probNotAvail) > 0:
            return None

        try:
            ps = soup.select("div p")
            s = [p.getText().replace('\n', '') for p in ps]
            s = ' '.join(s)
        except:
            return None

        s = s if s != '' else None

        return s

    def getProblem(self, number=None):
        url = self._generateProblemUrl(number)
        if url is None:
            return None, None

        content = self._getUrlContent(url)
        if content is None:
            return url, None

        return url, self._getProblemFromHtml(content)


```

**Folder structure**
```shell

(euler) ➜ (NMUDIVAR-M-422V) euler git:(master) ✗ tree
.
├── README.md
├── euler
│   ├── __init__.py
│   ├── __main__.py
│   ├── euler.py
│   └── test_euler.py
├── euler.egg-info
│   ├── PKG-INFO
│   ├── SOURCES.txt
│   ├── dependency_links.txt
│   ├── entry_points.txt
│   └── top_level.txt
├── makefile
├── requirements.txt
└── setup.py
```

**Setup.py**
To make the app pip installable, we need to have setup.py.  All we do in this is import the setup method from setuptools and pass the values to the arguments. Key argument of this method is entry_points. Using this we tell python to run a module in our app. 

```python
from setuptools import setup

setup(
    name='euler',
    version='0.1.0',
    packages=['euler'],
    entry_points={'console_scripts': ['euler = euler.__main__:main']})

```

**Installing the app using pip during development**

This is as simple as executing below command
```shell
pip3 install -e .
```

**Publishing out app to pypi.**
This i will have to figure out how to do. Will update once figured out. 

#Blogs
#Tutorials