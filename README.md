# Make

This repo is intended to be used for importing and reusing Makefiles in other repositories.
For referencing this repo in other git repositories, you can use git submodules.

## Quick Start

In your git repository, add this repo as a git submodule:

```
git submodule init
git submodule add -b main https://github.com:gardenbed/make.git
```

Then, in the root directory of your repo:

  1. Create a `Makefile`.
  1. Set required variables.
  1. Import `*.mk` files from `make` sub-directory.

```Makefile
include make/common.mk
include make/go.mk
include make/grpc.mk
include make/docker.mk
include make/terraform.mk

name := my-service                   # Required by go.mk
main_pkg := .                        # Required by go.mk
proto_path := idl                    # Required by grpc.mk
go_out_path := internal/idl          # Required by grpc.mk
docker_image := dockerid/my-service  # Required by docker.mk
docker_tag := $(version)             # Required by docker.mk
```

For upgrading the make submodule, run:

```
git submodule update --remote
```

## Documentation

| File | Required Variables | Macros | Rules |
|------|--------------------|--------|-------|
| `common.mk` | | `echo_red` <br/> `echo_green` <br/> `echo_yellow` <br/> `echo_blue` <br/> `echo_purple` <br/> `echo_cyan` | |
| `go.mk` | `name` <br/> `main_pkg` | | `test` <br/> `test-short` <br/> `test-coverage` <br/> `clean-test` <br/> `run` <br/> `build` <br/> `build-all` <br/> `clean-build` |
| `grpc.mk` | `proto_path` <br/> `go_out_path` | | `protoc` <br/> `protoc-gen-go` <br/> `protobuf` |
| `docker.mk` | `docker_image` <br/> `docker_tag` | | `docker` <br/> `docker-test` <br/> `push` <br/> `push-latest` <br/> `save-docker` <br/> `load-docker` <br/> `clean-docker` |
| `terraform.mk` | | `create_aws_key` <br/> `create_gcp_key` | `validate` <br/> `plan` <br/> `apply` <br/> `refresh` <br/> `destroy` <br/> `clean-terraform` |
