# 第6回 解答

## 演習

- STEP 1 のツールの名前：
  - 従来のエージェント：`search_materials`
  - MCPを使うエージェント：`glossary_search_glossary`

- STEP 2 の [tool call]：

```text
[tool call] glossary_search_glossary({'query': '3レベル'})
```

- STEP 3 の [tool call]：

```text
[tool call] fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
```

- STEP 4 の [tool call]：

```text
[tool call] aws_aws___search_documentation({'search_phrase': 'Amazon S3 バージョニング 概要', 'topics': ['general']})
[tool call] aws_aws___search_documentation({'search_phrase': 'Using versioning Amazon S3', 'topics': ['general']})
```

- 気づき・疑問：
  MCPを使う場合も、モデルにはツールの名前・説明文・引数が渡されることを確認しました。また、設定ファイルに接続先を追加することで、エージェント本体を変更せずに新しいツールを利用できることが分かりました。fetchは自分のCodespaces内で起動し、AWSのサーバーにはURLで接続するという違いも理解しました。回答だけでなく、traceで実際のツール呼び出しと返り値を確認することが大切だと感じました。

## 宿題

- 取り組んだレベル：基礎
- やったこと：
- 結果：
- 気づき・疑問：