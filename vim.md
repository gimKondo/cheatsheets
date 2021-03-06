# vimチートシート
## キーマップ
### ノーマルモード
- 変更履歴を辿る
	- g; : 戻る
	- g, : 進む
- gi : 最後に入力した場所で挿入モードを開始
- ( / ) : 文単位で戻る/進む
- { / } : 段落単位で戻る/進む
- C-w C-z or C-w z: プレビューウィンドウを閉じる
### コマンドモード
- C-r " : ペースト
### 挿入モード
- C-r = [式] : 式の結果を現在の位置に挿入

## コマンド
### タブ
- 複製: `:tab sp`
### 置換
- 区間
	- 10,50s/aaaa/bbbb/g : 10行目～50行目の置換
	- 10,$s/aaaa/bbbb/g : 10行目～最終行の置換
### 文字コード関連
- 文字コードを指定して開き直す
	- 例: `:e ++enc=utf8`
- 改行コードを指定して開き直す
	- 例: `:e ++ff=unix`

## その他の組み込み機能
### タグジャンプ
- Ctagsでtagsファイルを生成してあることが前提
- コマンド
    - 移動経路一覧: `:tags`
    - 指定単語の定義にジャンプ: `:tag [単語]`
    - 指定単語の定義をプレビューウィンドウで開く: `:ptag [単語]`
- ジャンプ系キーマップ
    - C-] : カーソル位置の定義にジャンプ(ビジュアルモード可)
    - g C-] : カーソル位置の定義にジャンプ(複数ある場合は選択・ビジュアルモード可)
    - C-w ] : カーソル位置の定義を分割ウィンドウで開く
    - C-w } : カーソル位置の定義をプレビューウィンドウで開く
- C-t : 戻る

### 連番作成
- 複数行の数値を矩形選択して`g C-a`
    - 数値付き箇条書きを作るのに便利

### 引数リスト
- 引数リストの作成
	- `:args ファイルパス`
		- ファイルパスにはワイルドカードが使える
		- 例: `:args ./**/*.txt`
- 一括置換
	- `:argdo %s/置換対象の文字列/置換後の文字列/g | update`
- 一括文字コード変換
	- `:argdo set fenc=utf-8 | update`
### モードライン
- シェル風のコメントと組み合わせる
	- `# vim: set expandtab fenc=cp932 ff=unix ft=shell`
- C言語風のコメントと組み合わせる
	- `/* vim: set expandtab fenc=cp932 ff=unix ft=shell : */`

## プラグイン
### ctrlp
- C-p C-p : ctrlpを起動
- C-p中の入力操作
    - C-k / C-j : カーソルを上／下へ
    - C-a / C-e : カーソルを先頭／末尾へ
    - C-u : 入力をクリア
    - C-d : フルパス or ファイル名の検索モード切り替え
    - C-r : 正規表現 or 通常の検索モード切り替え
    - C-f / C-b : 検索対象切り替え(ファイル、バッファ、最近使ったファイルなど)
- C-p中のファイル操作
    - Enter : 現在のウィンドウで開く
    - C-t : 新しいタブで開く
    - C-v : 垂直分割ウィンドウで開く
    - C-o : 開き方を選択して開く
- 独自キーマップ設定
    - C-p C-s: 対象に全部込みでctrlpを起動(だいたいコレでOK)
    - C-p C-b: バッファを対象としてctrlpを起動
    - C-p C-d: ディレクトリを対象としてctrlpを起動
    - C-p C-m: 最近使ったファイルを対象としてctrlpを起動
    - C-p C-l: カレントバッファの行を対象としてctrlpを起動
    - C-p C-t: タグを対象としてctrlpを起動

### vim-migemo
- ローマ字検索
	- `:Migemo [ローマ字]`
	- `<Leader>mi`
- Kaoriya版で `g/[ローマ字]` でやるようなインクリメンタル検索は今のところ無理

### vim-abolish
- 語彙
	- c: camelCase
	- m: MixedCase
	- _: snake_case
	- u: SNAKE_UPPERCAE
- 例
	- アッパースネークヘ変換 "cru"
	- キャメルケースへ変換 "crc"

### Agit
- Agitタブを開く: :Agit
- Agitタブを開く: q
- diff: di

### submode
- C-wでスタート
- サイズ調整: `+/-/</>`
- 移動: hjkl

### Ref
- K(Shift+K): カーソル単語をref
- 独自マッピング
	- \rr rubyのリファレンスの入力待ち
	- \re 和英の入力待ち
	- \rj 和英の入力待ち

### qfixgrep
- https://sites.google.com/site/fudist/Home/grep/usage
- g,e: grep
- g,re: 再帰検索grep
- g,f: 正規表現なしのgrep
- g,v: vimgrep
- g,b: buffer内grep
- QuickFix
	- C-w,: QuickFixのオープン/クローズ
	- C-w.: QuickFixへ移動
	- q: QuickFixのクローズ
	- i: プレビューON/OFF
	- I: プレビューのシンタクスハイライトON/OFF
	- S: ソート切替
	- s: 絞り込み検索
	- r: 絞り込み検索(否定)
	- u: ソート、絞り込みのアンドゥ
	- U: ソート、絞り込みのクリア

### dicwin.vim
- C-k C-k : カーソル下の単語を検索
- C-k /   : 入力した単語を検索
- C-k c   : ディクショナリウィンドウを閉じる
- C-k w   : ディクショナリウィンドウに移動
- C-k n/p : 次or前の単語に移動

