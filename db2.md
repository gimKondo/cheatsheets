# DB2
## CUIコマンド
- DB一覧: `list db directory`
- DBに接続: `connect to DB名`
- テーブル一覧: `list tables`
- テーブル定義表示: `describe table テーブル名`
- エクスポート: `EXPORT TO /tmp/test.ixf OF 形式 MESSAGES /tmp/test.log SELECT * FROM xml_test`
    - 形式
        - DEL: CSV形式
        - ASC: 区切り文字なし
        - IXF: 型情報なども含むバイナリ形式
    - MESSAGESは省略可
- インポート: `IMPORT FROM /tmp/test.csv OF 形式 COMMITCOUNT n MESSAGES /tmp/test.log INSERT INTO xml_test`
    - 形式: エクスポート同様
    - MESSAGESは省略可
    - COMMITCOUNTはn個ごとにコミットするオプション(省略可)
- 終了: `quit`
