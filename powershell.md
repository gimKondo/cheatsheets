
## コマンド
- Get-Help : ヘルプを表示
	- 事前に管理者権限でupdate-helpが必要
	- help / man : 似たコマンドだが、moreにパイプするっぽい。
		- なんだけど、moreがなんか上手く動かない(ページングできない・・・なんで？)
- Select-String / sls : grep相当
	- 否定検索: `sls -NotMatch hello`
	- 大文字・小文字の区別: -CaseSensitive
	- 正規表現を使わない: -SimpleMatch
		- デフォルトで正規表現
	- 行数: -Context 行数
		- マッチ行の前後「行数」分を表示
	- 文字コード: -Encoding 文字エンコーディング名
- Out-String -stream / oss : 標準出力にリアルタイムで出す
	- コマンドレットの結果などの一部はシェルに表示される内容と標準出力される内容が異なるものがある
		- 例: エイリアス一覧を出す`alias`、コマンド一覧を出す`get-command`
	- この結果、パイプに渡してgrepが上手くいかない。
	- こんなときにossを使う。
		- 例: `get-command -Command Function | oss | sls write`
		- これはFunction型のコマンドのうち、writeが含まれるものを一覧する。
- Write-Host
	- 色を付ける
		- 例:赤のテキストを出力 `Write-Host "hoge" -ForegroundColor Red`

## 自作コマンド
- PrintAppendedText / tail : `tail -f` っぽいもの

## レシピ
- カレントディレクトリ以下の全てのファイルから検索、ただし*.exeと*.binは除く
	- http://tech.sanwasystem.com/entry/2016/07/05/185717
	- `Select-String "pattern" (dir -recurse *.* -Exclude *.exe, *.bin)`
	- 別解: `dir -recurse *.* -Exclude *.exe, *.bin | Select-String "pattern"`
