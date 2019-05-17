pypy-manylinux-demo
=====================
Demo project for building Python+PyPy wheels for Linux with Travis-CI

[![Build Status](https://travis-ci.org/pypy/pypy-manylinux-demo.svg?branch=master)](https://travis-ci.org/pypy/pypy-manylinux-demo)

This is a fork of the official
[python-manylinux-demo](https://github.com/pypa/python-manylinux-demo)
project. Building PyPy wheels is as easy as changing the docker image to use, as shown by this [commit](https://github.com/pypy/pypy-manylinux-demo/commit/c4cc5570f32fff90e60ed4701ef6b755ef3922fc).

```diff
diff --git a/.travis.yml b/.travis.yml
index 51e4a73..990950e 100644
--- a/.travis.yml
+++ b/.travis.yml
@@ -17,7 +17,7 @@ matrix:
     - sudo: required
       services:
         - docker
-      env: DOCKER_IMAGE=quay.io/pypa/manylinux2010_x86_64
+      env: DOCKER_IMAGE=pypywheels/manylinux2010-pypy_x86_64
            PLAT=manylinux2010_x86_64
```

This works because the default script builds a wheel for every python
installation found in `/opt/python`, which now includes also PyPy.

If your build system is more elaborate or you want to build wheels for only
selected versions of CPython/PyPy, you probably need to tweak your scripts and
build wheels using e.g. `/opt/python/pp271-pypy_41/bin/python`.
