## GoldenEye 007: PS Vita Port (Japanese ROM Support)

**Draft build: review these notes and validate on hardware before publishing.**

- **Commit**: `<source_sha>` (`<short_sha>`)
- **Branch**: `<branch_name>`
- **Target**: 日本語版ROM (NTSC-J) 対応ビルド

### 導入手順
1. `GE007Vita_JP.vpk` をダウンロードし、PS Vita に転送してインストールします。
2. `ux0:data/GoldenEye007/` フォルダにご自身の日本版ゴールデンアイ007 ROM（`.z64` 形式、ファイル名: `ge007.jpn-final.z64` または `baserom.j.z64`）を配置してください。
3. 初回起動時に実機上でアセットの自動変換が行われ、日本語で起動します。

### 添付ファイル
- `GE007Vita_JP.vpk`: PS Vita アプリケーションパッケージ
- `SHA256SUMS.txt`: SHA-256 チェックサム

*※ 本パッケージにゲームROMや著作権保護されたアセットは一切含まれていません。*
