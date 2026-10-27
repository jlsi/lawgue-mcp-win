# eMudhra 信頼ルート修正の配布確認（2026-10-27）

対象: `jlsi/lawgue-mcp-win`。関連: https://github.com/jlsi/fraim.dev/issues/49

旧配布は **3.2.7 / Elsa 2.53.14** で、依存記録は webpki-roots 1.0.8 / rustls-webpki 0.103.13 でした。
この変更は **プラグイン 3.2.8 / Elsa 2.55.12** に更新します。
この PR のマージ前に、既存の配布先が修正済みになったとは扱いません。

## 成果物の対応

- 公式リリース: https://github.com/jlsi/elsa/releases/tag/2.55.12
- ソース commit: `55de35ba4b2e95051f9fe570273c1bdb982bb361`
- release イベントのビルド: https://github.com/jlsi/elsa/actions/runs/40272500815（成功、head SHA と tag の commit が一致）
- 配布アーカイブ: https://github.com/jlsi/elsa/releases/download/2.55.12/elsa-headless-mcp-x86_64-pc-windows-msvc.zip
- アーカイブ SHA-256: `998ad0e5ba0a1b42729d8cca12e967a772437cfadb785640a071c48aa8e5a89d`（公式 `.sha256` / GitHub asset digest と一致）
- 同梱実行ファイル SHA-256: `1e78276a0625b9a057df6ff2aacc838cb6b2d7f6ca328f561384ea8c6ab44216`（展開した公式成果物と一致、再ビルド・改変なし）

ソースの `Cargo.lock` と両対象の `cargo tree --locked -p elsa-headless-mcp --target TARGET --prefix none`
で **webpki-roots 1.0.10 / rustls-webpki 0.103.16** を確認しました。
Windows release job のコンパイルログでも同版を確認しています。
現在の依存一覧・ソース checksum・ライセンス原文の対応を `BUILD_DEPENDENCIES.json` に更新しました。
対象別 311 (macOS arm64) / 313 (Windows x64)、合計 315 パッケージで、hlink / d1sys は含みません。

## 動作・同梱物の確認

- macOS arm64 成果物をローカルで起動し initialize / tools/list が成功。31 ツールを確認。
- chunk_document / find_references / resolve_references / check_law_names / open_docx /
  open_docx_from_url / export_docx_to_url / fetch_docx_to_file / upload_docx_file が存在し、find_law_links は不在。
- Windows は release CI の署名後の initialize / tools/list と static CRT 検査が成功。
- Windows Authenticode は `Valid`、署名者 FRAIM Inc.、GlobalSign タイムスタンプを release job のログで確認。
- macOS は Developer ID 未署名・未公証（公式 SIGNING.txt を保持）。署名済みとは扱わない。
- 両実行ファイルに含まれる圧縮 IPADIC は、同 commit の元 IPADIC 再生成物とバイト単位で一致。
  その PROVENANCE / NOTICE / COPYING を保持。

TLS 接続の失敗だけを証明書拒否の実証とは扱っていません。本記録は公式成果物と修正版依存の対応の確認です。
利用権が必要な文書操作全体の本番認証テストは、このローカル smoke test に含みません。
マージ後に配布先の main commit・プラグイン版・同梱 SHA-256 を再確認し、issue #49 の配布完了チェックを更新してください。
