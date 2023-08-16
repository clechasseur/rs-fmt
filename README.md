# `rs-fmt-check` Action

[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![CI](https://github.com/clechasseur/rs-fmt-check/actions/workflows/ci.yml/badge.svg?branch=main&event=push)](https://github.com/clechasseur/rs-fmt-check/actions/workflows/ci.yml)

> Rustfmt suggestions in your Pull Requests

This GitHub Action executes [`rustfmt`](https://github.com/rust-lang/rustfmt)
and posts all suggestions as annotations for the pushed commit.

![Screenshot of a rustfmt suggestion displayed in the commit interface of GitHub](./.github/screenshot_fmt.png)

## Example workflow

Note: this workflow uses [`dtolnay/rust-toolchain`](https://github.com/dtolnay/rust-toolchain) to install the most recent `nightly` rustfmt <sup>1</sup>.

```yaml
name: Rustfmt check

on: push

jobs:
  rustfmt_check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: dtolnay/rust-toolchain@nightly
        with:
          components: rustfmt
      - uses: clechasseur/rs-fmt-check@v1
```

## Inputs

All inputs are optional.

| Name | Description | Type | Default |
| --- | --- | --- | --- |
| `toolchain` | Rust toolchain to use <sup>1</sup> | string | `nightly` |
| `args` | Arguments for the `cargo fmt` command | string |         |
| `working-directory` | Directory where to perform the `cargo fmt` command | string |         |

For extra details about the `toolchain` and `args` inputs, see [`rs-cargo` Action](https://github.com/clechasseur/rs-cargo#inputs).

<sup>1</sup> : This action currently relies on an unstable `rustfmt` feature (`emit json`) and as such, requires a `nightly` toolchain at the minimum. You should not change the value of the `toolchain` parameter unless you know the specified toolchain supports the feature correctly.
