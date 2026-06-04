# AGENTS.md

This file provides guidance to AI coding agents when working with code in this repository.

## Overview

This repository contains:
1. **Protocol Buffer definitions** (`proto/`) - message type definitions for cofidectl
2. **Generated code** (`gen/go/`) - auto-generated Go protobuf message stubs from the proto files

All APIs are versioned as `v1alpha1`/`v1alpha2` (backward compatibility not guaranteed).

## Commands

Commands use [Just](https://github.com/casey/just) as the task runner.

| Command | Purpose |
|---|---|
| `just fmt` | Format proto files (`buf format -w`) |
| `just lint` | Lint proto files and Go source |
| `just buf-lint` | Lint proto files only |
| `just go-lint` | Run golangci-lint only |
| `just proto-gen` | Regenerate Go stubs from proto files |
| `just proto-docs` | Generate Markdown API docs (to `docs/`, git-ignored) |

## Architecture

### Proto → Generated Code

The project follows a two-layer pattern:

1. **`proto/`** - Source of truth. Domain message types across 10 packages:
   - `ap_binding/v1alpha1`, `attestation_policy/v1alpha1`, `cluster/v1alpha1`, `config/v1alpha1`
   - `cofidectl/datasource_plugin/v1alpha2`, `cofidectl/provision_plugin/v1alpha2`
   - `federation/v1alpha1`, `plugins/v1alpha1`, `trust_provider/v1alpha1`, `trust_zone/v1alpha1`
   - Plus transitive dep: `spire/api/types/` (bundle + selector)

2. **`gen/go/`** - Auto-generated, do not edit manually. Regenerate with `just proto-gen`. Mirrors the `proto/` directory structure. Contains only `*.pb.go` message files (no service stubs).

### Key files

- `buf.gen.yaml` - Code generation config (protoc-gen-go only, messages only)
- `buf.yaml` - Buf linting rules (STANDARD minus FIELD_NOT_REQUIRED and PACKAGE_NO_IMPORT_CYCLE)

### Adding a new message type

1. Add proto definition under `proto/<domain>/`
2. Run `just proto-gen` to generate stubs in `gen/go/`

## Code Generation Prerequisites

Required tools for `just proto-gen`:
- `go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.36.5`
- [Buf CLI](https://buf.build/docs/installation)
