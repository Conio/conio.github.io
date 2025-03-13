<!-- PROJECT LOGO -->
<br/>
<p align="center">
	<h1 align="center">Conio SDK Documentation</h3>
	</p>
</p>

## Table of Contents

* [About the Project](#about-the-project)
* [Prerequisites](#prerequisites)
* [Build and test](#build-and-test)
* [Deploy](#deploy)
* [Notes](#notes)
* [Contacts](#contact)

## About The Project

This is the official Conio SDK documentation repository for both platforms Android and iOS.

The whole documentation is written in [Markdown](https://it.wikipedia.org/wiki/Markdown) and the [documentation site](https://sdk-docs.conio.com/) is generated
through [MkDocs](https://www.mkdocs.org/).

In order to correctly maintain and update the documentation, you need to install and setup `MkDocs`.


## Prerequisites

1. Create a new Virtual Enviroment (venv) for this project

	```sh
	python3 -m venv .venv
	```

2. Activate the venv

	```sh
	. .venv/bin/activate
	```

3. Install the dependencies:

	```sh
	# IMPORTANT: venv must be active
	pip3 install -r requirements.txt
	```

Please refer to official [MkDocs documentation](https://www.mkdocs.org/user-guide/writing-your-docs/) to update and/or modify generated site settings/layout and to [MkDocs Material theme](https://squidfunk.github.io/mkdocs-material/) to customize theme.

## Build and test

[MkDocs](https://www.mkdocs.org/getting-started/#creating-a-new-project) comes with a built-in dev-server that lets you preview your documentation as you work on it.
Simply run `mkdocs serve`¹ from root folder and go [here](http://127.0.0.1:8000).

The dev-server also supports auto-reloading, and will rebuild your documentation whenever anything in the configuration file, documentation directory, or theme directory changes.

If you add new `*.md` files, you will need to execute `mkdocs build`¹ in order to generate new pages, check [here](https://squidfunk.github.io/mkdocs-material/) for more info.

### PDF Generation

To export the documentation in PDF, follow these steps:

1. Run `PDF_EXPORT=true mkdocs serve`

2. Open to the [unified docs url](http://127.0.0.1:8000/print_page/) in your browser.

3. Print the webpage in PDF (using your browser print feature, usually accessible with `Ctrl + P` / `Cmd + P`)

## Deploy

Once docs are updated and pushed to repository, you will need to deploy the new site with `mkdocs gh-deploy --force`¹ command.

Check your changes visiting https://sdk-docs.conio.com/

## Notes

¹ Be sure the [venv is activated](#prerequisites)

## Contacts

* Alessandro Farina - alessandro.farina@conio.com
* Beatrice Buran - beatrice.buran@conio.com
* Giovanni Di Donato - giovanni@conio.com