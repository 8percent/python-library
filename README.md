# Python Library

![Build](https://github.com/8percent/python-library/actions/workflows/ci.yml/badge.svg)
[![codecov](https://codecov.io/gh/8percent/python-library/branch/master/graph/badge.svg?token=J7S8RQ32Y0)](https://codecov.io/gh/8percent/python-library)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)


This repository is a [template repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) providing boilerplate for Python library.

Developer can start writing code without wasting so much time to set up basic stuffs like CI, lint, etc.

## Table of Content
- [Usage](#usage)
- [Installation](#installation)
  - [Install Poetry](#install-poetry)
  - [Configuration](#configuration)
- [Architecture](#architecture)
  - [Project Layout](#project-layout)
  - [Dependency Management & Packaging](#dependency-management--packaging)
  - [Continuous Integration](#continuous-integration)
  - [Testing](#testing)
  - [Linting](#linting)
  - [Coverage](#coverage)

---

## Usage
We recommand to use GitHub's `Use this template` button to kick off this template.
But yet, you can set up copy this template by cloning or downloading this repository.

Once you prepared this repository on your local machine, remaining part is project configuration.
Unless you are familiar with stacks(poetry, tox, GitHub action, etc.),
Subsequent Installation step might be helpful.

---

## Installation

### Install Poetry
Please read this [installation guide](https://python-poetry.org/docs/) to install poetry.

Then install package dependencies with this command at project root.
This will resolve package dependencies and install it in poetry managed virtual environment.
```
$ poetry install
```

### (Optional) Install Pyenv
> pyenv lets you easily switch between multiple versions of Python.
It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

As quoted [pyenv readme](https://github.com/pyenv/pyenv/blob/master/README.md) demonstrates, It provide us handy python version management.

### Configuration

#### pyproject.toml
This file contains build system requirements and information, which are used by poetry to build the package.
We tried to gather every package related settings as much as possible here.
Through this design decision, project could remove package dependant configuration files like `.isort.cfg`, `pytest.ini`, etc.

- **[tool.poetry]**: Describe package's metadata. Including package name, versions, dscription, authors etc.
- **[tool.poetry.dependencies]**, **[tool.poetry.dev-dependencies]**: Manage package's dependencies. Poetry will check this section to resolve requirements version.
- **[build-system]**: Define how to build package. Generally no need to edit this section.
- **[tool.isort]**, **[tool.black]**: By Editing this part, you can set how linting library should work.
- **[tool.pytest.ini_options]**: pytest configuration.

Except **[build-system]**, We suggest you to update every settings above.

#### .github/workflows/ci.yml
We choose GitHub action as Continuous Integration tool. It contains package-build, unittest, and lint job.
Each job works concurrently on different virtual machines.

- **package-build**: Use tox to test package against multiple python versions.
- **unittest**: Test code and report coverage using pytest and codecov.
- **lint**: Lint code using flake, isort, black.

Change `python-version` value in this file according to package compatible python versions which configured at `pyproject.toml`.

#### tox.ini
Tox runs test against packages which built in isolated virtual environment.

- **[tox]**: Tox global settings.
- **[gh-actions]**: Mapping between GitHub action python-version matrix and tox virtual environment.
- **[testenv]**: Test environment setting.

According to package's python compatible versions, **[tox.envlist]** and **[gh-actions]** should be defined.

#### Source code
Make your own named package in src directory.

**NOTE**: package setting in `pyproject.toml` should be changed as you set up your own package.
```
packages = [
    { include = "{your-python-package-name}", from = "src" },
]
```

#### Test Code
Every test code should resides in `tests` package at project root.

To test your source code, simply use 'pytest' or 'tox'.
```
# Use pytest
$ pytest tests/

# Use Tox
$ tox
```

---

## Architecture
Detailed explanation about stacks used in this template is covered in this section.

### Project Layout
This template repository follows src layout style. As the name suggests, its distinctive feature is subdirectory named `src`.
Main python packages lives inside `src` directory.

To tests python built package. Testing should be done against built package. not from the source code itself.
Src layout helps to achieve this condition. By separating source code from project root, It prevents test code to import source code.

This layout is better explained in this [blog post by Ionel Cristian Mărieș](https://blog.ionelmc.ro/2014/05/25/python-packaging/#the-structure).

### Dependency Management & Packaging
We use [Poetry](https://github.com/python-poetry/poetry) to control dependencies and build package.
Advantages of using poetry is well explained in their [README.md](https://github.com/python-poetry/poetry/blob/master/README.md).

By default, Poetry automatically manages virtual environment for each project and python version.
It frees developer from virtual environment management. But also offers option to manage virtual environment manually.
For more information read this [docs](https://python-poetry.org/docs/managing-environments/)

### Continuous Integration
Our GitHub action consists of two workflows. one for CI, and one for release draft.

`ci.yml` workflow contains three different jobs. Those are package-build, unittest, lint.
- **package-build** job is responsible for build package and test it. so it uses tox and can have multiple python versions.
- **unittest** job is in charge of test on source code, and report test coverage.
- **lint** job processes every linting stuffs.

`release_drafter.yml` workflow is activated whenever master branch changed.
It tracks merged pull requests and generate release draft containing chagelog and contributors.
Release draft template can be modified by editing `.github/release-drafter.yml` file.
It demonstrates how draft should be presented.

### Testing
[Pytest](https://github.com/pytest-dev/pytest/) is our main test runner.

### Linting
Code is double-checked during development process. One at commit phase, and the other at CI process.

[pre-commit](https://pre-commit.com/) is help us to check at commit time. By executing installation command `pre-commit install`,
It automatically adds pre commit hooks. Types of hook are managed using `.pre-commit-config.yaml`.

### Coverage
Coverage of test functions is one of important metrics which decides code quality.
GitHub actions `ci.yml` workflow's unittest job is control coverage report.

We suggest to install Codecov GitHub App which can manage coverage of repository.

---

## Contributing
Pull requests are always welcome.

Check CONTRIBUTING.md for more details.

---

## License
Distributed under the terms of the MIT license.
