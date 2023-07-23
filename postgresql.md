以下のように `docker-compose.yaml` を作成する。

```yaml:docker-compose.yaml
version: '3.7'
services:
  posvar:
    image: postgres:15.3
    ports:
      - '5432:5432'
    # /docker-entrypoint-initdb.d 内のSQLが初期化時に実行されるのでマウントする
    # ref. https://hub.docker.com/_/postgres
    # :roはアクセスモード
    # ref. https://docs.docker.jp/v1.9/compose/compose-file.html#volumes-volume-driver
    volumes:
      - ./path/to/init/scripts:/docker-entrypoint-initdb.d:ro
    environment:
      - ./.env
```

`.env` を作成する。

```sh:.env
POSTGRES_PORT=5432
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=postgres
```
