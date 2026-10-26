# Toolchain / native runtime notices

確認日: 2026-10-27。Cargo 依存物の表示に加え、実行ファイルを生成した toolchain と
動的リンク先を確認しました。これはリンクされたコードだけを列挙した SBOM ではありません。

## Rust 標準ライブラリ

Elsa 2.55.12 の配布 workflow は Rust `1.99.0` を指定しています。
`rustc 1.99.0 (b940084d7 2026-09-28)`、commit `b940084d7eb6a299eb4bfeb8e34901bc051e7ac4` の
公式 rustup toolchain が配布する標準ライブラリの著作権・ライセンス表示を、改変せず収録しています。

- [COPYRIGHT-library.html](COPYRIGHT-library.html): 標準ライブラリとその依存物の著作権・条件全文。
  SHA-256: `5647be074c8edf7339fd863055923a8fc80bc5610a8d4661ec3b767b9d392c27`。
- [Apache-2.0](licenses/Apache-2.0.txt)、[MIT](licenses/MIT.txt)、
  [LLVM exception](licenses/LLVM-exception.txt)、[Unicode-3.0](licenses/Unicode-3.0.txt)、
  [NCSA](licenses/NCSA.txt)、[ISC](licenses/ISC.txt)、[BSD-2-Clause](licenses/BSD-2-Clause.txt): 同 toolchain のライセンス原文。

取得元: Rust 1.99.0 公式 rustup 配布物の `share/doc/rust/COPYRIGHT-library.html` と `share/doc/rust/licenses/`。
原文は複数ターゲットの標準ライブラリを含み、全項目が本実行ファイルにリンクされているという意味ではありません。
[Rust の著作権表示の説明](https://github.com/rust-lang/rust/blob/1.99.0/COPYRIGHT)
も参照してください。

## Windows の C/C++ ランタイム

配布する 2.55.12 x64 EXE は C/C++ ランタイムを静的リンクしています。
最終 EXE の通常・遅延読み込みの DLL 依存を確認し、VCRUNTIME / MSVCP / UCRT DLL
への依存がないことを確認しました。Microsoft Visual C++ Redistributable の追加導入は不要です。

動的リンク先は Windows の kernel32 / ntdll / ws2_32 / bcrypt / bcryptprimitives / advapi32 /
api-ms-win-core-synch です。配布 ZIP は署名済み EXE 1 個のみで、runtime DLL や
Visual C++ Redistributable のインストーラーは同梱していません。

静的リンクしたランタイムの修正は、実行ファイルの更新で反映されます。
