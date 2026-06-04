# cofidectl SDK

[![Buf CI](https://github.com/cofide/cofidectl-sdk/workflows/buf-ci/badge.svg)](https://github.com/cofide/cofidectl-sdk/actions?query=workflow%3Abuf-ci+branch%3Amain)

This repository contains the protobuf message type definitions and generated Go stubs for [`cofidectl`](https://github.com/cofide/cofidectl).

For more information about the Cofide Connect Workload Identity platform, take a look at our [blog post](https://www.cofide.io/resources/introducing-cofide-connect-the-control-plane-for-workload-identity-and-access-management-iam) or [public documentation](https://docs.cofide.dev). If you'd like to discuss how enterprise workload identity management could benefit you then [let us know](https://www.cofide.io/contact).

## Prerequisites

This repository uses the [Buf CLI](https://buf.build/docs/ecosystem/cli-overview) to generate Go stubs from protobuf definitions.
The following tools must be available in order to generate code stubs.

- [Go 1.25.11 toolchain](https://golang.org/doc/install)
- [protoc-gen-go](https://pkg.go.dev/google.golang.org/protobuf/cmd/protoc-gen-go): `go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.36.5`
- [Buf CLI](https://buf.build/docs/installation)
- [Just](https://github.com/casey/just)

## Getting started

For convenience, a set of useful commands have been added to the *Justfile* in the project root.
Some of the key commands include:

- `just fmt` - Formats the protobuf definitions
- `just lint` - Lints the protobuf definitions and Go source code
- `just proto-gen` - Generates Go stubs from the protobuf definitions
- `just proto-docs [out=<dir>]` - Generates Markdown API documentation (defaults to `./docs/`); requires `protoc-gen-doc` (`go install github.com/pseudomuto/protoc-gen-doc/cmd/protoc-gen-doc@latest`)

The `.proto` files are in the `proto/` directory. Generated Go stubs are in `gen/go/`.

## Stability

The message definitions in this repository are not currently guaranteed to be backward compatible over time, and have been versioned as `v1alpha1`/`v1alpha2` to indicate this.
