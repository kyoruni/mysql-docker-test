# kyoruni/mysql-docker-test

## 起動方法

```bash
$ docker compose up -d
```

## MySQL を使うには

```bash
$ docker compose exec mysql bash

mysql -u root -p # root
```

## 初期データを入れたい場合

- 任意の sql ファイルを `compose.yaml` の `volumes` で、 `/docker-entrypoint-initdb.d` 内にマウントする
  - 例： [MySQL :: Other MySQL Documentation](https://dev.mysql.com/doc/index-other.html) からダウンロードした `world database` を使う場合

```yaml
# 例（ sql が sample 配下にある場合 ）
./sample/world.sql:/docker-entrypoint-initdb.d/world.sql
```

- データベースがあると実行されない
- データベースを丸ごと削除するには以下を実行する

```bash
# mysql-docker-test_db-data があることを確認
$ docker volume ls

# ボリューム削除(テーブル内のデータも全部消えるので注意)
docker volume rm mysql-docker-test_db-data
```