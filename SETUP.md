# LAWGUE MCP のセットアップ — Windows x86_64

ご利用条件については、[LAWGUE 利用規約](https://lawgue.com/terms/)をご参照ください。

接続先: **production（本番環境）**。

Windows x64 版は C/C++ ランタイムを静的リンクしています。
Microsoft Visual C++ Redistributable の追加インストールは不要です。

## 1. Remote コネクタを登録する

Claude の個人設定では `Customize → Connectors` からカスタムコネクタを追加します。
組織では登録権限を持つ管理者が `Organization settings → Connectors` から追加します。

| 項目 | 値 |
| --- | --- |
| 名前（例） | LAWGUE |
| URL | `https://api.lawgue.com/mcp` |
| OAuth Client ID | `579ca0est193bdhvh0b9qp1uvt` |
| OAuth Client Secret | 空欄 |

認証を伴う接続を選び、OAuth client の選択で `Use your own OAuth client` を選択して
上記 Client ID を指定します。旧画面の `Advanced settings` でも同じ値を使います。
Client ID は公開クライアントの識別子です。Client Secret は配布も入力も不要です。
URL と Client ID は同じ環境の組み合わせを使ってください。

URL だけで登録して認証に失敗する場合は、削除して上記の設定で登録し直します。
各利用者は自分の LAWGUE アカウントで接続します。Tool permissions は組織の方針に従い、
更新・保存操作を利用者が承認できる設定にします。この設定は LAWGUE 側の権限を広げません。
[Remote コネクタの公式手順](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp)
も確認してください。画面や設定可能な項目はプラン・権限・アプリ版によって異なります。

## 2. Local プラグインを Claude Code に導入する

```sh
claude plugin marketplace add jlsi/lawgue-mcp-win
claude plugin install lawgue-mcp@lawgue-mcp-win --scope user
```

プラグイン名は `lawgue-mcp`、Local MCP の名前は `lawgue-jade` です。
反映の案内に従って `/reload-plugins` または Claude Code の再起動を行い、
`/mcp` で Local の `lawgue-jade` と Remote の LAWGUE ツールを確認します。

### Claude Code で Remote が表示されない場合

カスタムコネクタ経由で既に Remote が表示されている場合、この登録は不要です。
CLI で直接接続する場合は次を実行します。

```sh
claude mcp add --scope user --transport http --client-id 579ca0est193bdhvh0b9qp1uvt --callback-port 40342 lawgue https://api.lawgue.com/mcp
claude mcp login lawgue
```

40342 番ポートが利用可能であることを確認してください。組織ポリシーによっては管理者の
設定が必要です。認証に失敗する場合は、Client ID、環境、Claude Code の版を確認します。
[CLI の OAuth 設定](https://code.claude.com/docs/en/mcp) を参照してください。

## 3. 検証用文書で確認する

組織で用意した検証用文書の名前・プロジェクトを指定して検索し、対象を確認して開きます。
小さな変更を依頼し、保存前の差分を確認してから保存を承認します。LAWGUE 側でも
保存結果を確認してください。既存の契約書を検索結果の先頭という理由だけで選ばないでください。

Desktop のチャットで使う場合の `.mcpb` 導入手順とトラブルシューティングは
[setup-guide.html](setup-guide.html) にあります。本リポジトリに `.mcpb` は同梱されていません。
