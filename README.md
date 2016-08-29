[![POGODEV](https://github.com/pogodevorg/assets/blob/master/public/img/logo-github.png?raw=true)](https://pogodev.org)

# POGOProtos
[![Build Status](https://travis-ci.org/pogodevorg/POGOProtos.svg?branch=pogodev-develop)](https://travis-ci.org/pogodevorg/POGOProtos) [![Code Climate](https://codeclimate.com/github/pogodevorg/POGOProtos/badges/gpa.svg)](https://codeclimate.com/github/pogodevorg/POGOProtos) [![Issue Count](https://codeclimate.com/github/pogodevorg/POGOProtos/badges/issue_count.svg)](https://codeclimate.com/github/pogodevorg/POGOProtos) [![license](https://img.shields.io/github/license/pogodevorg/POGOProtos.svg?maxAge=2592000?style=flat-square)](https://github.com/pogodevorg/POGOProtos/blob/master/LICENSE.md)

## Table of Contents
* [What is it?](#what-is-it)
* [Installation](#installation)
  * [Requirements](#requirements)
  * [Instructions](#instructions)
    * [Cavets](#cavets)
* [Documentation](#documentation)
  * [Compilation](#compilation)
    * [Pretty Compilation (Recommended)](#pretty-compilation-recommended)
    * [Single File Compilation](#single-file-compilation)
    * [Recursive compilation](#recursive-compilation)
  * [Pre-compiled POGOProtos](#pre-compiled-pogoprotos)
* [Contributing](#contributing)
  * [Core Maintainers](#core-maintainers)
* [Licensing](#licensing)
  * [Third Party Licenses](#third-party-licenses)
* [Credits](#credits)

## What is it?
`POGOProtos` is a PogoDev maintained fork of [Aeon's POGOProtos](https://github.com/AeonLucid/POGOProtos).
This repository contains [ProtoBuf](https://github.com/google/protobuf) `.proto` files that are needed to decode the PokémonGO RPC.
If you want to know which messages are implemented right now, [click here](https://github.com/pogodevorg/POGOProtos/blob/master/src/POGOProtos/Networking/Requests/RequestType.proto).

## Installation

### Requirements
- [Protocol Buffers (>= v3.0.0-beta-4)](https://github.com/google/protobuf/releases)
- Python (> 2.7)

### Instructions
Firstly clone the current repository.

    git clone https://github.com/pogodevorg/POGOProtos

Then. please ensure that you have the required protocol buffers and python installed,
below are known cavets that need to be adhered to, depending on your operating system.

#### Cavets
| Operating System | Source                                                                        |
|------------------|-------------------------------------------------------------------------------|
| Windows          | Be sure to add `protoc` to your environmental path.                           |
| *nix             | Ensure that you have the newest version of `protoc` installed.                |
| OSX              | Use `homebrew` to install `protobuf ` with `brew install --devel protobuf`.   |

## Documentation
### Compilation
There are three ways to compile **POGOProtos**:

* Pretty Compilation (Recommended)
* Single File Compilation
* Recursive Compilation

#### Pretty Compilation (Recommended)
Pretty compilation creates an output specifically for the target language, i.e. respecting naming contentions, etc.
This is an example of how the generated code will be organized:

`python compile_pretty.py cpp`:
 - `POGOProtos/Data/PlayerData.proto` -> `POGOProtos/Data/PlayerData.pb.cpp`

`python compile_pretty.py csharp`:
 - `POGOProtos/Data/PlayerData.proto` -> `POGOProtos/Data/PlayerData.g.cs`

`python compile_pretty.py go`:
 - `POGOProtos/Data/*.proto` -> `github.com/aeonlucid/pogoprotos/data`
 - `POGOProtos/Data/PlayerData.proto` -> `github.com/aeonlucid/pogoprotos/data/player_data.pb.go`

`python compile_pretty.py java`:
 - `POGOProtos/Data/*.proto` -> `com/github/aeonlucid/pogoprotos/Data.java`

`python compile_pretty.py js`:
 - `POGOProtos/**/*.proto` -> `pogoprotos.js`

`python compile_pretty.py objc`:
 - `POGOProtos/Data/PlayerData.proto` -> `POGOProtos/Data/PlayerData.pbobjc.m`

`python compile_pretty.py python`:
 - `POGOProtos/Data/*.proto` -> `pogoprotos/data/__init__.py`
 - `POGOProtos/Data/PlayerData.proto` -> `pogoprotos/data/player_data_pb2.py`

`python compile_pretty.py ruby`:
 - `POGOProtos/Data/*.proto` -> `pogoprotos/data.rb`
 - `POGOProtos/Data/PlayerData.proto` -> `pogoprotos/data/player_data.rb`

More information can be found via running `python compile_pretty.py --help` for help.

#### Single File Compilation
Single file compilation merges every directory to it's own `.proto` file.

As an example:
 - Networking/Requests/Messages/\*.proto
 - Networking/Responses/\*.proto

Becomes:
 - POGOProtos.**Networking.Requests.Messages.proto**
 - POGOProtos.**Networking.Responses.proto**

These new files are then compiled by `protoc` and placed in the output directory, which greatly reduces the amount of output files.
Single file complication can achieved by running `python compile_single.py` to compile everything to a single file.

*Flags*
 - Add the `-l` or `--language` flag to compile to whatever language you need, the default is C#.
 - Add the `-o` or `--output` flag to set an output directory, the default is `out`.
 - Add the `-d` or `--desc_file` flag to only generate a descriptor file, `POGOProtos.desc` will be written to the specified output directory.

*Go Specific Flags*
 - Add the `--go_import_prefix` to prefix all imports in output go files for vendoring all dependencies
 - Add the `--go_package` to specify the name of the exported go package

#### Recursive compilation
Recursive compilation loops through all directories and compiles every `.proto` file it finds to the specified output directory.
Run `python compile.py` to recursively compile everything.

*Flags*
 - Add the `-l` or `--language` flag to compile to whatever language you need, the default is C#.
 - Add the `-o` or `--output` flag to set an output directory, the default is `out`.

### Pre-compiled POGOProtos
If you don't want to compile **POGOProtos** but instead use it directly, check out the following repositories.

| Language         | Source                                                  |
|------------------|---------------------------------------------------------|
| .NET             | https://github.com/johnduhart/POGOProtos-dotnet         |
| Go               | https://github.com/pogodevorg/POGOProtos-go             |
| Haskell          | https://github.com/relrod/pokemon-go-protobuf-types     |
| NodeJS           | https://github.com/rastapasta/node-pokemongo-protobuf   |
| NodeJS (pure JS) | https://github.com/cyraxx/node-pogo-protos              |
| PHP              | https://github.com/jaspervdm/pogoprotos-php             |
| Rust             | https://github.com/rockneurotiko/pokemon-go-protobuf-rs |

## Licensing
[GNU GPL](https://github.com/pogodevorg/POGOProtos/blob/master/LICENSE) v3 or later.

### Third Party Licenses
    None

## Contributing
Currently, you can contribute to this project by:
* Submitting a detailed [issue](https://github.com/pogodevorg/POGOProtos/issues/new).
* [Forking the project](https://github.com/pogodevorg/POGOProtos/fork), and sending a pull request back to for review.

### Core Maintainers

* [![keyphact](https://github.com/keyphact.png?size=36) - keyphact](https://github.com/keyphact)

## Credits
* [![AeonLucid](https://github.com/AeonLucid.png?size=36) AeonLucid](https://github.com/AeonLucid) - for creating and maintaing the upstream POGOProtos repository.
