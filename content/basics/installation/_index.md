---
title: "Installation"
weight: 2
---

You can download the current pre-release in [Releases](https://github.com/markusmoenig/Eldiron/releases).

On macOS you can get access to the current Beta via a public [TestFlight Link](https://testflight.apple.com/join/50oZ5yds).

For ArchLinux users, simply add Eldiron from AUR:
```
yay -S eldiron-bin
```

Once Eldiron v1.0 is released it should also become available on Steam.

### Building Eldiron Locally

First, create the directory `embedded` in the `core_embed_binaries` directory:

```sh
$ mkdir core_embed_binaries/embedded
```

Than, if you have [Rust installed](https://www.rust-lang.org/tools/install), you can build Eldiron simply via
```cargo build --release --bin creator_main```

Linux:

 Make sure these dependencies are installed: `libasound2-dev` `libatk1.0-dev` `libgtk-3-dev`
