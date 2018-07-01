[![Build Status](https://travis-ci.org/deadsnakes/travis-ci-python3.7-example.svg?branch=master)](https://travis-ci.org/deadsnakes/travis-ci-python3.7-example)

travis-ci-python3.7-example
===========================

_2018-07-01_: nearly all travis-ci VMs run Ubuntu trusty which ships with
openssl 1.0.1.  python3.7 [dropped][python3.7-pr] support for end-of-lifed
openssl versions.

travis-ci has a `xenial` distribution which can be enabled with `dist: xenial`
+ `sudo: required`.  The `python: 3.7-dev` virtualenv provided by travis-ci for
xenial is still 3.7a4 which is quite a bit different from 3.7.0 final.

deadsnakes provides a backport of python3.7 for ubuntu xenial which can be
enabled using the [travis-ci apt addon][travis-ci-apt-addon].  Unfortunately,
at the time of writing it appears that the shortcut `deadsnakes` does not work
with `dist: xenial` [travis-ci/travis-ci#9827][travis-ci-issue].  However, the
full source line works :tada:.

This repository contains a sample `.travis.yml` which installs python3.7 from
deadsnakes and invokes `tox`.

The tl;dr magic to enable this:

```yaml
sudo: required
dist: xenial
addons:
  apt:
    sources:
    - sourceline: 'deb http://ppa.launchpad.net/deadsnakes/ppa/ubuntu xenial main'
    packages:
    - python3.7-dev
```

It is suggested to use the [travis-ci matrix][travis-ci-matrix] feature to
only install `python3.7` once as both `sudo: required` and the `apt` add on
add a significant amount of time to the build.  The example `.travis.yml` does
this.

[python3.7-pr]: https://github.com/python/cpython/pull/3462
[travis-ci-apt-addon]: https://docs.travis-ci.com/user/installing-dependencies#Installing-Packages-with-the-APT-Addon
[travis-ci-issue]: https://github.com/travis-ci/travis-ci/issues/9827
[travis-ci-matrix]: https://docs.travis-ci.com/user/customizing-the-build#Explicitly-Including-Jobs
