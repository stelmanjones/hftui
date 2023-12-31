# Home

{{#include ../../README.md}}

## Introduction

[`ratatui`](https://github.com/ratatui-org/ratatui) is a Rust library to build rich terminal user
interfaces (TUIs) and dashboards. It is a community fork of the original
[`tui-rs`](https://github.com/fdehau/tui-rs) created to maintain and improve the project.

The [source code of this project](https://github.com/ratatui-org/ratatui-async-template) is an
opinionated template for getting up and running with `ratatui`. You can pick and choose the pieces
of this `ratatui-async-template` to suit your needs and sensibilities. This rest of this
documentation is a walk-through of why the code is structured the way it is, so that you are aided
in modifying it as you require.

## Background

`ratatui` is based on the principle of immediate rendering with intermediate buffers. This means
that at each new frame you have to build all widgets that are supposed to be part of the UI. In
short, the `ratatui` library is largely handles just drawing to the terminal.

Additionally, the library does not provide any input handling nor any event system. The
responsibility of getting keyboard input events, modifying the state of your application based on
those events and figuring out which widgets best reflect the view of the state of your application
is on you.

The `ratatui-org` project has added a template that covers the basics, and you find that here:
<https://github.com/ratatui-org/rust-tui-template>.

I wanted to take another stab at a template, one that uses `tokio` and organizes the code a little
differently. This is an opinionated view on how to organize a `ratatui` project.

```admonish info
Since `ratatui` is a immediate mode rendering based library, there are _multiple_ ways to organize your code, and there's no real "right" answer.
Choose whatever works best for you!
```

This project also adds commonly used dependencies like logging, command line arguments,
configuration options, etc.

As part of this documentation, we'll walk through some of the different ways you may choose to
organize your code and project in order to build a functioning terminal user interface. You can pick
and choose the parts you like.

You may also want to check out the following links (roughly in order of increasing complexity):

- <https://github.com/ratatui-org/ratatui/tree/main/examples>: Simple one-off examples to illustrate
  various widgets and features in `ratatui`.
- <https://github.com/ratatui-org/rust-tui-template>: Starter kit for using `ratatui`
- <https://github.com/ratatui-org/ratatui-book/tree/main/ratatui-book-tutorial-project>: Tutorial
  project that the user a simple interface to enter key-value pairs, which will printed in json.
- <https://github.com/ratatui-org/ratatui-async-template>: Async tokio crossterm based opinionated
  starter kit for using `ratatui`.
- <https://github.com/veeso/tui-realm/>: A framework for `tui.rs` to simplify the implementation of
  terminal user interfaces adding the possibility to work with re-usable components with properties
  and states.

## Usage

You can start by git cloning the project:

```bash
git clone https://github.com/kdheepak/ratatui-async-template your-project-name-here
```

I also recommend renaming both `ratatui-async-template` and `RATATUI_ASYNC_TEMPLATE` in all files
with the name of your project.

```bash
$ rg -i 'ratatui.async.template'

Cargo.toml
2:name = "ratatui-async-template"
62:name = "ratatui-async-template"

build.rs
45:println!("cargo:rustc-env=RATATUI_ASYNC_TEMPLATE_GIT_INFO={}", git_describe);

src/main.rs
3:use ratatui_async_template::{

.github/workflows/cd.yml
17:file: target/release/ratatui-async-template
21:file: target/release/ratatui-async-template.exe
25:file: target/release/ratatui-async-template
65:name: ratatui-async-template-${{ matrix.os }}
67:target/release/ratatui-async-template${{ matrix.os == 'windows-latest' && '.exe' || '' }}
87:asset_path: ./target/release/ratatui-async-template${{ matrix.os == 'windows-latest' && '.exe' || [... 0 more matches]
88:asset_name: ratatui-async-template-${{ matrix.os }}
```

Here's some other changes you probably want to make:

```bash
$ rg "dheepak"

LICENSE
1:Copyright (c) 2023 Dheepak Krishnamurthy

Cargo.toml
5:authors = ["Dheepak Krishnamurthy"]

src/utils.rs
32:} else if let Some(proj_dirs) = ProjectDirs::from("com", "kdheepak", "ratatui-async-template") {
45:} else if let Some(proj_dirs) = ProjectDirs::from("com", "kdheepak", "ratatui-async-template") {
```
