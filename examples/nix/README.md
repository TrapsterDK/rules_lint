# Nix Formatting Example

This example uses [nixfmt](https://github.com/NixOS/nixfmt) to format Nix files with `rules_lint`.

## Setup

- `MODULE.bazel` installs nixfmt with `rules_multitool`.
- `tools/nixfmt.lock.json` pins nixfmt 1.4.0 for Linux x86_64.
- `tools/format/BUILD` sets the `nix` attribute on `format_multirun`.

## Usage

From this directory:

```sh
bazel run //tools/format
bazel run //tools/format:format.check
bats test
```

The formatter discovers `*.nix` files. Check mode uses nixfmt's `--check` flag and leaves source files unchanged.

The pinned release only provides a Linux x86_64 binary. Other platforms need a compatible nixfmt binary and a matching URL, SHA-256, OS, and CPU entry in the lockfile, or a different binary target supplied through the `nix` attribute.
