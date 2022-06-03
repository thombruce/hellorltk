# Hello, Rust!

This is my learning project, following an excellent guide to creating a roguelike game using Rust. The brilliant tutorial, written by Herbert Wolverson, can be found here: https://bfnightly.bracketproductions.com/chapter_0.html

## A Note About WSL

Wolverson's tutorial is pretty amazing, and makes for an excellent introduction to Rust if you ask me... with only one minor snag so far: Windows Subsystem for Linux (WSL 2).

When it came time to run a windowed application, with `cargo run`, the process failed with something akin to the following error:

```
thread 'main' panicked at 'called `Option::unwrap()` on a `None` value'...
```

I searched for a solution and found the same error raised in an issue on the glutin repo, [here](https://github.com/rust-windowing/glutin/issues/1399).

The issue, I believe, is a lack of permission for the WSL instance to create windowed Linux applications... _I don't know this for a fact, but it seems about right._

The solution, then, is to build for Windows instead. We need to install a couple of build dependencies, and then run `cargo run` targeting the Windows environment instead:

```shell
# One time setup
sudo apt update && sudo apt install mingw-w64
rustup target add x86_64-pc-windows-gnu

# Run the application
cargo run --target x86_64-pc-windows-gnu
```

_You may need to tweak this for your particular machine. To obtain a list of available targets:_

```shell
rustc --print target-list
```

And hey presto! _It just works!_
