[![Build Status](https://travis-ci.org/StorjPlatform/StorjTelehash.svg?branch=master)](https://travis-ci.org/StorjPlatform/StorjTelehash)
[![Coverage Status](https://coveralls.io/repos/StorjPlatform/StorjTelehash/badge.svg?branch=master)](https://coveralls.io/r/StorjPlatform/StorjTelehash?branch=master)

# Messaging Layer on Storj Platform by Telehash

Explanation about messaging layer is [here](Messaging.md).

## Requirements
This requires 
* `g++` (v4.8 or higher for test)
* `python` (2.x or 3.x)

## Installation

To install 

    $ python setup.py install
    
To run the associated tests:

    $ make test
    $ LD_LIBRARY_PATH=libtap ./test

To run the associated tests for python:

    $ python  setup.py test -a "--doctest-modules --pep8 -v tests/"


for Windows OS, [Cygwin](https://www.cygwin.com/) must be installed first.

1. download cygwin installer from [here](https://www.cygwin.com/setup-x86.exe) and run it.
1. go forward to package selection, and select packages below, and go forward to install them.

under devel category:

1. gcc-g++
1. make
2. git

under Python category:

1. python
1. python3
1. python-setuptools
1. python3-setuptools

After that run c:\cygwin\cygwin.bat, where you can install and run StorjTelehash.

## Usage

API Document for messaging , which is concorete implementation of abstract messaging layer by telehash-c ,
is [here](https://rawgit.com/StorjPlatform/StorjTelehash/master/docs/html/messaging.html)

API Document for telehashbinder , which is classes/functions used by storjtelehash,
is [here](https://rawgit.com/StorjPlatform/StorjTelehash/master/docs/html/telehashbinder.html)

# Contribution
Improvements to the codebase and pull requests are encouraged.


