# Forecast implementation monorepo

This repository contains source code for different applications. It is split into 
modules to maximize code reuse and uses [Bazel](https://github.com/bazelbuild/bazelisk) as a build system to improve developer 
ergonomics.

## Repository contents
* **[apps](apps)**: contains applications that are normally executable with `bazel run`.
* **[forecast_model](forecast_model)**: Code of the Forecast Model project. Contains the layers, API, Repos and Services
* **[third_party](third_party)**: Locked third party python dependencies referenced in packages. These are managed
  with [poetry][poetry]

## Running the code on your machine
* Install [Bazelisk](https://github.com/bazelbuild/bazelisk) for your platform. 
* Run the targets:

```console
# Run the fast_api locally (should start a service on 0.0.0.0:8080)
$ bazel run //apps/api

# Run the starlette_api locally in debug mode (debugpy will wait for a debugger client to connect)
$ bazel run //apps/api --define DEBUG=1

# Clean everything
$ bazel clean --expunge
```

## FAQ
### Do I need to install docker, python, pyenv create a virtualenv ?
No. Bazel takes care of installing the right python toolchain version and create a sandbox for your code. Docker images can be built without requiring docker on the system.

### How do I configure LSP / DSP or other IDE tools ?
Bazel runs in a sandbox, however we are using [poetry][poetry] to manage dependencies. These dependencies are located in the
`third_party/` folder. As long as you set your IDE python interpreter to be the poetry env python, things should function normally in your IDE.

Here is one way to do this:
```console
$ cd third_party

# Get the python executable form the virtual env used by poetry, this is the python interpreter to use
$ poetry env info --executable

# An easy way to get the IDE to use the right environment is getting the poetry shell, which will set the right python
# interpreter and then cd to the project root and fire up your editor
$ cd third_party
$ poetry shell
$ cd ..
$ code
```

### Required Dependencies
Make sure you have the following installed on your machine
 - [Bazelisk](https://github.com/bazelbuild/bazelisk)
 - poetry
 - pyenv

## Setup Development Environment
#### Create the environment
Using terminal navigate to: `third_party` folder

```console
pyenv install 3.9.16
pyenv local 3.9.16
poetry config virtualenvs.in-project true
poetry install
poetry shell
```
