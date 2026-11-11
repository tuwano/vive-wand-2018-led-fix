# VIVE Wand 2018 LED Fix

An unofficial, experimental tool for VIVE Wand 2018 controllers whose LED stays orange after charging is complete.

**Current version: V1.1 — experimental / pre-release.**

[Releases](https://github.com/tuwano/vive-wand-2018-led-fix/releases) · [Bug reports](https://github.com/tuwano/vive-wand-2018-led-fix/issues)

## English

### Compatibility

- Windows with SteamVR installed at `C:\Program Files (x86)\Steam\steamapps\common\SteamVR`.
- VIVE Wand 2018: hardware ID `0x81020006`, application firmware version `1526689969`.
- Other hardware IDs and firmware versions are not supported by this package. Compatibility is checked before writing.

### What it changes

The observed failure was a charging-state transition from code `2` to `3` while the LED remained in orange state `2`. The fix preserves the existing notification processing and adds an existing LED-update event for this specific transition when the battery data and LED state meet the required conditions.

The patch adds no changes to charging voltage, charging current, or charge-termination settings.

### Use

1. Download the packaged tool ZIP from **Releases**, when available, and extract the entire archive.
2. Keep the two BAT files, `HowToUse.txt`, and `_Data` together.
3. Close SteamVR and `lighthouse_console`.
4. Connect **exactly one Wand** to the PC with a USB data cable.
5. Run `FixWand2018.bat`. It saves and verifies a recovery set before writing the fix.
6. Keep USB connected until the operation finishes.

The tool's normal screen messages are in English. Detailed English, Japanese, and Korean instructions are included in `HowToUse.txt`.

### Restore the original application

Run `RestoreWand2018.bat` only when you want to remove the fix.

V1.1 requires an **existing, verified recovery set for the connected controller's serial number** before restoration starts. Keep `_Data\backups` when updating the tool. Saved configuration and calibration data are checked and, only if different, written back to the same controller and verified by reading them again.

Recovery sets contain configuration/calibration JSON read from the controller and a supplied original SteamVR application firmware file. They are **not a readback of the controller's installed firmware or a full flash-memory backup**. Radio, FPGA, and bootloader restoration are not included. Recovery depends on the bootloader being detectable and is not guaranteed.

### Test status

- A modified-firmware reply with marker `D2`, battery level 100%, LED state `3`, and charging-state code `3` was obtained on one controller. Its owner reported an orange-to-white LED transition.
- Repeated charging cycles and a broader range of controllers have not been verified.
- The V1.1 PC workflow has received static checks, but its complete backup/restore workflow has not yet been verified on Windows hardware.
- Firmware modification can leave a controller unable to start. Please treat this as an experimental project.

### Report a problem

Use **Issues** and include the tool version, the operation performed, the on-screen error code/reason, and the LED color. Logs are saved in `_Data\logs`. Remove personal information before posting logs publicly.

## 日本語

### 対応環境

- Windowsと、標準パス `C:\Program Files (x86)\Steam\steamapps\common\SteamVR` にインストールされたSteamVR。
- VIVE Wand 2018：HWID `0x81020006`、アプリファーム版 `1526689969`。
- このパッケージは他の型式・ファーム版には対応していません。書き込み前に対応可否を確認します。

### 修正内容

充電状態コードが `2` から `3` へ変わっても、LEDがオレンジの状態 `2` に残る現象を観測しました。既存の通知処理を保持し、バッテリー情報とLED状態が所定の条件を満たす時、この変化に対して既存のLED更新イベントを追加します。

充電電圧・充電電流・充電終了条件の設定を変更する処理は追加していません。

### 使い方

1. 公開後、**Releases**から配布用ZIPをダウンロードし、全体を展開します。
2. 2本のbat、`HowToUse.txt`、`_Data`を一緒に保管します。
3. SteamVRと`lighthouse_console`を終了します。
4. データ通信対応USBケーブルで、Wandを**必ず1台だけ**PCへ接続します。
5. `FixWand2018.bat`を実行します。復元用セットを保存・検証してから修正ファームを書き込みます。
6. 完了までUSBを抜かないでください。

通常の画面表示は英語です。詳しい英語・日本語・韓国語の手順は、同梱の`HowToUse.txt`に記載しています。

### 純正アプリへ戻す

修正を取り除きたい時だけ`RestoreWand2018.bat`を実行します。

V1.1では、復元開始前に**接続した個体と同じシリアル番号の、有効な保存済み復元用セット**が必要です。ツール更新時は`_Data\backups`を引き継いでください。保存した設定・校正データを確認し、異なる場合だけ同じ個体へ書き戻して、再読み出しで検証します。

復元用セットには、実機から読み出した設定・校正JSONと、同梱のSteamVR純正アプリファームを保存します。**現在入っているファーム本体を実機から読み出したものでも、全フラッシュメモリのバックアップでもありません。** radio・FPGA・ブートローダーの復元は含みません。復元にはブートローダーを認識できることが必要で、復元成功を保証するものではありません。

### 検証状況

- 1台の実機で、修正版の応答マーカー`D2`、残量100%、LED状態`3`、充電状態コード`3`を取得し、所有者からオレンジ→白色への切り替えの報告を受けています。
- 繰り返しの充電サイクルや、幅広い個体での動作は未検証です。
- V1.1のPC側処理は静的確認済みですが、バックアップ・復元の全工程はWindows実機で未検証です。
- ファームの変更により起動できなくなる可能性があります。試験的なプロジェクトとして扱ってください。

### 不具合報告

**Issues**へ、ツールのバージョン・行った操作・画面のエラーコードと理由・LED色を記載してください。ログは`_Data\logs`へ保存されます。公開するログからは個人情報を除いてください。
