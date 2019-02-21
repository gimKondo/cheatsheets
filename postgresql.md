# PostgreSQL
## コマンドラインツール(psql)
### 引数
- データベース一覧: `psql -l`

### コマンド
- データベース一覧: `\l`
- テーブル一覧(viewやsequenceも含む): `\d`
- テーブル一覧: `\dt`
- フィールド一覧: `\d [テーブル名]`
- SQLファイル実行: `\i [SQLファイル名]`
- 終了: `\q`

### ページャ
- 切替: `¥pset pager`
- 有効／無効切替: `¥pset pager on` / `¥pset pager off`
