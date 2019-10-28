# 管理：AWSソリューションアーキテクトアソシエイト

## [AWS CLI](https://aws.amazon.com/jp/cli/)

コマンド操作できる  
アクセスIDとシークレットキーで操作できる  
IAMポリシーは認証に不要  

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

### [AWS CloudFormationデザイナー](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/working-with-templates-cfn-designer.html)

テンプレートを作成する際にAWSの各種リソース用テンプレートスぺニットなど補助的な機能を使う  
JSON形式やYAML形式で記載  

## [AWS Elastic Beanstalk](https://aws.amazon.com/jp/elasticbeanstalk/)

コードをアップロードしたらAWSが環境構築（プロビジョニング）・運用開始（デプロイ）まで面倒を見てくれる  
Nginx上に構築されたWebアプリケーションもデプロイできる  
自社におけるWebアプリインフラ管理の負荷を下げ、アプリのコード開発へ注力したいときに用いる  

## [AWS OpsWorks](https://aws.amazon.com/jp/opsworks/)

ChefやPuppet（構築手順）どおりにサーバー構築を自動化してくれる  

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

## [AWS Artifact](https://aws.amazon.com/jp/artifact/)

AWS上のコンプライアンスレポートへのオンデマンドアクセス

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

## SWF (Amazon Simple Workflow Service)

ひとかたまりの処理に関する状態管理とタスク間の流れ（＝ワークフロー）の管理を行う  
Ruby/Java/.NET/PHPなどに対応している、Pythonは非対応  

## タグ

部門や環境ごとに費用を確認するのなどに用いる

## Active Directory

* [Directory Service Simple AD](https://docs.aws.amazon.com/ja_jp/directoryservice/latest/admin-guide/directory_simple_ad.html)  
既存のActive Directoryとは連携できない  
Amazon EC2インスタンスの管理やWindowsアプリケーションのデプロイに用いる  

* Directory Service AD Connector  
既存のオンプレミスActive Directoryと連携できる、**認証をリダイレクトしてIAMロールで設定されたアクセス権限をADユーザーに与える**

## 管理者の退職

1. ルートユーザーのMFAデバイスを新しい管理者が引き継ぎ、パスワード変更

1. 旧管理者のIAMユーザーを削除

1. 旧管理者がルートユーザーのアクセスキー有していたら削除する  
（そもそもルートユーザーがアクセスキーを所有することを推奨していない）
