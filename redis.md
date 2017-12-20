# Redis
## CLI
- 全キー削除
    - 相当するコマンドは無く、シェルコマンドとの組み合わせ
    - `redis-cli keys "[パターン]" | xargs -d '\n' redis-cli del`
        - パターン
            - 全削除: `*`
            - abcから始まるキーを全削除: `abc*`
