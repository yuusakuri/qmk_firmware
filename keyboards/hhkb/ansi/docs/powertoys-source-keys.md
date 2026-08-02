# PowerToys Source キー対応表（US 配列）

Windows の入力言語を **US 配列**にしたときの PowerToys Keyboard Manager の Source キーと、QMK・macOS・HHKB との対応をまとめる。

## 前提

- **Mac** は、現行の MacBook 系内蔵 US ANSI キーボードを想定する。Touch Bar の有無や「F1、F2 などのキーを標準のファンクションキーとして使用」の設定によって、ファンクション列の押し方は変わる。
- **HHKB** は、HHKB Professional2 Type-S US 配列の工場出荷設定（DIP SW3 = OFF）を想定する。この設定では Delete が単独入力、Backspace が Fn + Delete になる。
- 物理入力欄の `○` は単独キー、`Fn` は標準の Fn レイヤー、`×` は同じキーイベントを物理入力できないことを表す。OS のショートカットで似た操作を実行できても、別のキーイベントなら `×` とする。
- **Win/US** は、QMK が送信したキーを Windows が意図した VK として認識できるかを示す。`○` は認識、`△` は別キーコード・IME・Num Lock などの条件付き、`×` は認識不可、`—` は対応する QMK キーなしを表す。QMK 候補が複数ある行は同じ順番で記号を並べる。
- Win/US の判定は、日本語 Microsoft IME を使用しつつ、`Layout File = KBDUS.DLL`、`LayerDriver JPN = kbdus.dll`、`OverrideKeyboardIdentifier = PCAT_101KEY`、Subtype `0`、Type `7` にした構成を前提とする。
- **Karabiner** は Mac 内蔵キーボードから物理入力できないキーについて、Karabiner-Elements の JSON で同じ HID Usage を指定できるかを示す。`○` は対応、`△` は同じ Windows VK への変換が入力言語などに依存、`×` は対応する名前がない、`—` は確認不要を表す。
- **標準動作**は Windows・macOS・Linux で想定される主な動きを短く列挙する。
- **候補**は、PowerToys・VK・QMK の各列に使用可能な値があり、Win/US が `○`、Mac と HHKB がともに `×` であるという条件をすべて満たす場合のみ `○` とする。それ以外は `×` とする。

PowerToys の実装は仮想キー `1..255` を列挙し、名前を持たない値も `VK n` として Source に追加する。そのため、本表は US 配列で文字名になるキーと、PowerToys が明示的な名前を付けるキーボード向けキーを対象とする。マウスボタン、ゲームパッド、予約・未割当・OEM 固有の `VK n` は、標準的な QMK キー名や全 OS 共通の操作がないため除外する。

列名は次の意味である。

| 列 | 意味 |
| --- | --- |
| PowerToys | Source 一覧に表示される名前 |
| VK | Windows 仮想キーコード |
| Win/US | 上記の Windows US 構成での QMK キー認識 |
| QMK | `keymap.c` に記載するキー名 |
| Mac | Mac 内蔵 US キーボードでの物理入力 |
| HHKB | HHKB Professional2 Type-S US での物理入力 |
| Karabiner | Mac で物理入力できない場合の対応状況 |
| 標準動作 | Windows / macOS / Linux での代表的な動作 |
| 候補 | 指定した条件をすべて満たすか |

## 文字キー

| PowerToys | VK | Win/US | QMK | Mac | HHKB | Karabiner | 標準動作 | 候補 |
| --- | --- | :---: | --- | :---: | :---: | --- | --- | :---: |
| `A`–`Z` | `0x41`–`0x5A` | ○ | `KC_A`–`KC_Z` | ○ | ○ | — | 文字入力 | × |
| `0`–`9` | `0x30`–`0x39` | ○ | `KC_0`–`KC_9` | ○ | ○ | — | 数字、Shift 記号 | × |
| `;` | `0xBA` | ○ | `KC_SCLN` | ○ | ○ | — | `;`、`:` | × |
| `=` | `0xBB` | ○ | `KC_EQL` | ○ | ○ | — | `=`、`+` | × |
| `,` | `0xBC` | ○ | `KC_COMM` | ○ | ○ | — | `,`、`<` | × |
| `-` | `0xBD` | ○ | `KC_MINS` | ○ | ○ | — | `-`、`_` | × |
| `.` | `0xBE` | ○ | `KC_DOT` | ○ | ○ | — | `.`、`>` | × |
| `/` | `0xBF` | ○ | `KC_SLSH` | ○ | ○ | — | `/`、`?` | × |
| `` ` `` | `0xC0` | ○ | `KC_GRV` | ○ | ○ | — | `` ` ``、`~` | × |
| `[` | `0xDB` | ○ | `KC_LBRC` | ○ | ○ | — | `[`、`{` | × |
| `\` | `0xDC` | ○ | `KC_BSLS` | ○ | ○ | — | `\`、`\|` | × |
| `]` | `0xDD` | ○ | `KC_RBRC` | ○ | ○ | — | `]`、`}` | × |
| `'` | `0xDE` | ○ | `KC_QUOT` | ○ | ○ | — | `'`、`"` | × |

`VK_OEM_102 (0xE2)` は ISO 102 キーであり、US ANSI 配列の対象外とする。

## 基本・修飾・移動キー

| PowerToys | VK | Win/US | QMK | Mac | HHKB | Karabiner | 標準動作 | 候補 |
| --- | --- | :---: | --- | :---: | :---: | --- | --- | :---: |
| `Backspace` | `0x08` | ○ | `KC_BSPC` | ○（Delete 表記） | Fn | — | 左側削除 | × |
| `Tab` | `0x09` | ○ | `KC_TAB` | ○ | ○ | — | 次項目、タブ入力 | × |
| `Enter` | `0x0D` | ○ | `KC_ENT` | ○（Return 表記） | ○ | — | 決定、改行 | × |
| `Esc` | `0x1B` | ○ | `KC_ESC` | ○ | ○ | — | キャンセル、終了 | × |
| `Space` | `0x20` | ○ | `KC_SPC` | ○ | ○ | — | 空白入力 | × |
| `PgUp` | `0x21` | ○ | `KC_PGUP` | Fn | Fn | — | 1 ページ上へ | × |
| `PgDn` | `0x22` | ○ | `KC_PGDN` | Fn | Fn | — | 1 ページ下へ | × |
| `End` | `0x23` | ○ | `KC_END` | Fn | Fn | — | 行末、文書末へ | × |
| `Home` | `0x24` | ○ | `KC_HOME` | Fn | Fn | — | 行頭、文書先頭へ | × |
| `Left` | `0x25` | ○ | `KC_LEFT` | ○ | Fn | — | 左移動 | × |
| `Up` | `0x26` | ○ | `KC_UP` | ○ | Fn | — | 上移動 | × |
| `Right` | `0x27` | ○ | `KC_RGHT` | ○ | Fn | — | 右移動 | × |
| `Down` | `0x28` | ○ | `KC_DOWN` | ○ | Fn | — | 下移動 | × |
| `Select` | `0x29` | × | `KC_SLCT` | × | × | ○ `select` | 選択、無視 | × |
| `Print` | `0x2A` | — | — | × | × | × | 印刷、無視 | × |
| `Execute` | `0x2B` | × | `KC_EXEC` | × | × | ○ `execute` | 実行、無視 | × |
| `Print Screen` | `0x2C` | ○ | `KC_PSCR` | × | Fn | ○ `print_screen` | スクリーンショット、F13 | × |
| `Insert` | `0x2D` | ○ | `KC_INS` | × | Fn | ○ `insert` | 挿入モード切替、無視 | × |
| `Delete` | `0x2E` | ○ | `KC_DEL` | Fn | ○ | — | 右側削除 | × |
| `Help` | `0x2F` | × | `KC_HELP` | × | × | ○ `help` | ヘルプ、無視 | × |
| `Apps/Menu` | `0x5D` | ○ | `KC_APP` | × | × | ○ `application` | コンテキストメニュー、無視 | ○ |
| `Sleep` | `0x5F` | ○ | `KC_SLEP` | × | × | ○ `system_sleep` | スリープ | ○ |
| `Alt` | `0x12` | ○ | `KC_LALT` / `KC_RALT` | ○ | ○ | — | Alt、Option | × |
| `Alt (Left)` | `0xA4` | ○ | `KC_LALT` | ○ | ○ | — | 左 Alt、左 Option | × |
| `Alt (Right)` | `0xA5` | ○ | `KC_RALT` | ○ | ○ | — | 右 Alt、AltGr、右 Option | × |
| `Ctrl` | `0x11` | ○ | `KC_LCTL` / `KC_RCTL` | ○ | ○ | — | Control | × |
| `Ctrl (Left)` | `0xA2` | ○ | `KC_LCTL` | ○ | ○ | — | 左 Control | × |
| `Ctrl (Right)` | `0xA3` | ○ | `KC_RCTL` | × | × | ○ `right_control` | 右 Control | ○ |
| `Shift` | `0x10` | ○ | `KC_LSFT` / `KC_RSFT` | ○ | ○ | — | Shift | × |
| `Shift (Left)` | `0xA0` | ○ | `KC_LSFT` | ○ | ○ | — | 左 Shift | × |
| `Shift (Right)` | `0xA1` | ○ | `KC_RSFT` | ○ | ○ | — | 右 Shift | × |
| `Win` | PowerToys 内部値 | ○ | `KC_LGUI` / `KC_RGUI` | ○（Command） | ○ | — | Windows、Command、Super | × |
| `Win (Left)` | `0x5B` | ○ | `KC_LGUI` | ○（Command） | ○ | — | 左 Windows、左 Command、左 Super | × |
| `Win (Right)` | `0x5C` | ○ | `KC_RGUI` | ○（Command） | ○ | — | 右 Windows、右 Command、右 Super | × |

## ファンクション・ロックキー

| PowerToys | VK | Win/US | QMK | Mac | HHKB | Karabiner | 標準動作 | 候補 |
| --- | --- | :---: | --- | :---: | :---: | --- | --- | :---: |
| `Caps Lock` | `0x14` | ○ | `KC_CAPS` | ○ | Fn | — | Caps Lock | × |
| `F1`–`F12` | `0x70`–`0x7B` | ○ | `KC_F1`–`KC_F12` | Fn | Fn | — | ファンクション、システム機能 | × |
| `F13`–`F24` | `0x7C`–`0x87` | ○ | `KC_F13`–`KC_F24` | × | × | ○ `f13`–`f24` | ファンクション、ショートカット、無視 | ○ |
| `Num Lock` | `0x90` | ○ | `KC_NUM` | × | × | ○ `keypad_num_lock` | 数字入力切替、Clear | ○ |
| `Scroll Lock` | `0x91` | ○ | `KC_SCRL` | × | Fn | ○ `scroll_lock` | スクロール切替、F14、無視 | × |
| `Pause` | `0x13` | ○ | `KC_PAUS` | × | Fn | ○ `pause` | 一時停止、F15、無視 | × |
| `Break` | `0x03` | × | `KC_CNCL`（近似） | × | Ctrl + Fn + Pause | ○ `cancel` | 中断、キャンセル、無視 | × |
| `Clear` | `0x0C` | × / △ | `KC_CLR` / `KC_P5`（Num Lock off） | × | × | ○ `clear` / `keypad_5` | Clear、無視 | × |

`F13`–`F24` は両方の物理キーボードから通常入力できず、PowerToys・QMK・Karabiner のすべてが明示的に扱える。中継キー候補として Browser キーより副作用が少ないが、OS やアプリにショートカットが登録されていれば動作するため、完全な「無反応キー」ではない。

## テンキー

| PowerToys | VK | Win/US | QMK | Mac | HHKB | Karabiner | 標準動作 | 候補 |
| --- | --- | :---: | --- | :---: | :---: | --- | --- | :---: |
| `NumPad 0`–`NumPad 9` | `0x60`–`0x69` | △ | `KC_P0`–`KC_P9` | × | × | ○ `keypad_0`–`keypad_9` | 数字、移動 | × |
| `*` | `0x6A` | ○ | `KC_PAST` | × | Fn | ○ `keypad_asterisk` | 乗算 | × |
| `+` | `0x6B` | ○ | `KC_PPLS` | × | Fn | ○ `keypad_plus` | 加算 | × |
| `Separator` | `0x6C` | × | `KC_SEPR` | × | × | ○ `separator` | 区切り、無視 | × |
| `- (Subtract)` | `0x6D` | ○ | `KC_PMNS` | × | Fn | ○ `keypad_hyphen` | 減算 | × |
| `. (Numpad)` | `0x6E` | △ | `KC_PDOT` | × | × | ○ `keypad_period` | 小数点、Delete | × |
| `/` / `/ (Numpad)` | `0x6F` | ○ | `KC_PSLS` | × | Fn | ○ `keypad_slash` | 除算 | × |
| `Enter (Numpad)` | `0x0D` + Numpad | ○ | `KC_PENT` | × | Fn | ○ `keypad_enter` | 決定、改行 | × |
| `Insert (Numpad)` | `0x2D` + Numpad | △ | `KC_P0`（Num Lock off） | × | × | ○ `keypad_0` | Insert | × |
| `Delete (Numpad)` | `0x2E` + Numpad | △ | `KC_PDOT`（Num Lock off） | × | × | ○ `keypad_period` | Delete | × |
| `End (Numpad)` | `0x23` + Numpad | △ | `KC_P1`（Num Lock off） | × | × | ○ `keypad_1` | End | × |
| `Down (Numpad)` | `0x28` + Numpad | △ | `KC_P2`（Num Lock off） | × | × | ○ `keypad_2` | 下移動 | × |
| `PgDn (Numpad)` | `0x22` + Numpad | △ | `KC_P3`（Num Lock off） | × | × | ○ `keypad_3` | 1 ページ下へ | × |
| `Left (Numpad)` | `0x25` + Numpad | △ | `KC_P4`（Num Lock off） | × | × | ○ `keypad_4` | 左移動 | × |
| `Right (Numpad)` | `0x27` + Numpad | △ | `KC_P6`（Num Lock off） | × | × | ○ `keypad_6` | 右移動 | × |
| `Home (Numpad)` | `0x24` + Numpad | △ | `KC_P7`（Num Lock off） | × | × | ○ `keypad_7` | Home | × |
| `Up (Numpad)` | `0x26` + Numpad | △ | `KC_P8`（Num Lock off） | × | × | ○ `keypad_8` | 上移動 | × |
| `PgUp (Numpad)` | `0x21` + Numpad | △ | `KC_P9`（Num Lock off） | × | × | ○ `keypad_9` | 1 ページ上へ | × |

PowerToys の `(Numpad)` は VK 自体ではなく、同じ VK にテンキー由来フラグを付けて区別する内部表現である。

## ブラウザー・メディア・起動キー

| PowerToys | VK | Win/US | QMK | Mac | HHKB | Karabiner | 標準動作 | 候補 |
| --- | --- | :---: | --- | :---: | :---: | --- | --- | :---: |
| `Browser Back` | `0xA6` | ○ | `KC_WBAK` | × | × | ○ `ac_back` | 戻る | ○ |
| `Browser Forward` | `0xA7` | ○ | `KC_WFWD` | × | × | ○ `ac_forward` | 進む | ○ |
| `Browser Refresh` | `0xA8` | ○ | `KC_WREF` | × | × | ○ `ac_refresh` | 再読み込み | ○ |
| `Browser Stop` | `0xA9` | ○ | `KC_WSTP` | × | × | **× `ac_stop` なし** | 読み込み停止、停止、無視 | ○ |
| `Browser Search` | `0xAA` | ○ | `KC_WSCH` | × | × | ○ `ac_search` | 検索、無視 | ○ |
| `Browser Favorites` | `0xAB` | ○ | `KC_WFAV` | × | × | ○ `ac_bookmarks` | お気に入り、ブックマーク | ○ |
| `Browser Home` | `0xAC` | ○ | `KC_WHOM` | × | × | ○ `ac_home` | ホームページ、ホーム | ○ |
| `Volume Mute` | `0xAD` | ○ | `KC_MUTE` | ○ | Fn | — | 音量ミュート | × |
| `Volume Down` | `0xAE` | ○ | `KC_VOLD` | ○ | Fn | — | 音量を下げる | × |
| `Volume Up` | `0xAF` | ○ | `KC_VOLU` | ○ | Fn | — | 音量を上げる | × |
| `Next Track` | `0xB0` | ○ | `KC_MNXT` | ○ | × | — | 次のトラック | × |
| `Previous Track` | `0xB1` | ○ | `KC_MPRV` | ○ | × | — | 前のトラック | × |
| `Stop Media` | `0xB2` | ○ | `KC_MSTP` | × | × | ○ `stop` | メディア停止 | ○ |
| `Play/Pause Media` | `0xB3` | ○ | `KC_MPLY` | ○ | × | — | 再生、一時停止 | × |
| `Start Mail` | `0xB4` | ○ | `KC_MAIL` | × | × | ○ `al_email_reader` | メール起動、無視 | ○ |
| `Select Media` | `0xB5` | ○ | `KC_MSEL` | × | × | ○ `al_consumer_control_configuration` | メディア選択、プレーヤー起動、無視 | ○ |
| `Start App 1` | `0xB6` | ○ | `KC_MYCM` | × | × | ○ `al_local_machine_browser` | コンピューター表示、アプリ起動、無視 | ○ |
| `Start App 2` | `0xB7` | ○ | `KC_CALC` | × | × | ○ `al_calculator` | 電卓、アプリ起動、無視 | ○ |

`Browser Search` は USB HID Consumer Page の `AC Search (0x0221)`、`Browser Stop` は `AC Stop (0x0226)` に対応する。両者は全 OS 共通の識別子ではあるが、標準動作は共通ではない。特に Karabiner-Elements は現在 `ac_search` を定義する一方、`ac_stop` を定義していない。

## IME キー

| PowerToys | VK | Win/US | QMK | Mac | HHKB | Karabiner | 標準動作 | 候補 |
| --- | --- | :---: | --- | :---: | :---: | --- | --- | :---: |
| `IME Hangul` | `0x15` | × / △ | `KC_LNG1` / `KC_INT2` | × | × | △ `lang1` / `international2` | Hangul、Kana、入力ソース切替、無視 | × |
| `IME On` | `0x16` | — | — | × | × | × | IME オン、無視 | × |
| `IME Junja` | `0x17` | — | — | × | × | × | Junja、無視 | × |
| `IME Final` | `0x18` | — | — | × | × | × | Final、無視 | × |
| `IME Kanji` | `0x19` | × | `KC_LNG2` | × | × | △ `lang2` | Kanji、Hanja、入力ソース切替、無視 | × |
| `IME Off` | `0x1A` | — | — | × | × | × | IME オフ、無視 | × |
| `IME Convert` | `0x1C` | ○ | `KC_INT4` | × | × | ○ `japanese_pc_xfer` | 変換 | ○ |
| `IME Non-Convert` | `0x1D` | ○ | `KC_INT5` | × | × | ○ `japanese_pc_nfer` | 無変換 | ○ |
| `IME Kana` ※ | `0x1E` | — | — | × | × | × | IME Accept、Kana、無視 | × |
| `IME Mode Change` | `0x1F` | — | — | × | × | × | IME モード変更、無視 | × |

※ PowerToys の現行実装は `VK_ACCEPT (0x1E)` に `IME Kana` という表示名を付けている。また、同じ値 `0x15` を持つ `VK_KANA` / `VK_HANGUL` の表示は最後の代入によって `IME Hangul` になる。したがって表示名だけで日本語 IME キーとの一致を判断しない。

`KC_LNG1`–`KC_LNG9` は QMK の対応表で Windows 非対応であり、この Win/US 構成で確認済みの `KC_LNG1` / `KC_LNG2` も認識されない。`KC_INT1`–`KC_INT5` は Windows 対応だが入力言語との対応が必要で、`KC_INT6`–`KC_INT9` は Windows では使用できない。

## 旧式・Windows 固有キー

| PowerToys | VK | Win/US | QMK | Mac | HHKB | Karabiner | 標準動作 | 候補 |
| --- | --- | :---: | --- | :---: | :---: | --- | --- | :---: |
| `Packet` | `0xE7` | — | — | × | × | × | Unicode パケット | × |
| `Attn` | `0xF6` | × | `KC_SYRQ` | × | × | ○ `sys_req_or_attention` | Attention、SysReq、無視 | × |
| `CrSel` | `0xF7` | × | `KC_CRSL` | × | × | ○ `cr_sel_or_props` | CrSel、プロパティ、無視 | × |
| `ExSel` | `0xF8` | × | `KC_EXSL` | × | × | ○ `ex_sel` | ExSel、無視 | × |
| `Erase EOF` | `0xF9` | × | `KC_ERAS` | × | × | ○ `alternate_erase` | Alternate Erase、無視 | × |
| `Play` | `0xFA` | — | — | × | × | × | 旧式再生、無視 | × |
| `Zoom` | `0xFB` | — | — | × | × | × | ズーム、無視 | × |
| `PA1` | `0xFD` | — | — | × | × | × | PA1、無視 | × |
| `Clear`（OEM） | `0xFE` | — | — | × | × | × | OEM Clear、無視 | × |
| `Undefined` | `0xFF` | — | — | × | × | × | 未定義、無視 | × |

これらは同名または近い名前の USB HID Consumer キーと同一とは限らず、中継キーには推奨しない。

## 参照

- [PowerToys `keyboard_layout.cpp`](https://github.com/microsoft/PowerToys/blob/d2c53bf3861ed2688a1c30aafd66ea0fc0186399/src/common/interop/keyboard_layout.cpp) — Source 候補の列挙と表示名
- [Microsoft Virtual-Key Codes](https://learn.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes) — VK 値と Windows 上の意味
- [QMK Basic Keycodes](../../../../docs/keycodes_basic.md) — QMK キー名
- [Karabiner keyboard key codes](https://github.com/pqrs-org/Karabiner-Elements/blob/385e317272f1cf5398029f1832e42fb5b6b45d24/src/share/types/momentary_switch_event_details/key_code.hpp) — Keyboard / Keypad Page の対応名
- [Karabiner consumer key codes](https://github.com/pqrs-org/Karabiner-Elements/blob/385e317272f1cf5398029f1832e42fb5b6b45d24/src/share/types/momentary_switch_event_details/consumer_key_code.hpp) — Consumer Page の対応名
- [Karabiner Generic Desktop codes](https://github.com/pqrs-org/Karabiner-Elements/blob/385e317272f1cf5398029f1832e42fb5b6b45d24/src/share/types/momentary_switch_event_details/generic_desktop.hpp) — `system_sleep` など
- [USB HID Usage Tables 1.4](https://www.usb.org/sites/default/files/hut1_4.pdf) — USB HID Usage Page / Usage ID
- [Apple: Mac keyboard shortcuts](https://support.apple.com/en-us/102650) — Mac 内蔵キーボードの Fn 操作
- [HHKB Professional2 key layout](https://happyhackingkb.com/jp/products/image/leaflet/hhkb_pro_2_keylayout.pdf) — HHKB Professional2 の物理・Fn 配列
- [HHKB FAQ: Delete キーを Backspace キーとして使う](https://faq.pfu.jp/faq/show/2659?site_domain=hhkb) — DIP SW3 による切り替え
