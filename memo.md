# AWSソリューションアーキテクトアソシエイト

個人的に忘れやすそうなところのメモ  

## [Amazon CloudFront](https://aws.amazon.com/jp/cloudfront/)

CDN  
地域制限の機能もある  
アクセスログを出力する場合、ログをS3へ出力する設定にする  

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
暗号化には対応していない  
（EBS, Glacier, DynamoDB, Storge Gateway, SQSは暗号化に対応）

### [Elastic IP](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

Amazon Elastic Compute Cloud用語  
アタッチしているEC2インスタンスが起動しているなら無料  

### ネットワークACLとセキュリティグループ

|種類|内容|
|:---|:---|
|ネットワークACL|VPC内のファイアウォール、サブネット間を跨ぐ通信を制御<br>特定のIPアドレスからの通信を拒否する設定はできない<br>許可しなければデフォルトで拒否|
|セキュリティグループ|EC2などに用いる、ファイアウォールで外部アクセスに対応|

### EC2におけるssh接続用標準ユーザー

ec2-user

### EC2のEIPアドレス

利用していない期間も課金される

### EC2に割り当てるアドレス

|項目|コメント|
|:---|:---|
|パブリックアドレス|毎回ランダムで割り当てられる<br>EC2インスタンスに割り当てないとEC2インスタンスはインターネットへアクセス不可|
|プライベートアドレス|再起動してもアドレスは固定<br>EC2インスタンスを削除しない限り保持される<br>EC2インスタンスをサブネットで起動したら割り当てられる|
|ENI Erastic Network Interface|セカンダリなプライベートIPアドレスとして利用できる<br>他のEC2インスタンスに割り当て可能|

### EC2インスタンスへのIAMロールの追加や修正方法

EC2マネジメントコンソールからEC2インスタンスのアクション操作でアタッチする

## [S3](https://aws.amazon.com/jp/s3/)

データは自動的に複数のAZへコピーされる（リージョンではない）  
有効期限付きの署名付きURLを発行できます
署名付きURLには、直接アップロードも可能（本機能を用いることでWebサーバーへの通信量を下げることができる）  
特定のユーザーのみ限定公開もできる  
標準的なファイルアクセスはサポートしていない  

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
オンプレミスでテープをAWSへ代替するのに用いる  

|種類|ロードに必要な時間|
|:---|:---|
|迅速（Expedited）|1～5分|
|標準（Standard）|3～5時間|
|大容量（Bulk）|5～12時間|

#### S3暗号化

* S3パケットポリシーでデフォルト暗号化を指定し、S3で管理されるキーによるサーバーサイド暗号化を使用  
* キーを使用してすべてのデータを暗号化してからS3に保存  
* S3バケットポリシーでデフォルト暗号化を指定し、[AWS KMS](https://aws.amazon.com/jp/kms/)の管理対象キーでS3サーバーサイド暗号化を使用

## [Amazon SNS](https://aws.amazon.com/jp/sns/)

NはNotification  
HTTP/S、Eメール、SQS、Mobile Push、SMS、Lambdaに対応  

## [Amazon Kinesis](https://aws.amazon.com/jp/kinesis/)

ストリミング処理  

|種類|内容|
|:---|:---|
|Data Analytics|リアルタイム分析|
|Data Streams|Lamdaなどへ提携処理|
|Data Firehose|S3・Redshiftなどへ配信|
|Video Streams|カメラ・ビデオを取り込んで解析可能にする|

## [CloudWatch](https://aws.amazon.com/jp/cloudwatch/)

EC2で稼動しているLinuxのログも取得できる  
CPU使用率・インスタンスストアボリュームより読み取られたバイト数・ネットワークインターフェイスから受信されたバイト数などは標準メトリックスで収集可能  
メモリ使用率・ディスク使用率はカスタムメトリクスの使用が必要  

EC2の障害を管理担当者に通知するには、EC2にCloudWatchエージェントをインストールすることでカスタムログをCloudWatch Logsに配信する  
そしてCloudWatch Logsのメトリックスフィルターで監視する文字列を設定し、SNSからアラートを送信する  

CloudWatch AlarmはClowdWatchの通知機能で、ログをフィルターすることはできない  

## [AWS CloudTrail](https://aws.amazon.com/jp/cloudtrail/)

AWS APIのログを記録する  
EC2で動かしているサーバー内部ログは取得出来ない  

## [Amazon Route 53](https://aws.amazon.com/jp/route53/)

DNS  
CNAMEレコード（ドメイン名やホスト名の定義）・エイリアスレコードはホストされている場所に関係なく任意のDNSレコードを登録できる  
SLAを100%で定義している  
AWSサービスは、エンドポイントのIPアドレスが動的変化するためAレコードの設定を行えません  
代わりにCNAMEレコードまたはエイリアスレコードでエンドポイントを設定する  
CNAMEレコードと比べてエイリアスレコードは、高速で、S3・CloudFront・ELBロードバランサーへのクエリが無料になる  

|Route 53ルーティングポリシーの種類|内容|
|:---|:---|
|Simple|従来のDNSと同様|
|Weight|重みづけを設定し、重み付けの高いほうへ優先|
|Latency|遅延が少ないほうへ優先|
|Failover|利用可能なリソースのみ|
|Geolocation|クライアントの位置情報に基づく|

### マルチバリュールーティング

IPアドレスごとにヘルスチェックをして問題ないルーターへランダムにルーティングできる

## [Amazon VPC](https://aws.amazon.com/jp/vpc/)

AWS内の独立した仮想ネットワークを構築する  

|種類|内容|
|:---|:---|
|[VPCフローログ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/flow-logs.html)|VPC内のネットワークインターフェィス間の通信トラフィックも監視可能|
|[VPCエンドポイント](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-endpoints.html)|VPCリソースとAWSサービス間を接続する、EC2からS3やDynamoDBに接続できる|
|[VPCピアリング](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-peering.html)|「別のAWSアカウントと」インターネットを経由せずVPC間を接続|

## [Amazon EBS](https://aws.amazon.com/jp/ebs/)

Amazon Elastic Block Store  
EC2に接続できるブロックレベルストレージ  
単一のEC2インスタンスにしかアタッチできない  
スナップショットを別のリージョンへコピー可能  
ストレージの自動拡大・縮小はサポートしていない  

|種類|内容|
|:---|:---|
|Instance Store-Backedインスタンス|停止や再開はできない<br>アタッチされているEC2インスタンスが再起動するとデータは失われる|
|EBS-Backedインスタンス|停止や再開が可能<br>アタッチされているEC2インスタンスが再起動してもデータは失われない、利用するアプリケーションの特性に応じてタイプを選択できる|

|種類|内容|
|:---|:---|
|プロビジョンドIOPS SSD|パフォーマンスを最大限に引き出す|
|スループット最適化HDD|HDDの中ではスループットが高い、低コスト、ビッグデータ向け|

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

### SQSにおけるキューの種類

キューは標準キューとFirst In First Out(FIFO)キューが利用できる  

|キュー|標準キュー|FIFOキュー|
|:---|:---|:---|
|配信|ベストエフォート<br>少なくとも1回行われる|メッセージが送信順のとおり配信<br>1回限りで確実に処理される|
|特徴|最大限のスループットが選べる|逐次処理を行うケースで利用|

FIFOキューにおいてメッセージは1回配信されることが保証されている  

## AWS Consolidated Billing

一括請求  
メンバーアカウント（Linked Account）とマスターアカウント（Payer Account）を統合可能

## [AWS CloudFormation](https://aws.amazon.com/jp/cloudformation/)

共通言語（JSONまたはYAML）を用いてリソースを公開可能準備をする  
プロビジョニング（リソースの準備）されるAWSリソースの集合＝スタック  
Properties Resourceが必須項目  
テスト環境と本番環境を自動で同一構成化させたいときに用いる  

|項目|内容|
|:---|:---|
|CidrBlock|許可・拒否するネットワークアドレスを表記|
|Egress|サブネットからの送受信どちらに適用するか指定|
|RuleAction|ルール一致するトラフィックについて許可・拒否するか指定|

## [AWS CloudFormationデザイナー](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/working-with-templates-cfn-designer.html)

テンプレートを作成する際にAWSの各種リソース用テンプレートスぺニットなど補助的な機能を使う、グラフィックツール

## [AWS Elastic Beanstalk](https://aws.amazon.com/jp/elasticbeanstalk/)

コードをアップロードしたらAWSが環境構築（プロビジョニング）・運用開始（デプロイ）まで面倒を見てくれる  
Nginx上に構築されたWebアプリケーションもデプロイできる  
自社におけるWebアプリインフラ管理の負荷を下げ、アプリのコード開発に注力したいときに用いる  

## [AWS OpsWorks](https://aws.amazon.com/jp/opsworks/)

ChefやPuppet（構築手順）どおりにサーバー構築を自動化してくれる  

## [Amazon Aurora](https://aws.amazon.com/jp/rds/aurora/)

RDB  
データ量に合わせで自動拡張する  

## RDS for MySQL

Amazon Auroraと比較してフェイルオーバー時に数分間のデータを損失する可能性がある  
シングルインスタンス構成で運用しているDBで障害が発生しバックアップからリストアする手段は以下の通り  

1. 新しいプライマリインスタンス上にRDSスナップショットからRDSを復元する。  

1. エンドポイントを新しいプライマリDBインスタンスに書き換える  

## [AWS Auto Scaling](https://aws.amazon.com/jp/autoscaling/)

EC2インスタンス増加時は、EC2インスタンスが一番少ないAZを指定して起動する  

### ユーザーデータ（EC2）

EC2起動時に一度だけスクリプトを実行できる  
Auto Scalingグループで作成された新しいAmazon Linuxインスタンスにカスタムスクリプトを渡すこともできる  

### インスタンスメタデータ（EC2）

実行中のEC2インスタンスを設定するのに用いる  

### Auto Scalingグループ

起動されたインスタンスは複数のアベイラビリティーゾーン間で均等にバランシングされる  

## NATゲートウェイ・[インターネットゲートウェイ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Internet_Gateway.html)

インターネットからアクセスできるのはWebサーバーだけだが、奥のDBサーバーも更新のために内部からの接続は許可したい場合に設置  
アクセス制御を行うためのものではない  

### ゲートウェイの種類

|種類|内容|
|:---|:---|
|保管型ボリュームゲートウェイ|オンプレミスのディスクデータスナップショットをS3に保存、データのプライマリコピーはオンプレミス|
|キャッシュ型ゲートウェイ|オンプレミスのディスクデータスナップショットをS3に保存、**データのプライマリコピーはS3・よく使われるデータのみオンプレミス**|
|テープゲートウェイ|仮想テープライブラリ対応バックアップソフトウェアを利用し、Storage gateway経由でS3に保存|
|ファイルゲートウェイ|S3をオンプレミスのNAS共有ファイルシステムのバックエンドストレージとして使う|

## [Amazon EMR](https://aws.amazon.com/jp/emr/)

Apache SparkやHadhopを用いて膨大なデータを迅速かつ高効率で分析するサービス

## リバースプロキシ

一般的な用語、[外部からWebサーバーへアクセスされる際、Webサーバーの代替を行って負荷を下げるサービス](https://www.atmarkit.co.jp/ait/articles/1608/25/news034.html)

## [IAM](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/introduction.html)

グローバルサービスなのでリージョンごとに作成する必要はない  
別リージョンで同じ権限を割り当てる場合は、コピーせずそのまま割り当てれば良い  

制限については以下の通り  
|種類|内容|
|:---|:---|
|アカウント|1アカウント＝5000ユーザーまで|
|所属グループ|10グループまで|
|作成グループ|100グループまで|

ユーザー一覧よりアクセスキーの古さやMFAの有効・無効を調べることができる  

### IAMのアクセスアドバイザー

ポリシーを使用したユーザの確認、サービスに関連するポリシーの確認ができる

### IAMのアクセスアドバイザー（Access Advisor）におけるService Last Accessed Data

IAMエンティティが、最後にAWSサービスへアクセスした日付と時刻

### IAMのCredential Report

利用日付などが記録されたIAM認証情報にかかわるレポートファイル

### [Temporary Security Credentials](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_credentials_temp.html)

AWSに対して一時的な認証情報を作成する仕組み

### [インラインポリシー](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#inline-policies)

1つのプリンシパルエンティティ（ユーザー、グループ、またはロール）に埋め込まれたポリシーであり、つまり、プリンシパルエンティティに固有です。  
プリンシパルエンティティの作成時、またはそれ以降で、ポリシーを作成してプリンシパルエンティティに埋め込むことができます。  

## [Elastic Load Balancing](https://aws.amazon.com/jp/elasticloadbalancing/)

### ELBの種類

||Application Load Balancer|Network Load Balancer|Classic Load Balancer|
|:--|:--|:--|:--|
|略称|ALB|NLB|CLB|
|機能|リクエストのクエリーからあらかじめ設定されたルーティングに沿って振り分けをする<br>ELB自体が負荷に応じて自動にスケールします|ロードバランサーのアクセス先をドメイン名ではなく固定IPアドレスで設定できる<br>宛先IPアドレスをターゲットのIPアドレスに書き換えて転送<br>応答トラフィックはロードバランサーを経由せず直接クライアントに送信される|リクエストのURL毎にロードバランサーを用意して、コンテナサービス上のアプリケーション単位でリクエストを振り分けられる、クライアント・ターゲット間通信はリクエスト・応答共にロードバランサーを経由する|
|コメント|レイヤー7でHTTP/HTTPSを提供、負荷分散など実装|レイヤー4のTCP・レイヤー5のTLSをサポート、固定IPアドレス、応答トラフィックはロードバランサーを経由せずクライアントに直接送るので高パフォーマンス|HTTP/HTTPSを提供しているが旧来のサービス|

### Pre-Warming（暖機運転）

トラフィックの急増が予想される場合事前にELBをスケールしたい場合は、AWSサポートに申請する  
※AWSコンソールからでは対応できない  

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

ElastiCacheの種類は以下の通り  
※どちらも複数台用いた大規模化が可能  

|種類|Redis用|memcached用|
|:---|:---|:---|
|概要|Redis(Remote dictionary Server)とはメモリ上にKey-Valueストアを構築することができるDBサーバーの1つ|分散メモリキャッシュシステムの1つ<br>DBの読み出し結果を返す|
|向いているケース|データ型:複雑<br>暗号化:あり<br>マルチスレッド:なし<br>高可用性:あり<br>自動フェイルオーバー:必須<br>バックアップと復元:あり|**データ型:シンプル**<br>暗号化:なし<br>**マルチスレッド:あり**<br>高可用性:なし<br>自動フェイルオーバー:なし<br>バックアップと復元:なし|

### Redis用ElastiCache

Redis(Remote dictionary Server)とはメモリ上にKey-Valueストアを構築することができるDBサーバーの1つ、複数台用いた大規模化が可能  
以下の環境に適する  

## [AWS Data Pipeline](https://docs.aws.amazon.com/ja_jp/datapipeline/latest/DeveloperGuide/what-is-datapipeline.html)

データベースからのデータを取り出し・加工・保存するサービス

## [AWS Storage Gateway](https://aws.amazon.com/jp/storagegateway/)

ローカルキャッシング対応のハイブリッドクラウドストレージ  
オンプレミスのアプライアンス（例:社内業務サーバー）と接続し、バックアップを行う  

## [Amazon Redshift](https://aws.amazon.com/jp/redshift/)

Amazon S3上の巨大データの分析に用いる  
スナップショットでバックアップする  
自動取得したスナップショットは8時間もしくは5GBのデータ更新があるたびに自動で取得する  
ノード数を増やすと複数のデータベースがクラスター化され、対象外性が高まる  
リードレプリカ・マルチAZは設定できない  
小さなデータを大量・高速に登録する行指向型の処理には向いていない  
コンピューターノードの障害は、自動的に検知・代替ノードがプロビジョニングされる  
ただし、代替ノードが復旧されるまでは更新されない  

### [Amazon Redshift Spectrum](https://aws.amazon.com/jp/blogs/news/amazon-redshift-spectrum-exabyte-scale-in-place-queries-of-s3-data/)

エクサバイトに膨れるデータ対応へ用いる  
（Readshiftではコスト効率が低下する）  
※ギガ→テラ→ペタ→エクサ  

## プレイスメントグループ

単一AZ内のEC2インスタンスを論理的にグルーピングしたもの  

## [Amazon EFS](https://aws.amazon.com/jp/efs/)

Elastic File System  
標準的なファイルシステムをサポート  
ストレージの自動拡大・縮小もサポート  

## [Dynamo DB](https://aws.amazon.com/jp/dynamodb/)

スキーマ（表と属性）のないデータベース  
複数のスキーマをそのままの状態で保存しつつ、保存後にスキーマを修正できる  
センサーから贈られる小さなデータを大量の受信リクエストによって高速蓄積するのに向いている  

## [AWS Artifact](https://aws.amazon.com/jp/artifact/)

AWS上のコンプライアンスレポートへのオンデマンドアクセス

## [AWS CodeCommit](https://aws.amazon.com/jp/codecommit/)

プライベートGitレポジトリでのコード保存

## [AWS CodeBuild](https://aws.amazon.com/jp/codebuild/)

コードのビルドとテスト

## [AWS CodeDeply](https://aws.amazon.com/jp/codedeploy/)

コードデプロイの自動化  
CodeComit（コード保存）→CodeBuild（ビルトとテスト）→CodeDeply（アプリケーションとして展開）とセットで使われることが多い  

## [AWS CodePipeline](https://aws.amazon.com/jp/codepipeline/)

継続的デリバリーを使用したソフトウェアのリリース  
DataPipelineとは異なる  
ビルド、テスト、デプロイなど、リリース作業に必要な一連のプロセスをまとめたもの  

## [AWS Config](https://aws.amazon.com/jp/config/)

IAMを用いたAWSリソースの設定（IAMのUser・Group・Role・Policyの変更履歴・構成変更）を評価、監査、審査を行う

## [AWS Security Token Service(STS)](https://aws.amazon.com/jp/blogs/news/category/security-identity-compliance/aws-security-token-service/)

動的にIAMユーザーを作り、一時的に利用するトークンを発行するサービス  

## [AWS Organizations](https://aws.amazon.com/jp/organizations/)

AWSアカウントの一元管理、大きな組織におけるIAMの管理を簡易化する  
開発アカウントと本番環境アカウントをOrganizationsメンバーアカウントとしてマスターアカウントに登録して一括請求させることもできる  

* 複数アカウントの一元管理  

組織単位をOUという  

* 新規アカウント作成の自動化  

* 一括請求  

管理ができるのはAWS Organizationのマスターアカウントのみ  
IAMのルートアカウントでは管理できない  

### AWS Organizations：機能セットの選択

|名前|機能|
|:--|:--|
|Consolidated Biling Only|支払い一括代行のみを実施する場合に選択|
|All Feature|Consolidated Biling Onlyに加えて企業内の複数アカウントも統制したい場合に選択|

## Direct Connect

### 接続構成

|種類|内容|
|:---|:---|
|物理接続|相互接続ポイントDirect Connectロケーションを介してAWSと接続|
|論理接続|物理的接続を論理的に分割し、複数のAWSアカウントで利用|

### 接続方法

|種類|内容|
|:---|:---|
|プライベート接続|VPC(EC2)への接続を許可する<br>アドレス変換は不要|
|パブリック接続|中国を除くAWSの前リージョンへのパブリックサービスへ接続できる<br>NAT機器などによるパブリックIPアドレスにアドレス変換する必要がある|

下記のどちらでも、AWS・オンプレミス間の安定した通信と万が一の障害時の迅速な対応＆低コストのネットワークが提供できる

|種類|内容|
|:---|:---|
|共有型|2Gbpsの帯域を提供|
|占有型|1Gbpsか10Gbpsの帯域を提供|

### Direct Connect Gateway

プライベート接続においてDirect Connect Gatewayを用いると中国を除くVPCリソースへアクセスができます＝中国を除きリージョンの設定が不要  
ただし複数リージョンへまたがるVPCのリソース同士はDirect Connect Gatewayで通信できない  
データセンター同士もDirect Connect Gatewayで通信できない  

### Direct Connect料金体系

ポート時間（使用料）とデータ転送量の2つに分けて請求される

### VGW (Virtual Private Gateway)

AWS側でVPCに対して取り付け可能な仮想ルーター  

### Virtual Interface（VIF:仮想インターフェイス）

新プロジェクト専用のVLAN IDを割り当てることで、独立したネットワーク環境のAWSとオンプレミス環境のハイブリッドシステムを低コストで開発できる

## SWF (Amazon Simple Workflow Service)

ひとかたまりの処理に関する状態管理とタスク間の流れ（＝ワークフロー）の管理を行う  
Ruby/Java/.NET/PHPなどに対応している、Pythonは非対応  

## インスタンスの種類

|No|種類|内容|
|--:|:---|:---|
|1|スポット|AWS側で余裕があるときに、ユーザーから提示した料金より安い場合に利用できる<br>中断されることがあるので、アプリケーションはEC2に障害が発生しても適切に対処できる必要がある|
|2|リザーブド|予約することで最大75%の割引を受ける<br>いつでもは使えない|
|3|オンデマンド|利用した分だけ課金|

## タグ

部門や環境ごとに費用を確認するのなどに用いる

## Active Directory

* Directory Service Simple AD  
既存のActive Directoryとは連携できない

* Directory Service AD Connector  
既存のオンプレミスActive Directoryと連携できる、認証をリダイレクトしてIAMロールで設定されたアクセス権限をADユーザーに与える

## 管理者の退職

1. ルートユーザーのMFAデバイスを新しい管理者が引き継ぎ、パスワード変更

1. 旧管理者のIAMユーザーを削除

1. 旧管理者がルートユーザーのアクセスキー有していたら削除する  
（そもそもルートユーザーがアクセスキーを所有することを推奨していない）

## AWSが提供するコンテナーサービスEKS/ECS

コントロープレーンは、KubernetesとAWS独自のコンテナー管理サービス  

## [Amazon Simple Email Service(SES)](https://aws.amazon.com/jp/ses/)

メール配信サービス  
HTTP REST APIもしくはSMTPエンドポイントによりメール送信を行う  
