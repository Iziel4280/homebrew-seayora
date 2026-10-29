# Seayora Bridge for Homebrew

The [Seayora Bridge](https://seayora.com/download/bridge) connects the security
cameras and building equipment on a property's own network to Seayora — outbound
only, with camera passwords only that computer can open.

```sh
brew install iziel4280/seayora/seabridge
seabridge ABCD-2345
```

The code comes from Seayora: **Cameras → Bridges → Add a bridge**. It works once,
for 30 minutes. `seabridge` asks for your password, because the bridge runs as a
service that starts with the computer (a launchd daemon on a Mac, a system service
on Linux).

Afterwards:

```sh
seabridge status     # how it is doing
seabridge doctor     # what is wrong, if anything
seabridge logs       # follow its log
seabridge uninstall  # remove the bridge (brew uninstall removes only the installer)
```

Works on macOS 13.5 or later (Apple silicon or Intel) and on 64-bit Linux with
Homebrew (x86-64 or ARM64). On a Raspberry Pi, Alpine, a 32-bit system or a NAS,
use one of the other ways on [seayora.com/download/bridge](https://seayora.com/download/bridge).

## What this formula does

It downloads the same signed package as the download page (1.7.0 today) and
keeps it packed. The first `seabridge` unpacks it as root and runs the package's own
installer, which checks every file against Seayora's signature before installing
anything. The bridge then updates itself with releases Seayora signs, so
`brew upgrade` only matters for new installs.

Guide: https://seayora.com/docs/security-cameras

This repository is written by `backend/scripts/homebrew_formula.cjs` in Seayora's
own repository. Changes made here by hand are overwritten.
