## 概要
コンテナ Lambda [(link)](https://aws.amazon.com/jp/builders-flash/202103/new-lambda-container-development/?awsf.filter-name=*all)  
における複数の Lambda 関数の管理を検討

## リポジトリ構成
### docker
Dockerfile を配置
### src
Lambda 関数単位でディレクトリを作成し配置

## Lambda 関数のコンテナ起動
### 起動
```
// build で関数を COPY しているので関数を変更した際には build で反映が必要
docker-compose up -d --build
```
### 確認
```
curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{}'
```
### 実行する Lambda 関数の切替 (handler 指定の切替)
docker-compose.yml の command 指定を別の Lambda 関数 handler に変更します。
```
command: src/function_a/app.handler
↓
command: src/function_b/app.handler
```

## この管理で何が嬉しいのか
- Lambda 関数のテストをローカルで行うことができる
- ひとつのコンテナイメージで複数の Lambda 関数を管理できる(特定のスコープの関数をまとめて管理できる)
- 起動時の設定(CMD) でどの関数を実行するのか指定できる
  - ローカルの Docker でも、本番の Lambda でも外部から handler 指定可能