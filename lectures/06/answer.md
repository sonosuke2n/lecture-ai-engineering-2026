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
  app/mcp_server.py に `server.tool()(tools.get_lecture_summary)` を追加し、講義の概要を取得する関数をMCPツールとして公開しました。宿題では、app/mcp_agent.py と app/mcp_servers.json は変更していません。

- 結果：
  「第2回では何を学びますか？」と質問すると、追加したツールが呼ばれ、第2回の「ファインチューニングとLoRA」に関する情報が返りました。最終回答にも、その内容が反映されていました。モデル応答は2回でした。

```text
[tool call] glossary_get_lecture_summary({'lecture': 2})
```

  `uv run pytest -q` を実行し、21件すべてのテストが通過しました。

```text
21 passed in 4.81s
```

- 気づき・疑問：
  エージェントは起動時にMCPサーバーからツール一覧を取得するため、サーバー側に登録するだけで、エージェント側を変更せずに新しいツールを使えることが分かりました。また、traceでツールの呼び出しと返り値を確認することで、追加した機能が実際に使われたかを確かめられると理解しました。