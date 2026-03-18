# C11 Compiler

A C11 compiler targeting x86-64 Linux, written in Rust. It compiles C source code to x86-64 assembly, then uses the system assembler and linker to produce executables.

## The Story

This project was an experiment in vibe coding. After Anthropic announced their "week-long multi-agent C compiler building Linux success story", I thought it could be done in a day.

This compiler is the result of about 5 hours of late-night vibe coding to get the core working, plus a few more hours of bug fixing to reach the milestone of **successfully compiling and running Doom**.

Linux requires GNU extensions and inline assembly support that would take a bit more time to implement, but the human-in-the-loop approach still makes the process much faster than fully autonomous multi-agent workflows.

## Features

- C11 language support (subset)
- x86-64 SysV ABI calling convention
- Struct/union pass-by-value
- Bitfields
- Compound literals
- Variadic functions (va_start/va_arg)
- Float/double support
- Switch statements
- Global and local initializers

## Usage

```
cargo build --release
./target/release/c11 input.c              # compile and link
./target/release/c11 -S input.c           # emit assembly
./target/release/c11 -S -o out.s input.c  # emit assembly to specific file
./target/release/c11 -c input.c           # compile to object file
./target/release/c11 -o mybin input.c     # compile, link, output to mybin
```

## Testing

GCC torture test suite results (1681 tests): ~835 pass, ~284 parse-fail, ~454 typecheck-fail, ~105 run-fail.

```
cargo test test_gcc_torture -- --nocapture
```
