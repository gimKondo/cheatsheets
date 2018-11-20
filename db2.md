# DB2
## CUIコマンド
- SQLファイルを実行: `db2 -tvf ファイルパス`
    - t: ステートメント終了文字を設定
    - f: ファイルから入力
    - v: 現行コマンドをエコー

## CUIコマンド(インタラクティブモード)
- `db2` で開始
- コマンドオプション一覧: `list command options`
- DB一覧: `list db directory`
- DBに接続: `connect to DB名`
- テーブル一覧: `list tables`
- テーブル定義表示: `describe table テーブル名`
- 主キー確認: `select * from syscat.keycoluse where tabname = 'テーブル名'`
- インデクス確認: `select tabname, indname, colnames from syscat.indexes where tabname = 'テーブル名'`
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
