# 連携：AWSソリューションアーキテクトアソシエイト

## [Amazon SNS](https://aws.amazon.com/jp/sns/)

NはNotification  
HTTP/S、Eメール、SQS、Mobile Push、SMS、Lambdaに対応  
SES(Simple Email Service)、SMTPには非対応  

## [Amazon SQS](https://aws.amazon.com/jp/sqs/)

EC2インスタンス間で非同期なジョブ制御に用いる  
透過的に保存データの暗号化ができる  

### SQSにおけるキューの種類

キューは標準キューとFirst In First Out(FIFO)キューが利用できる  

|キュー|標準キュー|FIFOキュー|
|:---|:---|:---|
|配信|ベストエフォート<br>少なくとも1回行われる|メッセージが送信順のとおり配信<br>1回限りで確実に処理される|
|特徴|最大限のスループットが選べる|逐次処理を行うケースで利用|

FIFOキューにおいてメッセージは1回配信されることが保証されている  

## [Amazon Simple Email Service(SES)](https://aws.amazon.com/jp/ses/)

メール配信サービス  
HTTP REST APIもしくはSMTPエンドポイントによりメール送信を行う  
