# Shackbus Interface Control Document

This repository contains the official message definitions for all Shackbus
messages. The messages are defined in the
[Protocol Buffers version 3)](https://developers.google.com/protocol-buffers/docs/proto3)
Interface Definition Language (IDL).

[Protocol Buffer](https://developers.google.com/protocol-buffers) provides a
variety of code generators which will create the code stubs in your favorite
language. Currently Protocol Buffers supports:

- C++
- C#
- Go
- Java
- Python
- PHP
- Ruby
- Objective C
- Javascript

There are many third party plugins available for other programming languages.

For pure ANSI C code generation check out:

- [nanopb](https://koti.kapsi.fi/jpa/nanopb/) for embedded devices
- [protobuf-c](https://github.com/protobuf-c/protobuf-c)

## License

This library is published under the the permissive
[MIT license](http://choosealicense.com/licenses/mit/). Allowing private and
commercial usage. You can find a good comparison of Open Source Software
licenses, including the MIT license at
[choosealicense.com](http://choosealicense.com/licenses/)


## How to use this repository

Typically, you would include this repository as a git submodule in your project.

``` bash
    $ git submodule add https://github.com/shackbus/icd.git
```

## How to generate code

It is always a good idea to seperate generated code from the source files.
Assuming you have included this repository as a git submodule, you would
probably have a directory structure similar to this one:

``` bash
    your_project -
                 | - icd //this repository
                 | - icd_gen //where the generated files will be located
                 | - build
                 | - src
                 | - include
                 | - ...
```

Make sure you are in the root directory of your project. The protocol buffers
code generator. The example below will generate C++ bindings for all Shackbus
messages.

``` bash
    $ protoc --proto_path=./icd --cpp_out=./icd_gen ./icd/*.proto
```

In this case, the protoc generated in the **./icd_gen** directory, two files
for each proto file. For example for error.proto:

``` bash
    error.pb.h // headers
    error.pb.c // code implementation
```

You can now include the generated files in your code. In C++ for example:

``` cpp
    #include "error.pb.h"
```

The amount of output files and the import depends of course on the specific
language you are using. For more information about the specifics of your
programming language, check the official
[protocol buffers](https://developers.google.com/protocol-buffers)
documentation.