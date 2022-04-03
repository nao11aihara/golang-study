# sample2

## コマンドメモ

### Docker イメージ

```bash
// イメージ確認
docker image ls

// イメージ作成
//
// イメージ名: sampleImage
// タグ名: latest
// . 今いるディレクトリのDockerfileを参照する
docker image build -t sampleImage:latest .
```

### Docker コンテナ

```bash
// コンテナ作成・起動
//
// コンテナ名: sampleContainer
// 参照イメージ: sampleImage:latest
// ポート8000とDocker上のポート8000を繋げる
// -dをつけるとバックグラウンドで起動する
docker container run -p 8000:8000 --name sampleContainer sampleImage:latest -d

// コンテナの起動状態を確認
//
// -aをつけると停止しているものも含めて表示する
docker container ls -a

// コンテナ停止
docker container stop sampleContainer

// コンテナ削除
docker container rm sampleContainer

// ログ確認
docker container logs sampleContainer

// 実行中のコンテナで別のコマンドを使う
//
// 実行中のコンテナのGoのバージョンを確認
docker container exec sampleContainer go version

// 使用していないイメージ、コンテナを削除
docker system prune -a
```

### docker-compose

```
// サービスのビルドを実行する
//
// ymlファイルにimageが書かれている場合、そのイメージ名がローカルになければリモートからプルしてくる
// imageが書かれていない場合、buildに書かれているパスのDockerfileを元にイメージを構築する
docker-compose build

// コンテナを作成して起動
//
// -d: バックグラウンドで実行
docker-compose up

// サーバーを切ってコンテナを削除
docker-compose down

// コンテナ一覧を表示
docker-compose ps

// ログを表示
docker-compose logs

// 引数で指定したサービスのコンテナ内でコマンドを実行（webコンテナの例）
docker-compose run web go version
```
