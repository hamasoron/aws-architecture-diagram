# Project 1: AWS Migration Support Sample for Web Applications

## 概要

オンプレミスからAWSへのWebアプリケーション移行を想定した構成設計のサンプルです。

## 構成図

### プレビュー
![Web Application Migration Architecture](architecture-diagram.png)

### ファイル
- `Project 1 AWS migration support sample for web applications.drawio` - draw.io編集可能ファイル
- `architecture-diagram.png` - PNG画像ファイル

## 主要な構成要素

### ネットワーク構成
- **Region**: ap-northeast-1（東京リージョン）
- **Availability Zones**: 2つのAZ（1a、1c）でMulti-AZ構成
- **VPC**: 独自のプライベートネットワーク空間
- **Public Subnet**: ALB/NLB配置用（各AZに配置）
- **Private Subnet**: アプリケーションとDB配置用（各AZに配置）

### コンピューティング
- **ELB (Elastic Load Balancer)**: 負荷分散とヘルスチェック
- **EC2**: Webサーバー・アプリケーションサーバー（Auto Scaling対応）
- **RDS (Multi-AZ)**: マネージドデータベース（自動フェイルオーバー対応）

### ネットワーク・セキュリティ
- **Internet Gateway**: インターネット接続
- **NAT Gateway**: Private Subnetからのアウトバウンド通信
- **VPC Endpoints**: S3やその他AWSサービスへのプライベート接続
- **Security Group**: きめ細かいアクセス制御

## 想定シナリオ

既存のWebアプリケーションをオンプレミスからAWSに移行する際の標準的なアーキテクチャです。

### 移行対象システム例
- ECサイト
- 社内業務システム（Web版）
- SaaS型Webアプリケーション
- コンテンツ管理システム（CMS）

### 移行フェーズ
1. **Assessment（評価）**: 現行システムの分析
2. **Migration（移行）**: Lift and Shift または Re-platform
3. **Optimization（最適化）**: AWS最適化、Auto Scaling等の導入

## 設計のポイント

### ✅ 高可用性
- Multi-AZ構成による冗長化
- ELBによる自動負荷分散とヘルスチェック
- RDS Multi-AZによるDBの自動フェイルオーバー
- 複数EC2インスタンスによる可用性確保

### ✅ セキュリティ
- **ネットワーク分離**: Public/Private Subnetの明確な分離
- **最小権限の原則**: Security Groupで必要最小限の通信のみ許可
- **データ保護**: RDSの暗号化、バックアップ自動取得
- **プライベート接続**: VPC EndpointsでS3等へセキュアにアクセス

### ✅ パフォーマンス
- ELBによる効率的な負荷分散
- RDS Read Replicaによる読み取りパフォーマンス向上（オプション）
- CloudFront（CDN）によるコンテンツ配信の高速化（オプション）

### ✅ 拡張性
- **Auto Scaling**: トラフィック変動に応じた自動スケーリング
- **ELB**: 新規インスタンスの自動追加・削除
- **RDS**: ストレージ自動拡張機能

### ✅ コスト最適化
- Reserved Instancesによるコスト削減（本番環境）
- Auto Scalingによる適正なリソース利用
- VPC Endpointsによるデータ転送コスト削減

## 移行戦略

### 1. Lift and Shift（リフト＆シフト）
- オンプレミスのVMをそのままEC2に移行
- AWS Application Migration Service（MGN）の活用
- 最小限の変更で迅速に移行

### 2. Re-platform（リプラットフォーム）
- 一部をAWSマネージドサービスに置き換え
- 例: 自己管理DBからRDSへ移行
- OS・ミドルウェアの最新化

### 3. 段階的移行
- まずステージング環境をAWSに構築
- 動作確認後、本番環境を移行
- DNS切り替えによるダウンタイム最小化

## 運用設計のポイント

### 監視・ログ
- **CloudWatch**: メトリクス監視、アラート設定
- **CloudWatch Logs**: アプリケーションログの集約
- **CloudTrail**: API操作の監査ログ

### バックアップ・リカバリ
- RDS自動バックアップ（ポイントインタイムリカバリ）
- EC2のAMI定期取得
- S3データのバージョニング・ライフサイクル管理

### CI/CD
- AWS CodePipeline / CodeDeploy によるデプロイ自動化
- Blue/Greenデプロイメント対応

## 想定コスト（参考）

月額概算（中規模Webアプリケーション想定）:
- EC2 (t3.medium × 4台): 約 ¥20,000
- RDS (db.t3.medium Multi-AZ): 約 ¥30,000
- ALB: 約 ¥3,000
- NAT Gateway: 約 ¥5,000
- その他（データ転送等）: 約 ¥5,000

**合計: 約 ¥63,000/月**

※実際のコストは利用状況により変動します

## 参考リンク

- [AWS Migration Hub](https://aws.amazon.com/jp/migration-hub/)
- [AWS Application Migration Service](https://aws.amazon.com/jp/application-migration-service/)
- [AWS クラウド移行ガイド](https://aws.amazon.com/jp/cloud-migration/)

