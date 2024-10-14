# `frequenz-floss/gh-action-cargo-test`

## Overview

This action runs quality checks and tests on your cargo crate. It runs the
following:

- format check using `cargo fmt`
- linting using `cargo clippy`
- tests using `cargo test`, or `cargo llvm-cov test` if coverage is enabled.

## Inputs

Note that the build-cache generated in previous runs of this action becomes
invalid if any input parameter is changed. In such cases, please delete the old
build cache `[OS]-cargo-build-test-[hash]` manually. It will be regenerated in
the next run.

### `enable-coverage: [true|false]`

Whether to enable generating a test coverage report or not. If yes, uses
`cargo-llvm-cov` for generating the report.


Default: `true`

### `enable-build-cache: [true|false]`

Whether to enable caching the build artifacts or not. If yes, caches the build
using a hash generated from the `Cargo.lock` file if it exists, otherwise uses
the `Cargo.toml` file.

Rust libraries may choose to set this to `false` if they are not using any
dependencies that take a long time to build. This ensures the latest versions of
the dependencies being fetched on each run.

Default: `true`

### `cargo-clippy-extra-parameters`

Additional parameters to pass to the `cargo clippy` call.

Default: `"-W clippy::unwrap_used -W clippy::expect_used -W clippy::panic"`

### `cargo-test-parameters: string`

Parameters to pass to the `cargo test` command.

Default: `""`

## Example

```yaml
jobs:
  test:
    runs-on: ubuntu-22.04

    steps:
      - name: Fetch sources
        uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Run tests
        uses: frequenz-floss/gh-action-cargo-test@v1
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file
for details.

