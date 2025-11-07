# AWS アーキテクチャ構成図サンプル

## 概要

このリポジトリでは、**AWSベストプラクティスを意識した構成図のサンプル**を公開しています。  
実務経験を活かし、可用性・セキュリティ・運用性を考慮した設計を draw.io 形式で作成しました。

## 📁 収録構成図

### 1. Personal Study 1 AWS Best Practices Configuration Diagram Sample.drawio
**学習用：AWSベストプラクティス構成図サンプル**

![Personal Study 1](https://img.shields.io/badge/Status-Learning%20Project-blue)

- **目的**: AWSのベストプラクティスに基づいた標準的な構成の学習と理解
- **主要な構成要素**:
  - Multi-AZ構成（ap-northeast-1a、1c、1d）
  - VPC、Public/Private Subnet
  - NAT Gateway、Internet Gateway
  - Route Table、VPC Endpoints
  - セキュリティグループ設計

- **想定シナリオ**: 一般的なWebアプリケーションの可用性・セキュリティを考慮した基本構成

---

### 2. Project 1 AWS migration support sample for web applications.drawio
**プロジェクト1：Webアプリケーション AWS移行支援サンプル**

![Project 1](https://img.shields.io/badge/Status-Sample%20Project-green)

- **目的**: オンプレミスからAWSへのWebアプリケーション移行を想定した構成設計
- **主要な構成要素**:
  - Multi-AZ構成（ap-northeast-1a、1c）
  - VPC、Public/Private Subnet
  - ELB、EC2、RDS
  - NAT Gateway、Internet Gateway
  - VPC Endpoints（S3、その他AWSサービス連携用）
  - Route Table設計

- **想定シナリオ**: 既存のWebアプリケーションをAWSに移行する際の標準的なアーキテクチャ
- **考慮点**:
  - 高可用性：Multi-AZ構成によるダウンタイム削減
  - セキュリティ：Private SubnetでのDB配置、適切なSG設計
  - 拡張性：Auto Scalingを見越した構成

---

### 3. Project 2 AWS migration and standardization sample for on-premise servers.drawio
**プロジェクト2：オンプレミスサーバー AWS移行・標準化サンプル**

![Project 2](https://img.shields.io/badge/Status-Sample%20Project-green)

- **目的**: オンプレミスサーバーのAWS移行と環境標準化を想定した構成設計
- **主要な構成要素**:
  - **On-Premisesネットワーク**（Firewall、Router、Switch、PC、Users）
  - **AWS環境**:
    - Multi-AZ構成
    - VPN/Direct Connect接続想定
    - VPC、Public/Private Subnet
    - セキュリティグループ・NACL設計

- **想定シナリオ**: オンプレミス環境からAWSへのハイブリッドクラウド移行
- **考慮点**:
  - ハイブリッド接続：オンプレとAWSのセキュアな接続
  - 段階的移行：既存環境を維持しながらのクラウド化
  - 標準化：AWS環境でのネットワーク・セキュリティ標準の確立

---

## 🎯 作成意図

これらの構成図は、以下の観点を意識して作成しています：

### ✅ 可用性（Availability）
- Multi-AZ構成による冗長化
- 単一障害点の排除
- Auto Scaling / ELBによる負荷分散

### ✅ セキュリティ（Security）
- Public/Private Subnetの適切な分離
- セキュリティグループ・NACLによる多層防御
- VPC Endpointsによるプライベート接続
- 最小権限の原則に基づいたIAM設計

### ✅ 運用性（Operability）
- CloudWatch等による監視設計
- ログ集約・分析基盤
- バックアップ・リカバリ戦略
- コスト最適化を考慮した構成

### ✅ パフォーマンス（Performance）
- 適切なインスタンスタイプ選定
- キャッシュ戦略（CloudFront、ElastiCache等）
- DB最適化（RDS Multi-AZ、Read Replica等）

---

## 🛠️ 使用ツール

- **draw.io (diagrams.net)**: 構成図作成ツール
  - 無料で使えるオープンソースのダイアグラムツール
  - AWSアイコンライブラリ対応
  - デスクトップ版・Web版どちらでも編集可能

---

## 📖 閲覧方法

### オンラインで閲覧
1. [draw.io](https://app.diagrams.net/) にアクセス
2. 「File」→「Open from」→「Device」を選択
3. このリポジトリからダウンロードした `.drawio` ファイルを開く

### ローカルで閲覧
1. [draw.io Desktop版](https://github.com/jgraph/drawio-desktop/releases) をインストール
2. `.drawio` ファイルをダブルクリックで開く

---

## 🔗 関連リポジトリ

以下のリポジトリでは、実際のインフラコードや自動化スクリプトを公開しています：

- [cloudformation](https://github.com/hamasoron/cloudformation) - CloudFormationによるAWSリソース構築
- [python/secretsmanager-rotation](https://github.com/hamasoron/python/tree/main/secretsmanager-rotation) - Secrets Manager自動ローテーション（Lambda）
- [srep1](https://github.com/hamasoron/srep1) - Terraform + GitHub ActionsによるWebアプリケーション構築

---

## 📝 ライセンス

このリポジトリの構成図は学習・参考目的で自由にご利用いただけます。  
商用利用の際は事前にご連絡いただけると幸いです。

---

## 📧 お問い合わせ

ご質問・ご意見がありましたら、Issueまたはプルリクエストでお気軽にご連絡ください。

---

**作成者**: hamasoron  
**最終更新**: 2025年11月

