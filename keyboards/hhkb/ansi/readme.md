HHKB Alternate Controller
===

An alternative controler for the HHKB designed by hasu.

Keyboard Maintainer: QMK Community  
Hardware Supported: HHKB Alternate Controller  
Hardware Availability: https://geekhack.org/index.php?topic=12047.0  

See [build environment setup](https://docs.qmk.fm/#/getting_started_build_tools) then the [make instructions](https://docs.qmk.fm/#/getting_started_make_guide) for more information.

## Keymap: alt_ime

This keymap is designed for **Japanese IME users using the US ANSI layout**. 

### Features
* **Dual-Role Alt Keys (Mod-Tap):**
    * **Left Alt:** Tap to switch to **English** / Hold for `LAlt`.
    * **Right Alt:** Tap to switch to **Japanese** / Hold for `RAlt`.

## Install QMK MSYS for Mac

```zsh
brew install python@3.12
brew install pipx
pipx ensurepath
pipx install qmk --python python3.12
```

## Download qmk_firmware for Mac

```
git clone https://github.com/yuusakuri/qmk_firmware.git
pushd qmk_firmware
qmk config user.qmk_home="$PWD"
echo "Select 3"
qmk setup
popd
```

### Build alt_ime keymap

```bash
qmk compile -kb hhkb/ansi -km alt_ime
```

### Flash alt_ime keymap

```bash
qmk flash -kb hhkb/ansi -km alt_ime
```
