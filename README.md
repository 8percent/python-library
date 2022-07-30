# Python Library

![Build & Test](https://github.com/8percent/python-library/actions/workflows/build_and_test.yml/badge.svg)
![Lint](https://github.com/8percent/python-library/actions/workflows/lint.yml/badge.svg)
[![codecov](https://codecov.io/gh/8percent/python-library/branch/master/graph/badge.svg?token=J7S8RQ32Y0)](https://codecov.io/gh/8percent/python-library)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)


This repository is a [template repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) providing boilerplate for Python library.

Developer can start writing code without wasting so much time to set up basic stuffs like CI, lint, etc.

## Table of Content

---

## Usage
We recommand to use GitHub's `Use this template` button to kick off this template.
But yet, you can set up copy this template by cloning or downloading this repository.

Once you prepared this repository on your local machine, remaining part is project configuration.
Unless you are familiar with stacks(poetry, tox, GitHub action, etc.) used in this template.
Subsequent Installation step might be helpful.

## Installation

### Install Poetry
Please read [this installation guide](https://github.com/pyenv/pyenv#installation) to install poetry.

After install poetry, install package dependencies with this command on project root.
This will resolve package dependencies and install it in poetry managed virtual environment.
```
$ poetry install
```

### Configuration

#### pyproject.toml
This file contains build system requirements and information, which are used by poetry to build the package.
We tried to gather every package related settings as much as possible here.
Through this design decision, project can keep configuration files as little as possible.

- [tool.poetry]: Describe package's metadata. Including package name, versions, dscription, authors etc.
- [tool.poetry.dependencies], [tool.poetry.dev-dependencies]: Manage package's dependencies. Poetry will check this section to resolve requirements version.
- [build-system]: Define how to build package. Generally no need to edit this section.
- [tool.isort], [tool.black]: By Editing this part, you can set how linting library should work.
- [tool.pytest.ini_options]: pytest configuration.

We suggest edit every setting above to represent your project better except [build-system].

#### .github/workflows/ci.yml
We choose GitHub action as Continuous Integration tool. It consists package-build, unittest, and lint.
Each jobs works concurrently at different virtual machines.

- package-build: Utilizes tox to test package against multiple python versions.
- unittest: Tests code and report coverage using pytest and codecov.
- lint: Lint codes using flake, isort, black.

Change `python-version` value in this file according to package compatible python versions. Versions should be same as pyproject.toml.

We suggest to use codecov to maintain your packages test coverage. For private repository, `CODECOV_TOKEN` should be set in GitHub repository secret.

#### tox.ini
Tox supports running tests against the package built in isolated virtual environment.

- [tox]: Tox global settings.
- [gh-actions]: Mapping between GitHub action python-version matrix and tox virtual environment.
- [testenv]: Test environment setting.

According to package's python compatible versions. You should define [tox.envlist] and [gh-actions].
Once envlist is defined, Proper python mapping should be designated [gh-actions].

#### Source code
Make your own named package in src directory.

NOTE: package setting in pyproject.toml should be changed as you create your own package.
```
packages = [
    { include = "{your-python-package-name}", from = "src" },
]
```

#### Test Code
Every test code should reside in 'tests' package at root directory.
Default package build strategy doesn't contain test code in distribution.

Test your code in local machine. you can just simply use 'pytest' or 'tox'.
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
This template repository follows src layout style. As the name suggests, its distinctive feature is it has src directory.
Main python packages lives inside src directory (not python package).

To tests python package strictly. Test should be tested against build package. not from source code itself.
Src layout helps to achieve this condition. By separating source code from project root, It prevents source code from accessed while testing.

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
package-build job is responsible for build package and test it. so it uses tox and can have multiple python versions.
unittest job is in charge of test on source code, and report test coverage.
lint job processes every linting stuffs.

`release_drafter.yml` workflow is working on master push event. which means master branch has changed.
It tracks all the merged pull requests and generate release draft containing chagelogs and contributors.
Release draft template can be modified by editing `.github/release-drafter.yml` file.
It demonstrates how draft should be presented.

### Testing
[Pytest](https://github.com/pytest-dev/pytest/) is our main test runner.

### Linting
Code lint is double-checked while development process. One at commit time, and the other at CI process.

[pre-commit](https://pre-commit.com/) is help us to check at commit time. By executing installation command `pre-commit install`
It automatically adds pre commit hooks. Types of hook that are running can be found in `.pre-commit-config.yaml`.

### Coverage
Coverage of test functions is one of important metrics deciding code quality.
GitHub actions `ci.yml` workflow's unittest job is control coverage report.

We suggest to install Codecov GitHub App which can manage coverage of repository.

---

## Contributing
- guideline

### Release
- release drafter

### Versioning
- 템플릿은 지속적으로 발전할 수 있다.
- Semantic Versining 을 활용한다.
- 프로젝트 구조가 변경되는 경우 major 버전을 변경해야하며, 일부 기능의 수정 변경은 minor, 이외 작은 코드의 개선은 patch 로 한다.
