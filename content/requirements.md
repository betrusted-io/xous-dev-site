+++
title = "Requirements"
description = "Requirements to run Xous on a new platform"
date = "2022-07-22"
aliases = ["requirements"]
author = "Xous Authors"
+++

To run Xous, you will need one of three things:

1. A supported desktop platform, such as Windows, Mac, or Linux. This will let you run Xous in "hosted" mode, where the kernel acts as a server and syscalls are implemented by making TCP requests via localhost.
2. A copy of [Renode](https://renode.io), a whole-system emulator that can be used to run Xous images
3. A supported hardware device. Currently, Precursor is the only supported hardware device.

## Hosted Mode

Hosted mode runs a version of the kernel in userspace. There are native implementations of various hardware blocks. For example, the `graphics-server` draws using the [minifb](https://crates.io/crates/minifb) crate rather than drawing directly to hardware. It presents the same programming API, so this can be a good way to get a feel for what Xous is like on real hardware.

Since programs run on your local machine, you can use everyday tools to debug and improve your code. For example, you can use [flamegraph](https://crates.io/crates/flamegraph) to profile your program to figure out where it's spending its time.

The easiest way to try hosted mode is to [check out Xous](https://github.com/betrusted-io/xous-core) and run `cargo xtask run`.

Behind the scenes, `xtask` runs `target/release/kernel` and passes it the names of each program to run under hosted mode on the command line.

## Renode

Renode is a whole-system emulator capable of running the full hardware image. To run under Renode, [check out Xous](https://github.com/betrusted-io/xous-core) and run `cargo xtask renode-image`.

Then, run `renode emulation/xous-release.resc`, or if you want to use TAP to connect the emulated image to a network card run `renode emulation/xous-release-tap.resc`.

## Hardware

To build Xous for hardware, run `cargo xtask hw-image precursors/soc.svd`. This will generate and sign a hardware image which you can then load onto real hardware.
