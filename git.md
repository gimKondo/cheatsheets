# Gitチートシート
## diff
- 改行コード無視: `git diff -w`
- スペースを無視: `git diff -b` / `git diff --ignore-space-change`
- ファイル名のみを見る: `git diff --name-only`

## show(コミット閲覧)
- 基本: `git show <commit id>`
- ファイル名のみ: `git show <commit id> --name-only`
	- 実際にはコミットIDやAuthorなどの情報も表示される(diffは出ない)。

## status
- short-format表記
	`git status -s`
- ブランチ名表示
 	`git status -b`
- 追跡していないディレクトリの中身も表示
	`git status -uall`
- 追跡していないファイルは無視
	`git status -uno`

## ログ
- ファイル名のみを見る
	`git log --name-only`
- コミットメッセージを検索してログ表示
	`git log --grep hogehoge`
- コミットの差分を検索してログ表示
	`git log -S"hogehoge" [filepath]`
- マージコミットのみ
	`git log --merges`
- マージコミットを除く
	`git log --no-merges`
- マージコミットのマージ元を非表示
	`git log --first-parent`
- ブランチ間のコミット差分を表示
    - `git log --no-merges [比較元ブランチ名]..[比較先ブランチ名]`
    - カレントブランチと比較: `git log --no-merges ..[比較先ブランチ名]`

## タグ
- 一覧: `git tag`
- 検索: `git tag -l 'v1.*'`
- 注釈付きタグ: `git tag -a v1.3 -m 'this is a tag'`
- 軽量タグ: `git tag v1.4`
- タグのコミットを閲覧: `git show v1.3`
- 後からタグ付け: `git tag -a v1.5 -m 'important change' 9fceb02`
- タグの共有(特定のタグ): `git push origin v1.5`
- タグの共有(すべてのタグ): `git push origin --tags`
- タグの削除: `git tag -d TAG_NAME`
- タグのリモートからの削除: `git push --delete origin TAG_NAME` ／ `git push origin :TAG_NAME`
- タグにチェックアウト
    - ブランチを作る場合: `git checkout -b BRANCH_NAME refs/tags/TAG_NAME`
    - ブランチを作らない場合: `git checkout refs/tags/TAG_NAME`

## コミット
- authorを一時的に指定: `git commit --author='John Smith <john@example.com>'`

## マージ
- コミットなしでマージ(※ブランチ側のコミットを残す版)
	`git merge -no-commit branch_name`
- コミットなしでマージ(※ブランチ側のコミットを残さない版)
	`git merge --squash branch_name`
- マージの取り消し(直前のコミットまでリセットしてるだけ)
	`git reset --hard ORIG_HEAD`
- マージの中止(`branch名|MERGING`となってるときに中止)
    `git merge --abort`

## ブランチ
- ブランチ名変更(カレントブランチを変更)
	`git branch -m <変更後ブランチ名>`
- リモートブランチ削除(対象がoriginの場合)
	- `git push origin :<ブランチ名>`
        - 補足: 直訳的に解説すると、空を`<ブランチ名>`に置き換える、という感じ
    - `git push --delete origin <ブランチ名>`
        - こっちの方が明示的で分かりやすいかも

## スタッシュ
- unstageファイルをスタッシュ
	`git stash -k`
- unstageファイルも含めてすべてスタッシュ
	`git stash -u`
- スタッシュの一覧
	`git stash list`
- スタッシュのdiff表示
	`git stash show -v`
- メッセージ付きスタッシュの保存
	`git stash save "message"`
- 指定のスタッシュの取得(スタッシュリストから削除する)
	`git stash pop stash@{n}`
- 指定のスタッシュの取得(スタッシュリストから削除しない)
	`git stash apply stash@{n}`
- スタッシュの1件削除
    `git stash drop` # 最新を削除
    `git stash drop stash@{n}` # N番目を削除
- スタッシュの全削除
    `git stash clear`

## add
- 更新ファイルのみadd
	- `git add -u`

## config
- どのファイルで設定されているか確認
    - `git config --show-origin -l`
- 特定のリポジトリのみでname, emailを変更
    - `git config --local user.name 名前`
    - `git config --local user.email "メールアドレス"`

## clone
### cloneでこんなエラーが出たときの対処
- 参考: https://qiita.com/cacahuatl/items/4d763e98f3934e3569ca
```
fatal: early EOF
fatal: The remote end hung up unexpectedly
fatal: index-pack failed
```

- 通信制限の緩和: `git config --global http.postBuffer 524288000`
- サーバ側の整理
```sh
        git gc
        git repack -a -f -d --window=250 --depth=250
```

- cloneを小分けにする
```sh
        git clone --depth 1 <my_repo_URI>
        git fetch --unshallow
        # unshallowで一度にやるのではなく、以下のようにさらに小分けしても良い
        git fetch --depth 2
        git fetch --depth 3
        git fetch --unshallow
```

## remote
- httpsでクローンしたリポジトリをsshでpush/pullするように変更
- 確認: リモートリポジトリがhttpsで指定されている
```
> git remote -v
origin  https://github.com/gimKondo/cheatsheets.git (fetch)
origin  https://github.com/gimKondo/cheatsheets.git (push)
```
- sshでの指定に変更
    - `git remote set-url origin git@github.com:gimKondo/cheatsheets.git`
- 確認: sshで指定されるようになっている
```
> git remote -v
origin  git@github.com:gimKondo/cheatsheets.git (fetch)
origin  git@github.com:gimKondo/cheatsheets.git (push)
```

## 設定
- 環境内すべてのリポジトリに適用したいignore
    - `~/.config/git/ignore` に.gitignoreと同じ形式で記述

## その他
- コミットなしでチェリーピック
	`git cherry-pick -n <hash>`

## ユーザ定義コマンド
### git now(mzp版) : https://gist.github.com/mzp/1127078
- `--all`   : トラッキングしていないファイルもnow
- `--fixup` : nowをまとめる
- `--rebase`: nowをrebase(通常は--fixupで十分だが)

