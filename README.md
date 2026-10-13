# GoldenEye 007 — PS Vita Port (日本語版ROM対応)

![license](https://img.shields.io/badge/license-MIT-green)
![platform](https://img.shields.io/badge/platform-PS%20Vita-blue)

<p align="center">
  本リポジトリは、<a href="https://github.com/kaziema/gevita">kaziema/gevita</a> をベースに、<br>
  <b>Nintendo 64 日本語版ROM（NTSC-J）に対応させたフォーク</b>です。<br>
  エミュレータではなく、実機ネイティブクロスコンパイルにより動作します。ゲームデータ・アセットは一切含まれていません。
</p>

<p align="center">
  <a href="https://github.com/kaziema/gevita"><b>⬆ フォーク元 (PS Vita移植版 / US版ROM対応)</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/jkdansereau/goldeneye-pc-port"><b>⬆ アップストリーム (PC版)</b></a>
</p>

---

## 本リポジトリについて (About This Fork)

本プロジェクトは、[kaziema/gevita](https://github.com/kaziema/gevita) のPS Vita移植版をベースに、日本版ROMへの対応を行ったフォークです。

- **日本語版ROMアセット抽出の修正**: 上流 CSV（`scripts/filelist.j.csv`）のタイポを修正し、日本語版アセットシンボル（`port/src/romassets_j.s`）を正常生成。
- **実機アセットコンバータの拡張**: `tools_pc/gen_pcconv_tables.py` および `port/src/pcconv_tables.c` を更新し、日本版ROMのモデル・CG・セットアップをVita実機上で正しく抽出・変換可能に修正。
- **動的フォントキャッシュとGPUキャッシュの整合**: N64実機のTMEM制約に由来する固定メモリスロット再利用時に、vitaGL のテクスチャキャッシュを即座に破棄（無効化）する処理を追加し、文字化け（Stale Texture Cache Hit）を防止。
- **ROMローダーの拡張**: 日本版ROMヘッダーおよびカントリーコード `'J'` を正規ROMとして受け付けるように拡張。
- **ゲーム内容・機能の詳細について**: ゲーム内容、操作方法、レンダラーの最適化、機能等の詳細については、フォーク元リポジトリ（[kaziema/gevita](https://github.com/kaziema/gevita)）およびアップストリーム（[jkdansereau/goldeneye-pc-port](https://github.com/jkdansereau/goldeneye-pc-port)）を参照してください（今後のフォーク元のアップデート・エンハンスとの仕様乖離を防ぐため、本リポジトリでは重複した詳細説明は省略しています）。

---

## 導入手順 (PS Vita / 日本版ROM)

### 1. 前提条件 (Homebrew環境)
- **HENkaku / H-Encore** 等のCFWが導入されたPS Vita
- **[VitaShell](https://github.com/TheOfficialFloW/VitaShell)**
- **`libshacccg.suprx`**（ランタイムシェーダーコンパイラ）:
  - `ur0:data/libshacccg.suprx` に配置されている必要があります。

### 2. ROMファイルの準備と配置
- ご自身で所有・吸い出した正規の **Nintendo 64 日本版ROM**（`.z64` 形式）を用意します。
- PS Vitaのストレージに以下の固定パスで配置します：
  ```text
  ux0:data/GoldenEye007/ge007.jpn-final.z64
  ```
  ※ または `ux0:data/GoldenEye007/baserom.j.z64` でも認識されます。

### 3. VPKのインストール
- 本リポジトリの [Releases](https://github.com/Renge921/GoldenEyeVita/releases) から最新の `GE007Vita_JP.vpk` をダウンロードします。
- VitaShell（USB転送またはFTP）等でPS Vitaへ転送し、VitaShell上からインストールします。

### 4. 起動
- LiveAreaに追加されたバブルからゲームを起動してください。
※ 初回起動時は Vita 実機上で ROM からモデルやテクスチャの自動コンバートが行われるため、起動に少し時間がかかります。

---

## ビルド方法 (Building)

Prerequisites:
- [VitaSDK](https://vitasdk.org/)
- `vitaGL`, `vitaShaRK`, `math-neon`, `SDL2`, `zlib` (vdpm 経由で導入可能)

```sh
export VITASDK=$HOME/vitasdk
export PATH=$VITASDK/bin:$PATH

# 日本語版のビルド (GE007Vita_JP.vpk を生成)
make -f Makefile.vita all -j8

# 北米版のビルド (GE007Vita.vpk を生成)
make -f Makefile.vita REGION=u all -j8
```
---

## クレジット & ライセンス

- [kaziema/gevita](https://github.com/kaziema/gevita) (PS Vita Port)
- [jkdansereau/goldeneye-pc-port](https://github.com/jkdansereau/goldeneye-pc-port) (GoldenEye 007 PC Port)
- [n64decomp/007](https://github.com/n64decomp/007) (GoldenEye 007 Decompilation)
- ライセンス: MIT License (詳細は [LICENSE](LICENSE) を参照)

---

## 免責事項

- 本プロジェクトには、ゲームのROMデータ、テクスチャ、音声、BGM、3Dモデル等の著作権で保護されたアセットは一切含まれていません。
- 本ソフトウェアは個人利用および研究目的の非公式ファンプロジェクトであり、任天堂、レア社、その他権利者とは一切関係ありません。
