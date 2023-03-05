---
title: "Installation"
weight: 2
---

You can download the current pre-release in [Releases](https://github.com/markusmoenig/Eldiron/releases).

## Building Eldiron Locally

First, create the directory `embedded` in the `core_embed_binaries` directory:

```sh
$ mkdir core_embed_binaries/embedded
```

Than, if you have [Rust installed](https://www.rust-lang.org/tools/install), you can build Eldiron simply via
```cargo build --release```

Linux:

 Make sure these dependencies are installed: `libasound2-dev` `libatk1.0-dev` `libgtk-3-dev`
