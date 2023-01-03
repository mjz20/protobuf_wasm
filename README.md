How to build
------------

bazel build proto-wasm --copt="-Wno-deprecated-builtins" --copt="-Wno-array-parameter" --copt="-Wno-deprecated-non-prototype" --copt="-pthread" --linkopt="-pthread" --sandbox_debug --verbose_failures

Note: due to emscripten toolchain enabled -Werror -Wall:
https://github.com/emscripten-core/emsdk/blob/main/bazel/emscripten_toolchain/toolchain.bzl#L433

so you will get following error:

'''
external/com_google_absl/absl/hash/internal/low_level_hash.cc:43:38: error: argument 'salt' of type 'const uint64_t[]' (aka 'const unsigned long long[]') with mismatched bound [-Werror,-Warray-parameter]
'''

you will need to disable the feature: wasm_warnings_as_errors by go to the sandbox folder and modify it. the path is like: /home/mj/.cache/bazel/_bazel_mj/9d77888f7e298040819668f1b7f626a8/external/emsdk/emscripten_toolchain/toolchain.bzl


How to run?
-----------
node --experimental-wasm-threads --experimental-wasm-bulk-memory bazel-bin/proto-wasm/protoc.js

What is the change to make it build?


changes
-------
- WORKSPACE
- BUILD.bazel

the [commit](https://github.com/mjz20/protobuf_wasm/commit/aa3ac75474327a33d0af10e6b6799c0e3b4b4b56)



Protocol Buffers - Google's data interchange format
===================================================

Copyright 2008 Google Inc.

[Protocol Buffers documentation](https://developers.google.com/protocol-buffers/)

Overview
--------

Protocol Buffers (a.k.a., protobuf) are Google's language-neutral,
platform-neutral, extensible mechanism for serializing structured data. You
can find [protobuf's documentation on the Google Developers site](https://developers.google.com/protocol-buffers/).

This README file contains protobuf installation instructions. To install
protobuf, you need to install the protocol compiler (used to compile .proto
files) and the protobuf runtime for your chosen programming language.

Protocol Compiler Installation
------------------------------

The protocol compiler is written in C++. If you are using C++, please follow
the [C++ Installation Instructions](src/README.md) to install protoc along
with the C++ runtime.

For non-C++ users, the simplest way to install the protocol compiler is to
download a pre-built binary from our [GitHub release page](https://github.com/protocolbuffers/protobuf/releases).

In the downloads section of each release, you can find pre-built binaries in
zip packages: `protoc-$VERSION-$PLATFORM.zip`. It contains the protoc binary
as well as a set of standard `.proto` files distributed along with protobuf.

If you are looking for an old version that is not available in the release
page, check out the [Maven repository](https://repo1.maven.org/maven2/com/google/protobuf/protoc/).

These pre-built binaries are only provided for released versions. If you want
to use the github main version at HEAD, or you need to modify protobuf code,
or you are using C++, it's recommended to build your own protoc binary from
source.

If you would like to build protoc binary from source, see the [C++ Installation Instructions](src/README.md).

Protobuf Runtime Installation
-----------------------------

Protobuf supports several different programming languages. For each programming
language, you can find instructions in the corresponding source directory about
how to install protobuf runtime for that specific language:

| Language                             | Source                                                      |
|--------------------------------------|-------------------------------------------------------------|
| C++ (include C++ runtime and protoc) | [src](src)                                                  |
| Java                                 | [java](java)                                                |
| Python                               | [python](python)                                            |
| Objective-C                          | [objectivec](objectivec)                                    |
| C#                                   | [csharp](csharp)                                            |
| Ruby                                 | [ruby](ruby)                                                |
| Go                                   | [protocolbuffers/protobuf-go](https://github.com/protocolbuffers/protobuf-go)|
| PHP                                  | [php](php)                                                  |
| Dart                                 | [dart-lang/protobuf](https://github.com/dart-lang/protobuf) |
| Javascript                           | [protocolbuffers/protobuf-javascript](https://github.com/protocolbuffers/protobuf-javascript)|

Quick Start
-----------

The best way to learn how to use protobuf is to follow the [tutorials in our
developer guide](https://developers.google.com/protocol-buffers/docs/tutorials).

If you want to learn from code examples, take a look at the examples in the
[examples](examples) directory.

Documentation
-------------

The complete documentation is available via the [Protocol Buffers documentation](https://developers.google.com/protocol-buffers/).

Developer Community
-------------------

To be alerted to upcoming changes in Protocol Buffers and connect with protobuf developers and users,
[join the Google Group](https://groups.google.com/g/protobuf).

