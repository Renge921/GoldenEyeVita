# GoldenEye 007: PS Vita Port (Japanese ROM Support Fork)

![license](https://img.shields.io/badge/license-MIT-green)
![platform](https://img.shields.io/badge/platform-PS%20Vita-blue)

本リポジトリは、kaziema 氏による GoldenEye 007 PS Vita ネイティブ移植版（[kaziema/gevita](https://github.com/kaziema/gevita)）のフォークです。

元のプロジェクトでは未対応だった **日本語版ROM（NTSC-J）に対応** し、PS Vita 実機上で日本語版『ゴールデンアイ 007』のブリーフィング、メニュー、日本語フォントを正常に描画・プレイできるようにしたバージョンです。

> [!NOTE]
> ゲーム内容、操作方法、レンダラーの最適化、機能や更新履歴の詳細については、フォーク元のリポジトリ [kaziema/gevita](https://github.com/kaziema/gevita) をご参照ください。

---

## 必要環境 (Requirements)

ご自身で吸い出した以下のいずれかの N64 ROM（ビッグエンディアン `.z64` 形式）が必要です。

| バージョン | ROMファイル名 (`ux0:data/GoldenEye007/` 配下に配置) | SHA-1 チェックサム |
|---|---|---|
| **日本語版 (NTSC-J)** | `ge007.jpn-final.z64` または `baserom.j.z64` | `2a5dade32f7fad6c73c659d2026994632c1b3174` |
| **北米版 (NTSC-U)** | `ge007.ntsc-final.z64` または `baserom.u.z64` | `abe01e4aeb033b6c0836819f549c791b26cfde83` |

※ 本リポジトリおよび配布 VPK には任天堂やRareのROMデータ・著作権アセットは一切含まれていません。

---

## インストール手順 (Installation)

1. HENkaku / VitaShell が導入された PS Vita を用意します。
2. VitaShell で `ux0:data/` を開き、新規フォルダ `GoldenEye007` を作成します（`ux0:data/GoldenEye007/`）。
3. 作成したフォルダ内に以下2つのファイルを転送します：
   - `GE007Vita_JP.vpk`（日本語版）または `GE007Vita.vpk`（US版）
   - 上記の要件を満たすご自身の ROM ファイル（例: `ge007.jpn-final.z64`）
4. VitaShell で VPK を選択してインストールします（拡張権限プロンプトを承認）。
5. LiveArea から起動します。
   - ※ 初回起動時は Vita 実機上で ROM からモデルやテクスチャの自動コンバートが行われるため、起動に少し時間がかかります。

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

## 本フォークでの主な変更点

- **日本語版ROMアセット抽出の修正**: 上流 CSV（`scripts/filelist.j.csv`）のタイポを修正し、日本語版アセットシンボル（`port/src/romassets_j.s`）を正常生成。
- **実機アセットコンバータの拡張**: `tools_pc/gen_pcconv_tables.py` および `port/src/pcconv_tables.c` を更新し、日本版ROMのモデル・CG・セットアップをVita実機上で正しく抽出・変換可能に修正。
- **動的フォントキャッシュとGPUキャッシュの整合**: N64実機のTMEM制約に由来する固定メモリスロット再利用時に、vitaGL のテクスチャキャッシュを即座に破棄（無効化）する処理を追加し、文字化け（Stale Texture Cache Hit）を防止。
- **ROMローダーの拡張**: 日本版ROMヘッダーおよびカントリーコード `'J'` を正規ROMとして受け付けるように拡張。

---

## クレジット & ライセンス

- [kaziema/gevita](https://github.com/kaziema/gevita) (PS Vita Port)
- [jkdansereau/goldeneye-pc-port](https://github.com/jkdansereau/goldeneye-pc-port) (GoldenEye 007 PC Port)
- [n64decomp/007](https://github.com/n64decomp/007) (GoldenEye 007 Decompilation)
- ライセンス: MIT License (詳細は [LICENSE](LICENSE) を参照)
