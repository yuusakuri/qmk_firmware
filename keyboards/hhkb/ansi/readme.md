HHKB Alternate Controller
===

An alternative controler for the HHKB designed by hasu.

Keyboard Maintainer: QMK Community  
Hardware Supported: HHKB Alternate Controller  
Hardware Availability: https://geekhack.org/index.php?topic=12047.0  

See [build environment setup](https://docs.qmk.fm/#/getting_started_build_tools) then the [make instructions](https://docs.qmk.fm/#/getting_started_make_guide) for more information.

## Keymap: alt_lang

This keymap is designed for **Japanese IME users using the US ANSI layout**. 

### Features
* **Dual-Role Alt Keys (Mod-Tap):**
    * **Left Alt:** Tap to switch to **English** / Hold for `LAlt`.
    * **Right Alt:** Tap to switch to **Japanese** / Hold for `RAlt`.

## Keymap: alt_convert_non_convert

This keymap provides the Windows IME NonConvert and Convert keys on the Alt keys for **Japanese IME users using the US ANSI layout**.

### Features
* **Dual-Role Alt Keys (Mod-Tap):**
    * **Left Alt:** Tap for **NonConvert** (`KC_INT5`, Windows VK `0x1D`) / Hold for `LAlt`.
    * **Right Alt:** Tap for **Convert** (`KC_INT4`, Windows VK `0x1C`) / Hold for `RAlt`.

### IME switching on Windows

The keymap sends NonConvert and Convert directly, so PowerToys remapping is not required. Configure Microsoft IME to use NonConvert for IME off and Convert for IME on. Tapping the Alt keys then switches the IME input mode, while holding them continues to work as `LAlt` or `RAlt`.

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

### Build alt_lang keymap

```bash
qmk compile -kb hhkb/ansi -km alt_lang
```

### Flash alt_lang keymap

```bash
qmk flash -kb hhkb/ansi -km alt_lang
```

### Build alt_convert_non_convert keymap

```bash
qmk compile -kb hhkb/ansi -km alt_convert_non_convert
```

### Flash alt_convert_non_convert keymap

```bash
qmk flash -kb hhkb/ansi -km alt_convert_non_convert
```
