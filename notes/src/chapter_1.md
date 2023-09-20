# Chapter 1 - Getting Started

## Tools

This chapter goes over installing the Rust toolchain (Rustup), as well as goes over how to intialize a project using `cargo new`.

There is a recommendation for using IntelliJ with the Rust plugin.
Since the latest version of the book, JetBrains has announced Rust Rover, a dedicated Rust IDE, so I imagine that would be the new recommendation.

I will be using VSCode with the rust-analyzer add-on.

## Linking

Section 1.4.1 gave tips for setting up a faster linker.
I added the configuration to [`.cargo/config.toml`](https://github.com/joseph-lozano/zero2prod/tree/main/.cargo/config.toml), making sure I installed llvm and exported the flags recommended by `brew install llvm`.

````toml
# On Windows
# ```
# cargo install -f cargo-binutils
# rustup component add llvm-tools-preview
# ```
[target.x86_64-pc-windows-msvc]
rustflags = ["-C", "link-arg=-fuse-ld=lld"]
[target.x86_64-pc-windows-gnu]
rustflags = ["-C", "link-arg=-fuse-ld=lld"]
# On Linux:
# - Ubuntu, `sudo apt-get install lld clang`
# - Arch, `sudo pacman -S lld clang`
[target.x86_64-unknown-linux-gnu]
rustflags = ["-C", "linker=clang", "-C", "link-arg=-fuse-ld=lld"]
# On MacOS, `brew install llvm` and follow steps in `brew info llvm`
[target.x86_64-apple-darwin]
rustflags = ["-C", "link-arg=-fuse-ld=lld"]
````

## Development Loop

Install `cargo install cargo-watch` and then

```bash
cargo watch -x check -x test -x run
```

## CI

The recommended Github actions CI is found on [Github](https://gist.github.com/LukeMathWalker/5ae1107432ce283310c3e601fac915f3)

And thats it for chapter 1, Onward to [Chapter 2](./chapter_2.md)!
