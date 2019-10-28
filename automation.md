# 自動化：AWSソリューションアーキテクトアソシエイト

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

## AWSが提供するコンテナーサービスEKS/ECS

コントロープレーンは、KubernetesとAWS独自のコンテナー管理サービス  

## OptWorks

サーバー構成管理にChefを利用している企業で、レシピやクックブックを再利用し、AWS上でサーバー構成管理の自動化を行うのに用いる
