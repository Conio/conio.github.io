<!-- PROJECT LOGO -->
<br/>
<p align="center">
	<h1 align="center">Conio SDK Documentation</h3>
	</p>
</p>

<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
* [Prerequisites](#prerequisites)
* [Deploy](#deploy)
* [Contacts](#contact)

## About The Project
This is the official Conio SDK documentation repository for both platforms Android and iOS.

The whole documentation is written in [Markdown](https://it.wikipedia.org/wiki/Markdown) and the [documentation site](https://sdk-docs.conio.com/) is generated
through [MkDocs](https://www.mkdocs.org/).

In order to correctly maintain and update the documentation, you need to install and setup `MkDocs`.


## Prerequisites
### MacOS
1. Install [Brew](https://brew.sh/)

2. Install [Pip](https://pip.pypa.io/en/stable/installation/#supported-methods)

	2.1 `brew install python`
	
	2.2 `brew unlink python && brew link python`

3. Install [Python3](https://www.python.org/) with `brew install python3`

4. Upgrade [Pip](https://pypi.org/project/pip/) with `pip3 install --upgrade pip`

5. Install MkDocs with `pip3 install mkdocs`

6. Install [MkDocs Material Extensions](https://pypi.org/project/mkdocs-material-extensions/) with `python3 -m pip install mkdocs-material-extensions`

7. Install [mkdocs-i18n](https://pypi.org/project/mkdocs-i18n/) for internationalization with `pip install mkdocs-i18n`

8. Install [mkdocs-pdf-export-plugin](https://pypi.org/project/mkdocs-pdf-export-plugin/) (NB: it requires other dependencies as described [here](https://doc.courtbouillon.org/weasyprint/latest/first_steps.html#macos))

### Linux
1. Check to see if [Python3](https://www.python.org/) is installed on the system (the python3 program corresponds to Python 3 and python corresponds to Python 2):
	```
	$ which python3
	/usr/bin/python3
	$ python3 --version
	Python 3.4.2
	```
	If necessary, install Python: `$ sudo apt-get install python3`

2. Check to see if [Pip](https://pypi.org/project/pip/): is installed
	```
	$ which pip3
	/usr/bin/pip3
	$ pip3 --version
	pip 1.5.6 from /usr/lib/python3/dist-packages (python 3.4)
	```
	If pip3 is not installed, install it: `$ sudo apt-get install python3-pip`

3. Install MkDocs with `$ pip3 install mkdocs`

4. Install [MkDocs Material Extensions](https://pypi.org/project/mkdocs-material-extensions/) with `$ pip3 install mkdocs-material`

5. Install [mkdocs-i18n](https://pypi.org/project/mkdocs-i18n/) for internationalization with `$ pip3 install mkdocs-i18n`

6. Install [mkdocs-pdf-export-plugin](https://pypi.org/project/mkdocs-pdf-export-plugin/) (NB: it requires other dependencies as described [here](https://doc.courtbouillon.org/weasyprint/latest/first_steps.html#linux))


Please refer to official [MkDocs documentation](https://www.mkdocs.org/user-guide/writing-your-docs/) to update and/or modify generated site settings/layout and to [MkDocs Material theme](https://squidfunk.github.io/mkdocs-material/) to customize theme.

## Build and test
[MkDocs](https://www.mkdocs.org/getting-started/#creating-a-new-project) comes with a built-in dev-server that lets you preview your documentation as you work on it.
Simply run `mkdocs serve` from root folder and go [here](http://127.0.0.1:8000).

The dev-server also supports auto-reloading, and will rebuild your documentation whenever anything in the configuration file, documentation directory, or theme directory changes.

If you add new `*.md` files, you will need to execute `mkdocs build` in order to generate new pages, check [here](https://squidfunk.github.io/mkdocs-material/) for more info.

## Deploy
Once docs are updated and pushed to repository, you will need to deploy the new site with `mkdocs gh-deploy --force` command.

Check your changes visiting https://sdk-docs.conio.com/

## Contacts

* Alessandro Farina - alessandro.farina@conio.com
* Beatrice Buran - beatrice.buran@conio.com
* Giovanni Di Donato - giovanni@conio.com
