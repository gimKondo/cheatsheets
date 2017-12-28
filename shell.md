# シェルチートシート
## コマンド
- rm
	- ドットファイルの削除: `rm -rf trgDir/.*`
		- ワイルドカードだけ(`rm -rf trgDir/*`)では削除されない
- find
    - パターンに合致する名前のファイル、ディレクトリを列挙: `find [検索パス] -name [パターン]`
        - 例: カレントディレクトリ配下のcファイル `find . -name *.c`
    - ファイルのみ: `find [検索パス] -name [パターン] -type f`
        - ディレクトリのみの場合は`-type d`
- zip圧縮
	- ファイルを圧縮: `zip アーカイブ名 対象ファイル名...`
	- ディレクトリを圧縮: `zip アーカイブ名 -r ディレクトリ名`
	- パスワードを付けて圧縮: `zip -e アーカイブ名 対象ファイル名...`
- zip解凍: `unzip アーカイブ名`
- tar
    - アーカイブ: `tar cvf tarファイル名 アーカイブ対象ディレクトリ`
    - 圧縮してアーカイブ: `tar cvzf tgzファイル名 圧縮対象ディレクトリ`
    - 解凍して展開: `tar xvzf tgzファイル名`
    - 特定のファイルのみ解凍して展開: `tar xvzf tgzファイル名 ファイルパス`
    - アーカイブされているファイルの一覧: `tar tf tarファイル名`
    - 圧縮してアーカイブされているファイルの一覧: `tar tzf tgzファイル名`
    - オプションの補足
        - f: 'f'ile
            - fはファイル名指定の直前に必要なので、だいたいオプションの最後になる
        - c: 'c'reate
        - t: lis't'
        - x: e'x'tract
        - z: g'z'ipの圧縮／展開
- ディレクトリ移動
    - ディレクトリ位置の記憶: `pushd`
        - zshで`setopt auto_pushd`と設定していると、移動中のディレクトリがすべて記憶される
    - 記憶したディレクトリに戻る: `popd`
    - 記憶したディレクトリ一覧: `dirs`
- ディスク容量
	- `df -h`
- ファイル容量
	- バイト単位: `du -h`
	- 直下ディレクトリのみ: `du -hs`
	- 対象のディレクトリのみ: `du -hs ディレクトリ名`

## 操作
- Ctrl-u
    - 直前の入力をクリア
    - パスワード入力プロンプトでのミスもクリアできる
- cd -
    - 前のディレクトリに戻る

## curl
- HEADリクエスト
    - `curl -I http://example.com`
- レスポンスとレスポンスヘッダの両方を表示
    - `curl -i http://example.com`
- リクエストヘッダを変更して送信
    - `curl -H 'Origin:http://example.com' http://example.com`
    - `curl -H 'Origin:http://example.com' -H 'Content-Type:text/html' http://example.com`
    - 良く使うものは個別オプションあり
        - User-Agent: `-A / --user-agent`
        - Referer: `-e / --referer`
        - Cookie: `-b / --cookie`
- メソッドを指定する
    - `curl -X POST http://example.com`
        - データを送信: `curl -X POST -d "hoge=0&fuga=1" http://example.com`
        - データ(ファイル)を送信: `curl -X POST -d @hoge.json http://example.com`
    - `curl -X OPTIONS -H "Origin:http://example.com" -H "Access-Control-Request-Method:GET"  http://example.com`
        - プリフライトのOPTIONSを送信するならこんな感じになる
    - 参考: http://takuya-1st.hatenablog.jp/entry/2017/03/07/210319
        - ここに書かれてる方法は上記とちょっと違うものもある

## sed
### 大文字小文字変換(GNU拡張前提)
- 小文字→大文字: `sed -E "s/(.*)/\U\1/"`
- 大文字→小文字: `sed -E "s/(.*)/\L\1/"`
- 先頭のみ大文字: `sed -E "s/(.)(.*)/\U\1\L\1/"`

### キャメルケース・スネークケース変換
- ローワーキャメルケース → スネークケース: `sed -r 's/([A-Z])/_\L\1\E/g'`
- アッパーキャメルケース → スネークケース: `sed -r -e 's/^([A-Z])/\L\1\E/' -e 's/([A-Z])/_\L\1\E/g'`
- スネークケース → ローワーキャメルケース: `sed -r 's/_(.)/\U\1\E/g'`
- スネークケース → アッパーキャメルケース: `sed -r 's/(^|_)(.)/\U\2\E/g'`

## 変数参照
- http://shellscript.sunone.me/variable.html
- ${VAR=aaa}
	- 変数 VAR が未使用の場合に限り、変数VARへ文字列「aaa」を代入し文字列「aaa」を返す。
	- 変数VARがNULL値を含み既に使用されている場合は、変数 VAR への代入を行わず、変数 VAR の値を返す。
- ${VAR:=aaa}
	- 変数 VAR が未使用もしくは NULL の場合に限り、変数 VAR へ文字列「aaa」を代入し文字列「aaa」を返す。
	- 変数 VAR が NULL 値の場合を除き、既に使用されている場合は変数 VAR への代入を行わず、変数 VAR の値を返す。
- ${VAR-aaa}
	- 変数 VAR が未使用の場合に限り、文字列「aaa」を返す。
	- 変数 VAR が NULL 値を含み既に使用されている場合は、変数 VAR の値を返す。
	- また、変数 VAR が使用済み・未使用に関わらず、変数 VAR への代入は行われない。
- ${VAR:-aaa}
	- 変数 VAR が未使用もしくは NULL 値の場合に限り、文字列「aaa」を返す。
	- 変数 VAR が NULL 値以外の値で既に使用されている場合は、変数 VAR の値を返す。
	- また、変数 VAR が使用済み・未使用に関わらず、変数 VAR への代入は行われない。
- ${VAR+aaa}
	- 変数 VAR が NULL 値も含み既に使用されている場合に限り、文字列「aaa」を返す。
	- 変数 VAR が未使用の場合は、NULL 値を返す。
	- また、変数 VAR が使用済み・未使用に関わらず、変数 VAR への代入は行われない。
- ${VAR:+aaa}
	- 変数 VAR が NULL 値以外で既に使用されている場合に限り、文字列「aaa」を返す。
	- 変数 VAR が NULL 値もしくは未使用の場合は、NULL 値を返す。
	- また、変数 VAR が使用済み・未使用に関わらず、変数 VAR への代入は行われない。
