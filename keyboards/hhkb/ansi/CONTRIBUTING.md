# Developer Guide

## Syncing with Upstream

One-time setup (Reference only - already configured)

```
git remote add upstream https://github.com/qmk/qmk_firmware.git
```

Use the following commands to synchronize this fork with the main QMK Firmware repository:

```
git fetch upstream
git checkout master
git rebase upstream/master
make git-submodule
git push origin master
```
