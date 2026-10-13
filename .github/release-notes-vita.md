## GoldenEye 007: PS Vita Port (Japanese ROM Support)

**Draft build: review these notes and validate on hardware before publishing.**

- **Commit**: `<source_sha>` (`<short_sha>`)
- **Branch**: `<branch_name>`
- **Target**: 日本語版ROM (NTSC-J) 対応ビルド

### 導入手順
1. 事前準備として、PS Vita に `libshacccg.suprx`（SharkF00d / ShaRKBR33D 経由）が導入されていることを確認してください（3Dシェーダーコンパイルに必須）。
2. `ux0:data/GoldenEye007/` フォルダを作成し、ご自身の日本版ゴールデンアイ007 ROM（`.z64` / `.n64` / `.v64` 形式、推奨ファイル名: `ge007.jpn-final.z64` または `baserom.j.z64`）を配置してください。
3. `GE007Vita_JP.vpk` を VitaShell でインストールし、LiveArea から起動します。
4. 初回起動時に実機上でアセットの自動変換が行われ（約1分）、ゲームが起動します。
   - ※ 万一起動に失敗する場合は、`ux0:data/GoldenEye007/log.txt` をご確認ください。

### 添付ファイル
- `GE007Vita_JP.vpk`: PS Vita アプリケーションパッケージ
- `SHA256SUMS.txt`: SHA-256 チェックサム

*※ 本パッケージにゲームROMや著作権保護されたアセットは一切含まれていません。*
