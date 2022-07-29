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
- Remove repeated, boring tasks

## Usage
- GitHub `Use this template` button
- Clone this repository

- 사용법에 대한 설명

## Architecture

### Project Layout
- This template repository follows src layout style
- Main package is reside in src directory
- Tests are separated from main package. All test related modules should be in 'tests' python package located at project root

#### Reference
- https://blog.ionelmc.ro/2014/05/25/python-packaging/#the-structure
- https://doc.pytest.org/en/latest/explanation/goodpractices.html#tests-outside-application-code

### Linting
- GitHub workflow
- pre-commit
  - flake8, isort, black

### Testing
- ci
  - tox: 패키지 빌드한것에 대한 테스트 수행
    - 3.9, 3.10 등 여러개의 matrix 를 지정
  - lint: 코드 린트
  - test: 저장소 코드의 테스트 및 커버리지

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
