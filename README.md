# Python Library

![Build & Test](https://github.com/8percent/python-library/actions/workflows/build_and_test.yml/badge.svg)
![Lint](https://github.com/8percent/python-library/actions/workflows/lint.yml/badge.svg)
[![codecov](https://codecov.io/gh/8percent/python-library/branch/master/graph/badge.svg?token=J7S8RQ32Y0)](https://codecov.io/gh/8percent/python-library)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)


This repository is a [template repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) for Python library which provides linting, testing, coverage reporting and packaging.

## Table of Content


## Goals
- Fast project setup
- Reduce repeated task
- Make developer to concentrate on writing library's core function

## Usage
### Github
- Press `Use this template` button. on top right repos code section

### Clone
- Clone this repository using following command
  - `git clone https://github.com/8percent/python-library.git`

## Architecture

### Project Layout
- We use src layout
- https://doc.pytest.org/en/latest/explanation/goodpractices.html#tests-outside-application-code

### Linting
- github workflow
- pre-commit
  - flake8, isort, black

### Testing
- tox
  - test-matrix
  - default 3.9, 3.10

- pytest
- poetry install ( 현재 프로젝트의 패키지 설치 - 현재 로컬의 프로젝트를 연결해줌)
- tox -e dev ( 패키지 만들고 테스트 )

### Coverage
- codecov

### Packaging
- poetry

## Contributing
- guideline

### Release
- release drafter

### Versioning
- 템플릿은 지속적으로 발전할 수 있다.
- Semantic Versining 을 활용한다.
- 프로젝트 구조가 변경되는 경우 major 버전을 변경해야하며, 일부 기능의 수정 변경은 minor, 이외 작은 코드의 개선은 patch 로 한다.



### TESTING

- poetry install 을 하면 로컬의 프로젝트 Path 가 지정됨
  - pytest 수행시 로컬 프로젝트 변경을 잘 반영함
  - tox 수행시 dist 에 현재 프로젝트 변경사항을 기반으로 패키징을 함

- 로컬 개발시
  - poetry install을 해두면 pytest 를 활용할 수 있다. ( CLI, IDE )
  - tox -e dev 를 통해 패키징한 결과를 테스트할 수 있다.

- CI
  - poetry install 을 통해 패키징 결과를 테스트 할 수 있다.
