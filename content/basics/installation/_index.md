---
title: "Installation"
weight: 2
---

You can download the current pre-release in [Releases](https://github.com/markusmoenig/Eldiron/releases).

For ArchLinux users, simply add Eldiron from AUR:
```
yay -S eldiron-bin
```

Once Eldiron v1.0 is released it should also become available on Steam.

### Building Eldiron Locally

If you have [Rust installed](https://www.rust-lang.org/tools/install), you can build Eldiron simply via
```cargo build --release --package creator```

Linux:

 Make sure these dependencies are installed: `libasound2-dev` `libatk1.0-dev` `libgtk-3-dev`
