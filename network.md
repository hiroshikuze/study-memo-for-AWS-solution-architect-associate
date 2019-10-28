# ネットワーク：AWSソリューションアーキテクトアソシエイト

## [Amazon CloudFront](https://aws.amazon.com/jp/cloudfront/)

CDN  
地域制限の機能もある  
アクセスログを出力する場合、ログをS3へ出力する設定にする  
暗号化通信をする場合、**デフォルトのSSL証明書では独自ドメイン名が使えない**ので、X.509PEM形式のSSL証明書をインポート  

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
|[VPCエンドポイント](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-endpoints.html)|インターネットを経由せずVPCリソースとAWSサービス間をプライベート接続する、EC2からS3やDynamoDBに接続できる|
|[VPCピアリング](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/vpc-peering.html)|「別のAWSアカウントと」インターネットを経由せずVPC間を接続|

## NATゲートウェイ・[インターネットゲートウェイ](https://docs.aws.amazon.com/ja_jp/vpc/latest/userguide/VPC_Internet_Gateway.html)

インターネットからアクセスできるのはWebサーバーだけだが、奥のDBサーバーも更新のために内部からの接続は許可したい場合に設置  
アクセス制御を行うためのものではない  
単一サービスで起動しているので、単一障害点にならないよう構築する必要がある  

### ゲートウェイの種類

|種類|内容|
|:---|:---|
|保管型ボリュームゲートウェイ|オンプレミスのディスクデータスナップショットをS3に保存、データのプライマリコピーはオンプレミス|
|キャッシュ型ゲートウェイ|オンプレミスのディスクデータスナップショットをS3に保存、**データのプライマリコピーはS3・よく使われるデータのみオンプレミス**|
|テープゲートウェイ|仮想テープライブラリ対応バックアップソフトウェアを利用し、Storage gateway経由でS3に保存|
|ファイルゲートウェイ|S3をオンプレミスのNAS共有ファイルシステムのバックエンドストレージとして使う|

## リバースプロキシ

一般的な用語、[外部からWebサーバーへアクセスされる際、Webサーバーの代替を行って負荷を下げるサービス](https://www.atmarkit.co.jp/ait/articles/1608/25/news034.html)

## [Elastic Load Balancing](https://aws.amazon.com/jp/elasticloadbalancing/)

### ELBの種類

||Application Load Balancer|Network Load Balancer|Classic Load Balancer|
|:--|:--|:--|:--|
|略称|ALB|NLB|CLB|
|機能|リクエストのクエリーからあらかじめ設定されたルーティングに沿って振り分けをする<br>ELB自体が負荷に応じて自動にスケールします|**ロードバランサーのアクセス先をドメイン名ではなく固定IPアドレスで設定できる**<br>宛先IPアドレスをターゲットのIPアドレスに書き換えて転送<br>応答トラフィックはロードバランサーを経由せず直接クライアントに送信される|リクエストのURL毎にロードバランサーを用意して、コンテナサービス上のアプリケーション単位でリクエストを振り分けられる、クライアント・ターゲット間通信はリクエスト・応答共にロードバランサーを経由する|
|コメント|レイヤー7でHTTP/HTTPSを提供、負荷分散など実装|レイヤー4のTCP・レイヤー5のTLSをサポート、固定IPアドレス、応答トラフィックはロードバランサーを経由せずクライアントに直接送るので高パフォーマンス|HTTP/HTTPSを提供しているが旧来のサービス|

### Pre-Warming（暖機運転）

トラフィックの急増が予想される場合事前にELBをスケールしたい場合は、AWSサポートに申請する  
※AWSコンソールからでは対応できない  

## Direct Connect

AWSとオンプレミス間を専用線で接続  

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
|共有型|**2Gbpsの帯域**を提供|
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