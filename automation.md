# 自動化：AWSソリューションアーキテクトアソシエイト

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

### [AWS CloudFormationデザイナー](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/working-with-templates-cfn-designer.html)

テンプレートを作成する際にAWSの各種リソース用テンプレートスぺニットなど補助的な機能を使う  
JSON形式やYAML形式で記載  

## [AWS Elastic Beanstalk](https://aws.amazon.com/jp/elasticbeanstalk/)

コードをアップロードしたらAWSが環境構築（プロビジョニング）・運用開始（デプロイ）まで面倒を見てくれる  
Nginx上に構築されたWebアプリケーションもデプロイできる  
自社におけるWebアプリインフラ管理の負荷を下げ、アプリのコード開発へ注力したいときに用いる  

## [AWS OpsWorks](https://aws.amazon.com/jp/opsworks/)

ChefやPuppet（構築手順）どおりにサーバー構築を自動化してくれる  

## AWS CodeCommit

プライベートGitレポジトリでのコード保存
**2024年7月25日をもって新規顧客の受け付けを終了**（既存ユーザーは継続利用可能）
代替としてGitHubやGitLabなどの利用が推奨される

## [AWS CodeBuild](https://aws.amazon.com/jp/codebuild/)

コードのビルドとテスト

## [AWS CodeDeply](https://aws.amazon.com/jp/codedeploy/)

コードデプロイの自動化  
CodeComit（コード保存）→CodeBuild（ビルトとテスト）→CodeDeply（アプリケーションとして展開）とセットで使われることが多い  

## [AWS CodePipeline](https://aws.amazon.com/jp/codepipeline/)

継続的デリバリーを使用したソフトウェアのリリース  
DataPipelineとは異なる  
ビルド、テスト、デプロイなど、リリース作業に必要な一連のプロセスをまとめたもの  

## AWSが提供するコンテナーサービスEKS/ECS

コントロープレーンは、KubernetesとAWS独自のコンテナー管理サービス  

### ECSがサポートしているデータプレーン

EC2とFargate（コンテナーが稼働するサーバーの管理をせずコンテナーを実行できる）


## OptWorks

サーバー構成管理にChefを利用している企業で、レシピやクックブックを再利用し、AWS上でサーバー構成管理の自動化を行うのに用いる
