# データベース：AWSソリューションアーキテクトアソシエイト

## [Amazon Aurora](https://aws.amazon.com/jp/rds/aurora/)

RDB  
データ量に合わせで自動拡張する  

## [RDS for MySQL](https://aws.amazon.com/jp/rds/mysql/)

Amazon Auroraと比較してフェイルオーバー時に数分間のデータを損失する可能性がある  
シングルインスタンス構成で運用しているDBで障害が発生しバックアップからリストアする手段は以下の通り  

1. 新しいプライマリインスタンス上にRDSスナップショットからRDSを復元する。  

1. エンドポイントを新しいプライマリDBインスタンスに書き換える  

### RDS for MySQLにおける接続安定化コマンドオプション

ssl-caオプションに公開鍵のフルパスを指定してmysqlクライアントを起動  

## [AWS Data Pipeline](https://docs.aws.amazon.com/ja_jp/datapipeline/latest/DeveloperGuide/what-is-datapipeline.html)

データベースからのデータを取り出し・加工・保存するサービス

## [Amazon Redshift](https://aws.amazon.com/jp/redshift/)

Amazon S3上の巨大データの分析に用いる  
スナップショットでバックアップする  
自動取得したスナップショットは8時間もしくは5GBのデータ更新があるたびに自動で取得する  
**ノード数を増やすと複数のデータベースがクラスター化され、対象外性が高まる**  
リードレプリカ・マルチAZは設定できない  
小さなデータを大量・高速に登録する行指向型の処理には向いていない  
コンピューターノードの障害は、自動的に検知・代替ノードがプロビジョニングされる  
ただし、代替ノードが復旧されるまでは更新されない  

### [Amazon Redshift Spectrum](https://aws.amazon.com/jp/blogs/news/amazon-redshift-spectrum-exabyte-scale-in-place-queries-of-s3-data/)

**ペタ・エクサバイトに膨れるデータ対応へ用いる**  
（Redshiftでも運用できるがコスト効率が低下する）  
※ギガ→テラ→ペタ→エクサ  
S3上に置いたファイルを外部テーブルとして使用する  

## [Dynamo DB](https://aws.amazon.com/jp/dynamodb/)

スキーマ（表と属性）のないデータベース  
複数のスキーマをそのままの状態で保存しつつ、保存後にスキーマを修正できる  
センサーから贈られる小さなデータを大量の受信リクエストによって高速蓄積するのに向いている  

## [Dynamo DB Accelerator](https://aws.amazon.com/jp/dynamodb/dax/)

Dyanamo DBのインメモリキャッシュサービス  
1秒あたり100満開単位のリクエスト処理でも、数ミリ秒のレイテンシーを実現  
