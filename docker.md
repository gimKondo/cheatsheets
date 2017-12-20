# Docker
- 参考: https://qiita.com/curseoff/items/a9e64ad01d673abb6866

## イメージ
- イメージ一覧: `docker images`
- イメージ構築: `docker build .`
    - カレントディレクトリにDockerfileがあること前提
- イメージ構築(タグ付き): `docker build -t TAG_NAME .`
- イメージ構築(最初から): `docker build . --no-cache`
- イメージ削除: `docker rmi IMAGE`

## コンテナ
- コンテナ一覧: `docker ps`
- コンテナ一覧(停止中を含む): `docker ps -a`
- コンテナ削除: `docker rm CONTAINER`
- コンテナ全削除: `docker rm $(docker ps -aq)`
- コンテナ作成: `docker create IMAGE`
- コンテナ作成(名前付き): `docker create --name NAME IMAGE`
- コンテナ起動: `docker start CONTAINER`
- コンテナ停止: `docker stop CONTAINER`
- コンテナ再起動: `docker restart CONTAINER`
- イメージからコンテナを起動: `docker run IMAGE`
    - 名前付き: `docker run --name NAME IMAGE`
    - バックグラウンド: `docker run -d IMAGE`
    - ポート転送: `docker run -p HOST_PORT:CONTAINER_PORT IMAGE`

## docker-compose
- 起動: `docker-compose start`
- 停止: `docker-compose stop`
- ビルドから起動まで全部: `docker-compose up`
- バッシュを起動:  `docker-compose run CONTAINER bash`
