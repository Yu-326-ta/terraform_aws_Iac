# terraform_aws_Iac

## 作成するアプリケーション
![MainImage](images/main.png)
![DetailImage](images/main2.png)

## 作成するVPC
### サブネット
作成するサブネットは以下の４つ
* (Pubilc Subnet) 192.168.1.0/24
* (Pubilc Subnet) 192.168.2.0/24
* (Private Subnet) 192.168.3.0/24
* (Private Subnet) 192.168.4.0/24
![subnet](images/subnet.png)

### ルートテーブル
作成するルートテーブルは以下の2つ
* public network
* private network
![routeTable](images/routetable.png)

### 作成するインターネットゲートウェイ
![InternetGateWay](images/internetgateway.png)

## 作成するセキュリティグループ

作成するセキュリティグループは以下の４つ

* Webサーバー用  
  → http/httpsが入ってくる  
  ← TCP3000（アプリケーションサーバー）が出ていく
* APサーバー用  
  → TCP3000が入ってくる  
  ← http/httpsがS3に出ていく  
  ← Mysql向けポート(TCP3306)に出ていく  
*  DBサーバー用  
  → Mysql向けポート(TCP3306)が入ってくる
* 運用管理用  
  → SSHが入ってくる  
  → TCP3000が入ってくる  
  ← HTTP/HTTPSが出ていく

  ![SGImage](images/sg.png)

### プレフィックスリスト
  S3向けのプレフィックスリストを取得

  ![PlefixImage](images/plefix.png)

## 作成するRDS
![RDSImage](images/rds.png)

### パラメータグループ

### オプショングループ

### サブネットグループ

## 作成するEC2 (app server)
* Amazon Linux 2
* パブリックサブネット
* セキュリティグループ（APPサーバ用、運用管理用）
![EC2Image](images/ec2.png)

### AMIの追加

### キーペアの作成

## 作成するIAMロール
![IAMImage](images/iam_role.png)
![session](images/session.png)

### ポリシーの作成
* AmazonSSMManagedInstanceCore = SessionManagerを使った接続
* AmazonS3ReadOnlyAccess = S3からファイル取得
* AmazonEC2ReadOnlyAccess = EC2のタグ情報取得
* AmazonSSMReadOnlyAccess = Parameter storeから環境変数取得

### インスタンスプロフィールの作成

## 作成するEC2(app server)２回目

### ssm_parameterにDB接続先情報を保存

### 手動でamiの作成
![ami](images/ami.png)

## 作成するELB
![elb](images/elb.png)

### ターゲットグループの作成

### リスナーの作成

## Route53の設定
![route53](images/route.png)

### Route53ゾーンの作成
### Route53レコード作成
### ドメインサービス側への登録（手動）

## ACMの設定
![acm](images/acm.png)

### ELBに証明書を設定
![elb](images/elb_cer.png)

## 作成するS3
![s3](images/s3.png)

### EC2のオートスケーリングで参照するためのプライベートバケットの作成

## 作成するCloudFront(オリジンサーバー)
![cloudfront](images/cloudfront.png)

### cacheサーバーの設定
![cache](images/cache.png)