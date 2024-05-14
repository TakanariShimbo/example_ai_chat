# About

Ollama x Dify x OpenWebUI のサンプル

### ollama

以下の Docker Image を利用している

https://hub.docker.com/r/ollama/ollama

### dify

以下のリポジトリの docker dir の `docker-compose.yaml`, `nginx` を利用している

https://github.com/langgenius/dify

### dify2openai

以下のリポジトリを Docker Image 化したものを使用している

https://github.com/fatwang2/dify2openai

### open_webui

以下のリポジトリを利用している

https://github.com/open-webui/open-webui

リポジトリの readme と以下の litellm totorial を参考に docker-compose を作成した

https://docs.openwebui.com/tutorial/litellm/

# Use

### ollama

ディレクトリの直下で docker compose を実行   
※ `docker-compose.yaml` で GPU を使う or 使わないの設定する

```shell
cd ollama
docker-compose up -d
```

コンテナが起動後に pull, run でテストする

```shell
# コンテナに入る
docker exec -it ollama bash

# pull
ollama pull llama2

# run
ollama run llama2
```

### dify

ディレクトリの直下で docker compose を実行

```shell
cd dify
docker-compose up -d
```

コンテナが起動したら以下リンクから起動する  
アカウント設定すれば使えるようになる

[http://localhost:54322/install](http://localhost:54322/install)

### dify2openai

`docker-compose.yaml.sample` を参考に `docker-compose.yaml` を作成し  
 その後、ディレクトリの直下で docker compose を実行

```shell
cd dify2openai
docker-compose up -d
```

### open_webui

litellm dir の`config.yaml.sample` を参考に `config.yaml` を作成し  
 その後、ディレクトリの直下で docker compose を実行

```shell
cd open_webui
docker-compose up -d
```

コンテナが起動したら以下リンクから起動する  
アカウント設定すれば使えるようになる

[http://localhost:54321/auth/](http://localhost:54321/auth/)

# Build

以下、 dify2openai の Docker Image の作成フロー

1. リポジトリをクローン

```shell
git clone https://github.com/fatwang2/dify2openai
```

2. Docker Image 化
   以下の .dockerignore, Dockerfile を用意し、コマンドを打ってビルド

```.dockerignore
.github
pictures/
.env.template
.gitignore
LICENSE
pnpm-lock.yaml
readme.md
vercel.json
```

```Dockerfile
FROM node:16

WORKDIR /work
COPY . .

RUN npm install
EXPOSE 3000

CMD ["npm", "start"]
```

```shell
docker build -t <user name>/<image name>:<varsion> .
```
