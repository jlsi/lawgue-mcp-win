# Third-party notices

このプラグインには `elsa-headless-mcp` を同梱しています。実行ファイルに組み込まれた
形態素解析辞書・法令名コーパスと第三者ソフトウェアの条件は、それぞれに適用されます。
今後の配布にも、このファイルと参照先の表示を含めてください。
JLSI のソフトウェアのご利用条件は、[LAWGUE 利用規約](https://lawgue.com/terms/)をご参照ください。
第三者ソフトウェアには、それぞれのライセンスが適用されます。

## Windows 実行ファイルの署名

同梱した実行ファイルは、Elsa 2.53.9 の正式リリースの署名済みバイナリです。
[配布 CI](https://github.com/jlsi/elsa/actions/runs/38332720801)で Authenticode が `Valid`、
署名者が FRAIM Inc.、GlobalSign のタイムスタンプがあること、および署名後の起動を確認しました。
取得元・SHA-256 は `BUILD_DEPENDENCIES.json` に記録しています。

## ビルドの依存物

[Elsa 2.53.9](https://github.com/jlsi/elsa/releases/tag/2.53.9)（ソース commit `1e4b93584832ab448c2dcebab18f5138d8305ef4`）の
[配布ビルド](https://github.com/jlsi/elsa/actions/runs/38332720801) に対応する
Cargo.lock と対象別 `cargo tree --locked -p elsa-headless-mcp` に基づく一覧です。
macOS arm64 は 285、Windows x64 は 292、重複を除いて 292 パッケージです。
ビルドツール・proc macro を含みます。リンクされたコードだけの SBOM ではありません。
hlink 系と d1sys はこの依存ツリーに含まれません。

- [BUILD_DEPENDENCIES.json](third-party/dependencies/BUILD_DEPENDENCIES.json): バージョン、宣言ライセンス、ソース入手先、crates.io checksum、対象 OS、表示原文の対応。
- [NOTICES.txt](third-party/dependencies/NOTICES.txt): ライセンス・著作権・NOTICE の原文。同一原文は SHA-256 でまとめています。

crates.io アーカイブは Cargo.lock の SHA-256 と照合しました。
パッケージに全文が入っていないものは、その Git revision の上流から取得しました。
emf-core / wmf-core のリポジトリルートの MIT LICENSE、delarocha 0.1.1 の MIT / Apache-2.0 全文、
ring / zstd-sys 等のパッケージ内の第三者表示も収録しています。
本ビルドの Cargo 依存ツリーに `zig-ffi` は含まれません。

## Toolchain / native runtime

Rust 標準ライブラリの著作権・ライセンス全文と、OS / MSVC runtime の確認結果は
[runtime の表示と配布範囲](third-party/runtime/README.md) に収録しています。
Rust 1.99.0 の公式表示を保持しています。Windows の runtime DLL / 再頒布インストーラー、
macOS の OS dylib は同梱せず、利用者の端末にあるものを参照します。

## UniFFI — MPL-2.0 のソース入手先

UniFFI 系 8 パッケージの使用版はすべて `0.30.0` です。
MPL-2.0 の全文は上記 NOTICES.txt に収録しています。
該当するソースコードは、追加の料金なく各パッケージの crates.io ソースアーカイブから入手できます。
以下のアーカイブと照合し、使用したローカルのソース全ファイルが未変更であることを確認しました。

| パッケージ | 使用版のソース |
| --- | --- |
| uniffi | [0.30.0](https://crates.io/api/v1/crates/uniffi/0.30.0/download) |
| uniffi_bindgen | [0.30.0](https://crates.io/api/v1/crates/uniffi_bindgen/0.30.0/download) |
| uniffi_core | [0.30.0](https://crates.io/api/v1/crates/uniffi_core/0.30.0/download) |
| uniffi_internal_macros | [0.30.0](https://crates.io/api/v1/crates/uniffi_internal_macros/0.30.0/download) |
| uniffi_macros | [0.30.0](https://crates.io/api/v1/crates/uniffi_macros/0.30.0/download) |
| uniffi_meta | [0.30.0](https://crates.io/api/v1/crates/uniffi_meta/0.30.0/download) |
| uniffi_pipeline | [0.30.0](https://crates.io/api/v1/crates/uniffi_pipeline/0.30.0/download) |
| uniffi_udl | [0.30.0](https://crates.io/api/v1/crates/uniffi_udl/0.30.0/download) |

上流の対応 revision は [mozilla/uniffi-rs 47cb437](https://github.com/mozilla/uniffi-rs/tree/47cb43774d7d4dc2fb13225fb95fb1eb24efa893) です。
本案内は MPL 対象ファイルのソース提供の案内であり、プラグイン全体を MPL で許諾するものではありません。

## MeCab / IPADIC 系辞書

同梱バイナリは、元の MeCab IPADIC `2.7.0-20070801` だけを入力として
Delarocha 形式へ変換した辞書を含みます。BCCWJ、Vibrato の加工済み辞書、
顧客文書、D1-Law データは生成入力に使いません。

- [COPYING](third-party/ipadic/COPYING): 元のライセンスのバイト列を保持。
- [COPYING.UTF-8](third-party/ipadic/COPYING.UTF-8): 同じ全文の文字コード変換版。
- [NOTICE](third-party/ipadic/NOTICE): 出典と加工内容。
- [PROVENANCE.json](third-party/ipadic/PROVENANCE.json): 原アーカイブ、生成物、ライセンスの SHA-256。
- [辞書の説明](third-party/ipadic/README.md): 生成方法と検証手順。

COPYING は NAIST の著作権表示と ICOT の免責を含み、原形・改変版の再配布時に
その全文を保持する条件です。本配布物には全文を収録しています。
元アーカイブと生成辞書のハッシュは上流の検証スクリプトで確認しました。
配布 EXE 内の圧縮辞書も、この PROVENANCE.json が示す生成物とバイト単位で一致します。

## 法令名コーパス — e-Gov

残る `check_law_names` の法令名コーパスについて、
[出典・加工表示](third-party/egov/NOTICE.md) を収録しています。
hlink による法令コードへの引用解決とは別の機能です。
D1-Law 由来の `00000.hlkd`、`hlk_config.json` および hlink は同梱しません。
`find_law_links` は提供していません。
