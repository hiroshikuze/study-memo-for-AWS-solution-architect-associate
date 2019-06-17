# AWSソリューションアーキテクトアソシエイト

個人的に忘れやすそうなところのメモ  

## [Amazon CloudFront](https://aws.amazon.com/jp/cloudfront/)

CDN  

## [AWS CLI](https://aws.amazon.com/jp/cli/)

コマンド操作できる  
アクセスIDとシークレットキーで操作できる  
IAMポリシーは認証に不要  

## [Amazon Elastic Compute Cloud (EC2)](https://aws.amazon.com/jp/ec2/)

ハイパーバイザー仮想化を利用したコンピューティングサービス

### [Elastic IP](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

Amazon Elastic Compute Cloud用語  
アタッチしているEC2インスタンスが起動しているなら無料  

### ネットワークACLとセキュリティグループ

ネットワークACLはVPC内のファイアウォール  
サブネット間を跨ぐ通信を制御  
セキュリティグループはEC2などに用いるファイアウォールで外部アクセスに対応  

### EC2インスタンス

### [リザーブドインスタンス](https://aws.amazon.com/jp/ec2/pricing/reserved-instances/)

利用期間分をあらかじめ購入することで割引価格が適応

|種類|内容|
|:---|:---|
|Standardタイプ|リージョンやAZを指定してインスタンスを購入、同じインスタンス構成なら同じリージョンやAZ内でインスタンスの配置変更が可能|
|Convertibleタイプ|自由に構成変更が可能だが、Standardタイプより割高|
|スケジュール|1年間に渡り毎日・毎週・毎月キャパシー予約を受けつける|

### EC2インスタンスストア

インスタンス用のブロックレベルの一時ストレージを提供

## [S3](https://aws.amazon.com/jp/s3/)

データは自動的に複数のAZへコピーされる（リージョンではない）  
有効期限付きの署名付きURLを発行できます
署名付きURLには、直接アップロードも可能（本機能を用いることでWebサーバーへの通信量を下げることができる）  
特定のユーザーのみ限定公開もできる  

### [S3 Glacier](https://aws.amazon.com/jp/glacier/)

もっとも安価、ロードに何時間もかかる  
めったにアクセスしないデーターの管理に用いる  

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

### [VPCフローログ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/flow-logs.html)

 VPC内のネットワークインターフェィス間の通信トラフィックも監視可能

## [Amazon EBS](https://aws.amazon.com/jp/ebs/)

Amazon Elastic Block Store  
EC2に接続できるブロックレベルストレージ  
単一のEC2インスタンスにしかアタッチできない  
スナップショットを別のリージョンへコピー可能  

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

## NATゲートウェイ

インターネットからアクセスできるのはWebサーバーだけだが、奥のDBサーバーも更新のために内部からの接続は許可したい場合に設置
