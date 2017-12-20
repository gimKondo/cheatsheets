# Elixir
## Phoenix
### mix
#### 一般
- スクリプト実行: `mix run [スクリプトファイルのパス]`
- コード実行: `mix run -e "[コード]"`

#### test
- テスト実行: `mix test`
    - オプション等についてはこちらを参照: https://hexdocs.pm/mix/Mix.Tasks.Test.html
- ESpec(Phoenix前提)
    - テスト実行: `mix espec`
    - espec、espec_phoenixをmix.exsで導入
    - mix.exsのproject関数に`preferred_cli_env`を設定
        - こちらを参照: https://github.com/antonmi/espec
    - オプション
        - `--trace`: 詳細表示
        - `--order`: 記述順に実行？(通常はバラバラに非同期実行？)

#### DB周り
- モデルの生成: `phoenix.gen.model [モジュール名(キャメル・単数形)] [テーブル名(ローワースネーク・複数形)]`
- マイグレーションのやり直し: `ecto.reset`
    - 以下のコマンドと同等
        1. DB破棄: `ecto.drop`
        2. DB作成: `ecto.create`
        3. マイグレーションん実行: `ecto.migrate`
        4. 初期データ投入: `run priv/repo/seeds.exs`
