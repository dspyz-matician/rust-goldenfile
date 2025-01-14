# 👑 Rust Goldenfile

[![Documentation](https://docs.rs/goldenfile/badge.svg)](https://docs.rs/goldenfile) [![Latest Version](https://img.shields.io/crates/v/goldenfile.svg)](https://crates.io/crates/goldenfile) [![Build Status](https://app.travis-ci.com/calder/rust-goldenfile.svg?branch=master)](https://app.travis-ci.com/calder/rust-goldenfile) [![Coverage Status](https://coveralls.io/repos/github/calder/rust-goldenfile/badge.svg?branch=master)](https://coveralls.io/github/calder/rust-goldenfile?branch=master)

**Simple goldenfile testing in Rust.**

[Goldenfile](https://softwareengineering.stackexchange.com/questions/358786/what-is-golden-files) tests generate one or more output files as they run. At the end of the test, the generated files are compared to checked-in "golden" files produced by previous runs. This ensures that all changes to goldenfiles are intentional, explicit, and version controlled.

You can use goldenfiles to test the output of a parser, the order of a graph traversal, the result of a simulation, or anything else that shouldn't change without a human's approval.

## Usage

```rust
extern crate goldenfile;

use std::io::Write;

use goldenfile::Mint;

#[test]
fn test() {
    let mut mint = Mint::new("tests/goldenfiles");
    let mut file1 = mint.new_goldenfile("file1.txt").unwrap();
    let mut file2 = mint.new_goldenfile("file2.txt").unwrap();

    write!(file1, "Hello world!").unwrap();
    write!(file2, "Foo bar!").unwrap();
}
```

When the `Mint` goes out of scope, it will compare the contents of each file to its checked-in "golden" version and fail the test if they differ. To update the check-in versions, run:
```sh
REGENERATE_GOLDENFILES=1 cargo test
```

## Contributing

Pull requests are welcome! Run `dev/install-git-hooks` to install pre-commit test and formatting hooks.

This project follows the Rust community's [Code of Conduct](https://www.rust-lang.org/policies/code-of-conduct).
