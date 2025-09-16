---
title: Forms Experience Builder
description: フォームフラグメントを使用した強力なフォームの迅速な作成
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 6bbec984e1e22764c762d95ff52ae1f474c6b413
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 41%

---


# Forms Experience Builder の概要

>[!IMPORTANT]
>
> **ドキュメントは変更される場合があります**：このドキュメントは現在製品に対してテスト中であり、更新および改訂される可能性があります。早期導入プログラム期間中、Forms Experience Builder は継続的に改良されるので、機能、コマンド、例が変更される場合があります。

AEM Forms Experience Builder は、ジェネレーティブ AI の機能を活用して、デジタルフォームエクスペリエンスの作成と更新を民主化および迅速化します。 自然言語とのやり取りを通じてインテントベースのワークフローを実現することで、ユーザーはフォームを迅速かつシンプルにシームレスに設計、変更、最適化できるようになります。

最新の web テクノロジーに基づき、高度な AI サービスを活用した Forms Experience Builder を使用すると、技術ユーザーとそれ以外のユーザーの両方が、対話型インターフェイスを通じて洗練されたプロフェッショナル向けのフォームを作成できます。この革新的なアプローチにより、価値創出までの時間を数日から数時間に短縮し、インターフェイスのシンプルさを通じて技術的な障壁を排除し、フォームエコシステム全体で最新化の取り組みを拡大します。

## コア機能

Forms Experience Builder には、強力なデジタルフォームを作成するための 2 つの主なワークフローが用意されています。

### &#x200B;1. AI を活用したフォームの作成

**自然言語フォーム生成**

わかりやすい英語の説明を使用して、完全なフォームをゼロから作成します。「評価スケールとコメントフィールドを含んだカスタマーフィードバックフォームを作成する」などの要件を記述するだけで、Forms Experience Builder が適切なフォーム構造を生成します。 ビジュアルエディターの experience builder を使用して、フィールド、検証ルールおよび送信ロジックをさらに追加します。

**Dynamic Tag Management**

対話型コマンドを使用してフォームフィールドを追加、変更または削除します。AI はコンテキストを理解し、要件に基づいてフィールドタイプ、検証ルール、ユーザーインターフェイスの改善をインテリジェントに提案できます。

**レイアウト最適化**

自然言語を通じてフォームのレイアウトと設定を更新します。「フォームレイアウトをウィザードレイアウトに変更」などの変更内容をリクエストし、Forms Experience Builder が適切なスタイルとレイアウトの調整を適用します。

**包括的な送信アクションの設定**

既存のビジネスシステムと統合するようにフォーム送信を設定します。

- **メール統合**：自動メール通知と確認を設定します
- **REST API エンドポイント**：カスタムアプリケーションおよびサービスに接続します
- **クラウドストレージ**： Azure Blob Storage、SharePoint、OneDrive と統合します
- **ワークフロー自動化**：Power Automate および Workfront Fusion に接続します
- **マーケティングプラットフォーム**：リード管理のために Marketo と直接統合します
- **AEM ワークフロー**：既存の AEM ワークフロー機能を活用します

### 2.インテリジェントなインポートと変換

**サポートされている読み込み形式**

既存のフォームとドキュメントをインタラクティブなデジタルエクスペリエンスに変換します。 Forms Experience Builder は、次の項目をサポートしています。

- **Acroforms**：既存のフィールド構造を持つインタラクティブなPDF forms
- **XFA PDF**：複雑な XML ベースのフォームアーキテクチャ
- **フラット PDF**：静的ドキュメントをインタラクティブ Forms に変換する
- **画像とスクリーンショット**:JPG、PNG 形式（サイズ制限についてはチームに確認してください）
- **手描きForms**：スケッチと紙のフォーム写真


**インテリジェント変換プロセス**

アップロードされたコンテンツは、次の目的で分析されます。

- フィールドのタイプと関係の検出
- レイアウトを可能な限り保持する
- 最新のレスポンシブデザインによる機能強化
- 高度な検証と条件付きロジックの追加
- アクセシビリティおよびモバイルエクスペリエンス向けに最適化

## 仕組み

Forms Experience Builder は、シンプルな対話型のアプローチに従います。

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │1. 説明    │───▶│2. AI が │───▶│ 3 を作成します。 絞り込み&amp;    フォームを │
    │ きます      │    │ の最初のフォーム   │    │ Configure      │
    │ 要件   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       「ローン申し込みフォームを作成」フォームに関連する→ールを ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │ きます                  │
    │ 「メールフィールドを追加」           → フィールドと基本                          検証ルールの「Set value of email filed to @firstname@gmail.com」を │
    │→します   │
    └───────────────────────────────────────────────────────────────────────────┘

## シナリオの例

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">PDF forms をデジタルフォームに変換</p>
                    <p class="is-size-6">Acroforms、XFA PDF、フラットなPDF ドキュメントを、機能を強化した、レスポンシブなインタラクティブなデジタルフォームに変換する。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">従来の XFA Formsを最新化</p>
                    <p class="is-size-6">ユーザーワークフローを改善して、複雑な XFA アプリケーションを最新のアクセス可能なデジタルエクスペリエンスに変換します。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">スクリーンショットのデジタルFormsへの変換</p>
                    <p class="is-size-6">画像、スクリーンショット、手描きのフォームを、完全に機能するデジタルエクスペリエンスに変換します。</p>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- #### Import and Enhance Web Forms

Import existing HTML forms and enhance them with advanced features while preserving existing functionality.

**Key benefits:**

- Advanced validation and business logic
- Conditional field behaviors
- Multi-channel submission options
- Enhanced user experience design -->

## Forms Experience Builder と従来の開発の比較

| 項目 | 従来のフォーム作成 | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **作成にかかる時間** | 2～3 日 | 2～3 時間 |
| **技術的知識** | 必須 | 必須ではありません |
| **検証ルール** | 手動コーディング | 自然言語 |
| **アクセシビリティ** | 手動での実装 | ビルトインコンプライアンス |


## 組織にとってのメリット

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">民主化されたフォーム作成</p>
                    <p class="is-size-6">技術に詳しくないユーザーが、自然言語に関する会話を通じて、プログラミングの知識がなくても高度なフォームを作成できるようにします。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">価値創出までの時間（TTV）の短縮</p>
                    <p class="is-size-6">フォーム開発を数日から数時間へと大幅に高速化し、デジタルイニシアティブの迅速な市場投入を可能にします。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">インターフェイスのシンプルさ</p>
                    <p class="is-size-6">直感的な会話型インターフェイスにより学習曲線をなくし、トレーニング時間を短縮して採用を増やします。</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">最新化の取り組みの拡大</p>
                    <p class="is-size-6">レガシーフォームポートフォリオを効率的に最新化し、ビジネスロジックを維持し、フォームエコシステム全体でのユーザーエクスペリエンスを強化します。</p>
                </div>
            </div>
        </div>
    </div>
</div>

## オンボーディング

Forms Experience Builder は現在、早期アクセス（EA）プログラムの一部として利用できます。参加してアクセスするには、次の情報が必要です：

### 必要な情報

- **IMS 組織 ID**:Adobeの組織識別子
- **プログラム ID**:Adobe Experience Cloud内の固有のプログラム ID
- **プロジェクト詳細**：タイムライン、範囲、意図されたユースケース
- **仕事用の公式メール**：組織のAdobe アカウントに関連付けられています


### IMS 組織 ID とプログラム ID の取得方法

IMS 組織 ID とプログラム ID を見つける詳細な手順については、以下を参照してください。

- [Adobe Experience Cloud組織セットアップガイド](/help/onboarding/cloud-manager-introduction.md)
- [プログラムと環境の管理](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### アクセスをリクエスト

1. 上記のガイドを使用して、IMS 組織 ID とプログラム ID を収集します
2. [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にアクセスを要求するメールを送信
3. リクエストに含める：
   - 組織名と IMS 組織 ID
   - プログラム ID
   - プロジェクトのタイムラインと範囲
   - 使用目的と事業目的

>[!IMPORTANT]
>
> **限定提供プログラム**:Forms Experience Builder へのアクセスは、内部の関係者の承認が必要です。 Adobeは、プログラムの処理能力と早期アクセス基準との整合性に基づいて、リクエストをレビューします。 承認は保証されず、現在のプログラムの可用性によって異なります。

早期アクセスプログラムとその機能について詳しくは、[AEM Forms 早期アクセスドキュメント](/help/forms/early-access-ea-features.md)を参照してください。


## はじめに

Forms Experience Builder の使用を開始するには、[Forms Experience Builder ドキュメント](forms-ai-assistant-getting-started.md)を参照してください。Forms Experience Builder には、好みのワークフローに応じて、AEM Forms エディターまたはユニバーサルエディターからアクセスできます。

フォーム作成プロセスの変革を目指す組織のために、Forms Experience Builder は、対話型 AI の柔軟性とエンタープライズクラスのフォーム管理の堅牢性を組み合わせた、強力で直感的なソリューションを提供します。
