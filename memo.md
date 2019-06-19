# AWSソリューションアーキテクトアソシエイト

個人的に忘れやすそうなところのメモ  

## [Amazon CloudFront](https://aws.amazon.com/jp/cloudfront/)

CDN  
地域制限の機能もある  

## [AWS CLI](https://aws.amazon.com/jp/cli/)

コマンド操作できる  
アクセスIDとシークレットキーで操作できる  
IAMポリシーは認証に不要  

## [Amazon Elastic Compute Cloud (EC2)](https://aws.amazon.com/jp/ec2/)

ハイパーバイザー仮想化を利用したコンピューティングサービス

### EC2インスタンスメタデータで確認できる情報

* プライベートIPアドレス
* パブリックIPアドレス
* インスタンスのローカルホスト名
* 公開鍵（パブリックキー）

### [リザーブドインスタンス](https://aws.amazon.com/jp/ec2/pricing/reserved-instances/)

利用期間分をあらかじめ購入することで割引価格が適応

|種類|内容|
|:---|:---|
|Standardタイプ|リージョンやAZを指定してインスタンスを購入、同じインスタンス構成なら同じリージョンやAZ内でインスタンスの配置変更が可能|
|Convertibleタイプ|自由に構成変更が可能だが、Standardタイプより割高|
|スケジュール|1年間に渡り毎日・毎週・毎月キャパシー予約を受けつける|

### EC2インスタンスストア

インスタンス用のブロックレベルの一時ストレージを提供

### [Elastic IP](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

Amazon Elastic Compute Cloud用語  
アタッチしているEC2インスタンスが起動しているなら無料  

### ネットワークACLとセキュリティグループ

|種類|内容|
|:---|:---|
|ネットワークACL|VPC内のファイアウォール、サブネット間を跨ぐ通信を制御<br>特定のIPアドレスからの通信を拒否する設定はできない<br>許可しなければデフォルトで拒否|
|セキュリティグループ|EC2などに用いる、ファイアウォールで外部アクセスに対応|

## [S3](https://aws.amazon.com/jp/s3/)

データは自動的に複数のAZへコピーされる（リージョンではない）  
有効期限付きの署名付きURLを発行できます
署名付きURLには、直接アップロードも可能（本機能を用いることでWebサーバーへの通信量を下げることができる）  
特定のユーザーのみ限定公開もできる  

### S3データ整合性

|種類|データ整合性|
|:---|:---|
|PUT（新規追加）|書き込み後の読み込み整合性、S3から完了（HTTP200）が返されるとデータ参照可能|
|PUT（更新）|結果整合性|
|DELETE（削除）|結果整合性|

### S3ストレージクラス

|種類|ストレージクラス|
|:---|:---|
|スタンダード|頻繁なデータアクセスに向く|
|標準低頻度アクセス|低頻度アクセスに向く、すぐにデータが取り出せる|
|1ゾーン低頻度アクセス|低頻度アクセスで耐久性が低くても良くてコスト重視の場合に向く、すぐにデータが取り出せる|
|[S3 Glacier](https://aws.amazon.com/jp/glacier/)|※別項目参照|

#### [S3 Glacier](https://aws.amazon.com/jp/glacier/)

S3ストレージクラスの1つ  
もっとも安価、ロードに何時間もかかるものもある  
めったにアクセスしないデーター＝アーカイブの管理に用いる  

|種類|ロードに必要な時間|
|:---|:---|
|迅速（Expedited）|1～5分|
|標準（Standard）|3～5時間|
|大容量（Bulk）|5～12時間|

## [Amazon SNS](https://aws.amazon.com/jp/sns/)

NはNotification  

## [Amazon Kinesis](https://aws.amazon.com/jp/kinesis/)

ストリミング処理  

|種類|内容|
|:---|:---|
|Data Analytics|リアルタイム分析|
|Data Streams|提携処理|
|Data Firehose|配信|

## [CloudFormation](https://aws.amazon.com/jp/cloudformation/)

プロビジョニング（リソースの準備）されるAWSリソースの集合＝スタック  

## [CloudWatch](https://aws.amazon.com/jp/cloudwatch/)

EC2で稼動しているLinuxのログも取得できる  
メモリ使用率はカスタムメトリクスの使用が必要  

## [AWS CloudTrail](https://aws.amazon.com/jp/cloudtrail/)

AWS APIのログを記録する  
EC2で動かしているサーバー内部ログは取得出来ない  

## [Amazon Route 53](https://aws.amazon.com/jp/route53/)

DNS  
CNAMEレコード（ドメイン名やホスト名の定義）はホストされている場所に関係なく任意のDNSレコードを登録できる  

## [Amazon VPC](https://aws.amazon.com/jp/vpc/)

AWS内の独立した仮想ネットワークを構築する  

|種類|内容|
|:---|:---|
|[VPCフローログ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/flow-logs.html)|VPC内のネットワークインターフェィス間の通信トラフィックも監視可能|
|[VPCエンドポイント](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-endpoints.html)|VPCリソースとAWSサービス間を接続する|
|[VPCピアリング](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-peering.html)|別のAWSアカウントとインターネットを経由せずVPC間を接続|

## [Amazon EBS](https://aws.amazon.com/jp/ebs/)

Amazon Elastic Block Store  
EC2に接続できるブロックレベルストレージ  
単一のEC2インスタンスにしかアタッチできない  
スナップショットを別のリージョンへコピー可能  

|種類|内容|
|:---|:---|
|Instance Store-Backedインスタンス|停止や再開はできない|
|EBS-Backedインスタンス|停止や再開が可能|

### マグネティック

EBSにおいてアクセス頻度が低い用途に適した旧世代のHDD

## [AWS KMS](https://aws.amazon.com/jp/kms/)

鍵の管理・保管  
一般的な案件に用いる  

## [AWS CloudHSM](https://aws.amazon.com/jp/cloudhsm/)

鍵の管理・保管  
コンプライアンス要件が厳しい場合に用いる  
ユーザー占有のハードウェアアプライアンスを用いている  

## IOPS

ハードディスクなどの記憶装置の性能指標の1つで、ある条件の元で1秒間に読み込み・書き込みできる回数のこと  

## [Amazon SQS](https://aws.amazon.com/jp/sqs/)

EC2インスタンス間で非同期なジョブ制御に用いる  

## AWS Consolidated Billing

一括請求  
メンバーアカウント（Linked Account）とマスターアカウント（Payer Account）を統合可能

## [AWS CloudFormation](https://aws.amazon.com/jp/cloudformation/)

|項目|内容|
|:---|:---|
|CidrBlock|許可・拒否するネットワークアドレスを表記|
|Egress|サブネットからの送受信どちらに適用するか指定|
|RuleAction|ルール一致するトラフィックについて許可・拒否するか指定|

## [AWS Elastic Beanstalk](https://aws.amazon.com/jp/elasticbeanstalk/)

コードをアップロードしたらAWSが環境構築（プロビジョニング）・運用開始（デプロイ）まで面倒を見てくれる  
Nginx上に構築されたWebアプリケーションもデプロイできる

## [AWS OpsWorks](https://aws.amazon.com/jp/opsworks/)

ChefやPuppet（構築手順）どおりにサーバー構築を自動化してくれる  

## [Amazon Aurora](https://aws.amazon.com/jp/rds/aurora/)

RDB  
データ量に合わせで自動拡張する  

## [AWS Auto Scaling](https://aws.amazon.com/jp/autoscaling/)

EC2インスタンス増加時は、EC2インスタンスが一番少ないAZを指定して起動する  

### ユーザーデータ

EC2起動時に一度だけスクリプトを実行できる  
Auto Scalingグループで作成された新しいAmazon Linuxインスタンスにカスタムスクリプトを渡すこともできる  

## NATゲートウェイ

インターネットからアクセスできるのはWebサーバーだけだが、奥のDBサーバーも更新のために内部からの接続は許可したい場合に設置

## [Amazon EMR](https://aws.amazon.com/jp/emr/)

Apache SparkやHadhopを用いて膨大なデータを迅速かつ高効率で分析するサービス

## リバースプロキシ

一般的な用語、[外部からWebサーバーへアクセスされる際、Webサーバーの代替を行って負荷を下げるサービス](https://www.atmarkit.co.jp/ait/articles/1608/25/news034.html)

## [IAM](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/introduction.html)

グローバルサービスなのでリージョンごとに作成する必要はない  
別リージョンで同じ権限を割り当てる場合は、コピーせずそのまま割り当てれば良い

## [Elastic Load Balancing](https://aws.amazon.com/jp/elasticloadbalancing/)

ELB  
Application Load Balancerでは、リクエストのクエリーからあらかじめ設定されたルーティングに沿って振り分けをする  

## 脆弱性／侵入テスト

ユーザー自身がAWSに事前申請し許可を得た上で行う  
テストはすべてのインスタンスで許可されるわけではない  

## [API Gateway](https://aws.amazon.com/jp/api-gateway/)

APIを簡単に作れる  
APIキャッシュを有効にすることでレスポンスがキャッシュされ、APIキャッシュは時間単位で課金される  
有効期限TTLが0の場合、キャッシュはされない  

## [Amazon ElastiCache](https://aws.amazon.com/jp/elasticache/)

メモリ上でキャッシュするので高速  
RDSと組み合わせる  
