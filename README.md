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
1. Install [Brew](https://brew.sh/)
2. Install [Python3](https://www.python.org/) with `brew install python3`
3. Upgrade [Pip](https://pypi.org/project/pip/) with `pip3 install --upgrade pip`
4. Install MkDocs with `pip3 install mkdocs`
5. Install [MkDocs Material Extensions](https://pypi.org/project/mkdocs-material-extensions/) with `python3 -m pip install mkdocs-material-extensions`

Please refer to official [MkDocs documentation](https://www.mkdocs.org/user-guide/writing-your-docs/) to update and/or modify generated site layout and settings.

## Build and test
[MkDocs](https://www.mkdocs.org/getting-started/#creating-a-new-project) comes with a built-in dev-server that lets you preview your documentation as you work on it.
Simply run `mkdocs serve` from root folder and go [here](http://127.0.0.1:8000).

The dev-server also supports auto-reloading, and will rebuild your documentation whenever anything in the configuration file, documentation directory, or theme directory changes.

## Deploy
Once docs are updated and pushed to repository, you will need to deploy the new site with `mkdocs gh-deploy` command.

Check your changes visiting https://sdk-docs.conio.com/

## Contacts

* Matteo Gazzato - matteo.gazzato@conio.com
* Giovanni Di Donato - giovanni@conio.com
