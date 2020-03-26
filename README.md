CSV Visualizer by Metabase
====

CSVファイルをMetabaseで可視化する

## Description
- 「[Metabase](https://www.metabase.com/)」と「PostgreSQL」をDockerで環境構築する
- CSVファイルから[ddlgenerator](https://github.com/catherinedevlin/ddl-generator)を利用してDDLを作成する
- 作成したDDLでPostgreSQLへデータ投入してMetabaseから参照する

## Requirement
- docker
- docker-compose

## Prepare
予め「./csv_data」ディレクトリに可視化するCSVファイルを配置しておくこと。</br>
※「./csv_data」はPostgreSQL環境の「/tmp」にマウントされます

## Install
1. git clone
```sh
$ git clone https://github.com/numasa/metabase.git
$ cd metabase; mkdir csv_data db_data
```
2. build & up
```bash
$ docker-compose up -d
```
3. login to postgres
```bash
$ docker-compose exec postgres /bin/ash
```
4. generate DDL
```ash
# cd /tmp
# ddlgenerator -i postgresql {your_file}.csv > {your_file}.sql
```
5. Create Table & Insert Data
```ash
# psql -U postgres -d metabase -f {your_file}.sql > /dev/null
```
6. Access localhost:3000 with browser & setting your db params
</br>
<img src="https://user-images.githubusercontent.com/55865542/77620417-a8189580-6f7d-11ea-8955-a9716ce8d690.png" width="70%">
</br>
<img src="https://user-images.githubusercontent.com/55865542/77620436-b961a200-6f7d-11ea-9cd4-61f378b49c67.png" width="100%">
