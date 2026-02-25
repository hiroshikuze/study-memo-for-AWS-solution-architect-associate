# 解析：AWSソリューションアーキテクトアソシエイト

## [Amazon Kinesis](https://aws.amazon.com/jp/kinesis/)

ストリーミング処理

|種類|内容|
|:---|:---|
|[Amazon Managed Service for Apache Flink](https://aws.amazon.com/jp/managed-service-apache-flink/)（旧：Kinesis Data Analytics）|リアルタイム分析、ストリーミングデータに対してSQLクエリが実行できる|
|[Kinesis Data Streams](https://aws.amazon.com/jp/kinesis/data-streams/)|ストリーミングデータをリアルタイムで保存できる、EMRやLambdaなどへ連携処理|
|[Amazon Data Firehose](https://aws.amazon.com/jp/firehose/)（旧：Kinesis Data Firehose）|S3・Redshiftなどへ配信|
|[Kinesis Video Streams](https://aws.amazon.com/jp/kinesis/video-streams/)|カメラ・ビデオを取り込んで解析可能にする|

## [CloudWatch](https://aws.amazon.com/jp/cloudwatch/)

EC2で稼動しているLinuxのログも取得できる  

標準メトリックスで収集可能なのは以下などの項目  

* CPU使用率
* インスタンスストアボリュームより読み取られたバイト数
* ネットワークインターフェイスから受信されたバイト数

カスタムメトリクスが必要なのは以下のような項目  

* メモリ使用率
* ディスク使用率はカスタムメトリクスの使用が必要  

EC2の障害を管理担当者に通知するには、**EC2にCloudWatchエージェントをインストールすることでカスタムログをCloudWatch Logsに配信する**  
そしてCloudWatch Logsのメトリックスフィルターで監視する文字列を設定し、SNSからアラートを送信する  

MFAについてIAMユーザーで有効化されていないものがいないか、アクセスキーのローテートを満たしていないユーザーを検出するには、IAMのユーザー一覧で確認するか、もしくはCloudTrailでユーザーのアクティビティログを確認する  

CloudWatch AlarmはClowdWatchの通知機能で、ログをフィルターすることはできない  

## [AWS CloudTrail](https://aws.amazon.com/jp/cloudtrail/)

AWS API・すべてのアクティビティのログを記録する  
EC2で動かしているサーバー内部ログは取得出来ない  
セキュリティグループが変更されたときに個別にEメールによる通知が必要な場合、CloudTrailにCloudWatch LogsとSNSを組み合わせる  
（※AWS Configではユーザーのアクティビティログは取得できない）

## [Amazon EMR](https://aws.amazon.com/jp/emr/)

[Apache Spark](https://www.atmarkit.co.jp/ait/articles/1608/24/news014.html)や[Apache Hadoop](http://hadoop.apache.jp/)を用いて膨大なデータを迅速かつ高効率で分析するサービス
