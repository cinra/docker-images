# Docker Images

## Docker Hub

https://hub.docker.com/r/cinra/

## Usage

1. Docker Imageごとにディレクトリを切る
1. 各ディレクトリにDockerfileとREADME.mdを配置する
1. Docker Hubにリポジトリがない場合は、[cinraリポジトリ](https://hub.docker.com/r/cinra/)で作成する
1. Docker Hubにログインしていない場合は、`docker login`でログイン
1. 各ディレクトリ以下で、`docker build -t cinra/{リポジトリ名} .`を開始する
  1. 必要な場合は、`docker tag cinra/{リポジトリ名} cinra/{リポジトリ名}:{タグ}`でタグ付けする
1. `docker push cinra/{リポジトリ名}`で、`latest`をDocker Hubに反映する