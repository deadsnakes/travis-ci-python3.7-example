[![Build Status](https://travis-ci.org/deadsnakes/travis-ci-python3.7-example.svg?branch=master)](https://travis-ci.org/deadsnakes/travis-ci-python3.7-example)

travis-ci-python3.7-example
===========================

_2018-07-01_: nearly all travis-ci VMs run Ubuntu trusty which ships with
openssl 1.0.1.  python3.7 [dropped][python3.7-pr] support for end-of-lifed
openssl versions.

travis-ci has a `xenial` distribution which can be enabled with `dist: xenial`.
The `python: 3.7-dev` virtualenv provided by travis-ci for trusty is still
3.7a4 which is quite a bit different from 3.7.0 final.

deadsnakes provides a backport of python3.7 for ubuntu xenial which can be
enabled using the [travis-ci apt addon][travis-ci-apt-addon].

This repository contains a sample `.travis.yml` which installs python3.7 from
deadsnakes and invokes `tox`.

The tl;dr magic to enable this:

```yaml
dist: xenial
addons:
  apt:
    sources:
    - deadsnakes
    packages:
    - python3.7-dev
```

It is suggested to use the [travis-ci matrix][travis-ci-matrix] feature to
only install `python3.7` once as the `apt` add on adds a significant amount of
time to the build.  The example `.travis.yml` does this.

### update (2018-07-03)

travis-ci has enabled `python: 3.7` on `dist: xenial` so deadsnakes is no
longer necessary:

```yaml
    - env: TOXENV=py37
      python: 3.7
      dist: xenial
```

_update 2018-10-15_: `sudo: required` is no longer necessary


[python3.7-pr]: https://github.com/python/cpython/pull/3462
[travis-ci-apt-addon]: https://docs.travis-ci.com/user/installing-dependencies#Installing-Packages-with-the-APT-Addon
[travis-ci-matrix]: https://docs.travis-ci.com/user/customizing-the-build#Explicitly-Including-Jobs
