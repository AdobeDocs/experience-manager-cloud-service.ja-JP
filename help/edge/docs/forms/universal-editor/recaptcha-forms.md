---
title: reCAPTCHA でFormsを保護 – ビジュアルガイド
description: Google reCAPTCHA をEdge Delivery Services フォームに簡単に追加して、スパムやボットの送信を防ぐ方法を説明します
feature: Edge Delivery Services
keywords: フォームの reCAPTCHA、ユニバーサルエディターの reCAPTCHA の使用、フォームの reCAPTCHA の追加、フォームセキュリティ、スパム保護
role: Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 3%

---


# Google reCAPTCHA でFormsをスパムから保護

<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセスをリクエストするには、公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に、GitHub の組織名とリポジトリ名を記載したメールを送信します。</span>



## フォームで reCAPTCHA を使用する理由

| ![セキュリティ](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![ ボットの保護 ](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![ユーザーエクスペリエンス](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **セキュリティの強化** | **ボットおよびスパムの防止** | **シームレスなユーザーエクスペリエンス** |
| 不正行為や悪意のある攻撃からフォームを保護 | 自動ボットが無関係または有害なコンテンツでフォームをあふれさせないようにする | 目に見えない reCAPTCHA は、正当なユーザーを妨げることなく、バックグラウンドで機能します |

例えば、機密性の高い財務情報を含む税金計算フォームは、誤用から保護する必要があります。 reCAPTCHA は、送信が自動システムではなく、正規のユーザーからのものであることを検証します。

## reCAPTCHA ソリューションの選択

Edge Delivery Services Formsは、次の 2 つのGoogle reCAPTCHA オプションをサポートしています。

| ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/enterprise.svg) | ![reCAPTCHA 標準 ](/help/edge/docs/forms/universal-editor/assets/standard.svg) |
|:-------------:|:-------------:|
| [**reCAPTCHA Enterprise**](#set-up-recaptcha-enterprise) | [**reCAPTCHA 標準**](#set-up-recaptcha-standard) |
| 追加機能とカスタマイズを備えた、プレミアムでエンタープライズクラスの不正検出 | バックグラウンドで目に見えないように動作するスコアベースの検出を備えた無料サービス |
| 次の用途に最適：複雑なセキュリティのニーズを持つ大企業 | 最適な用途：基本的な保護ニーズを持つ中小規模プロジェクト |

どちらのオプションも、スコアベースの検出（0.0 ～ 1.0）を使用して、ユーザーエクスペリエンスを中断することなく、人間によるインタラクションとボットによるインタラクションを識別します。

## reCAPTCHA Enterprise の設定

### 手順 1:Google Cloud の資格情報を取得する

reCAPTCHA Enterprise を設定する前に、以下が必要です。

- [ プロジェクト ID](https://support.google.com/googleapi/answer/7014113) が設定された [&#128279;](https://cloud.google.com/recaptcha/docs/prepare-environment?hl=ja#before-you-begin)0&rbrace;Google Cloud プロジェクト
- プロジェクトの [reCAPTCHA Enterprise API 有効 ](https://cloud.google.com/recaptcha/docs/prepare-environment?hl=ja#enable-api)
- 認証用の [API キー ](https://console.cloud.google.com/apis/credentials)
- ドメインの [ サイトキー ](https://console.cloud.google.com/security/recaptcha)

### 手順 2：クラウド設定コンテナの作成

![ クラウド設定のセットアップ手順 ](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. AEM オーサーインスタンスにログインします
2. **ツール**/**一般**/**設定ブラウザー** に移動します。
3. フォームを見つけて、「**プロパティ**」を選択します
4. ダイアログで **クラウド設定** を有効にします
5. 設定を保存して公開します。

### 手順 3:reCAPTCHA エンタープライズサービスの設定

![reCAPTCHA エンタープライズ設定画面 ](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. **ツール**/**クラウドサービス**/**reCAPTCHA** に移動します
2. フォームに移動し、「作成 **をクリックし** す
3. ダイアログで、次の手順を実行します。
   - **ReCAPTCHA Enterprise** バージョンの選択
   - タイトルと名前を入力
   - プロジェクト ID、サイトキー、API キーを追加します
   - **スコアベースのサイトキー** をキータイプとして選択します
   - 人間とボットを区別するしきい値スコア （0-1）を設定
4. **作成** をクリックし、設定を公開します

## reCAPTCHA 標準の設定

### 手順 1:API キーを取得する

開始する前に、Google reCAPTCHA コンソールから [reCAPTCHA API キーペアを取得 ](https://www.google.com/recaptcha/admin) （サイトキーと秘密鍵）します。

>[!IMPORTANT]
>
>Edge Delivery Services Forms では、**reCAPTCHA スコアベース**&#x200B;のバージョンのみをサポートしています。

### 手順 2：クラウド設定コンテナの作成

Enterprise バージョンと同じ手順に従って、クラウド設定コンテナを作成し公開します。

### 手順 3:reCAPTCHA 標準サービスの設定

![reCAPTCHA 標準設定画面 ](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. **ツール**/**クラウドサービス**/**reCAPTCHA** に移動します
2. フォームに移動し、「作成 **をクリックし** す
3. ダイアログで、次の手順を実行します。
   - **ReCAPTCHA v2** バージョンの選択
   - タイトルと名前を入力
   - サイトキーと秘密鍵の追加
4. **作成** をクリックし、設定を公開します

## reCAPTCHA のフォームへの追加

reCAPTCHA を設定したので、次はフォームに追加します。

![reCAPTCHA コンポーネントのフォームへの追加 ](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

1. フォームをユニバーサルエディターで開きます
2. コンテンツツリーのアダプティブフォームセクションに移動します
3. **追加** アイコンをクリックし、アダプティブフォームコンポーネント リストから **Captcha （非表示）** を選択します
   - *または、コンポーネントをフォームにドラッグ&amp;ドロップします*
4. 「**公開**」をクリックして、reCAPTCHA 保護でフォームを更新します

これで、フォームが保護されました。 次の場所で表示します。
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name>`

![reCAPTCHA 保護が有効になっているフォーム ](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## reCAPTCHA 統合の検証

reCAPTCHA をフォームに追加した後、正しく機能していることを確認する必要があります。 実装の検証方法を次に示します。

### 視覚的検証

reCAPTCHA v2 （スコアベース）は目に見えて動作しますが、次の方法で存在を確認できます。

1. **ページソースの検査**：フォームページを右クリックして、「ページのSourceを表示」を選択します
   - サイトキーと共に reCAPTCHA スクリプトを追加する場所を探します
   - 例：`<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>`

2. **ネットワークリクエストの確認**：ブラウザー開発者ツールの使用（F12）
   - フォームを送信し、`google.com/recaptcha` へのネットワークリクエストを探します
   - これらのリクエストは、フォーム上で reCAPTCHA がアクティブであることを示します

### 機能テスト

reCAPTCHA が実際にフォームを保護していることを検証するには：

1. **通常の送信テスト**:
   - フォームに有効なデータを入力します
   - 人間が通常使用するペースでフォームを送信します
   - フォームが正常に送信されたことを確認します

2. **ボット様動作テスト**:
   - フォームを匿名/プライベートブラウジングウィンドウで開きます
   - フォームに素早く入力する（自動タイプの動作）
   - 連続して複数回送信
   - reCAPTCHA が機能している場合、これらの送信はブロックされたりフラグが付けられたりする可能性があります

3. **フォーム送信記録の確認**:
   - フォーム送信データを確認する
   - 各送信には、reCAPTCHA スコアを含める必要があります
   - スコアが 1.0 に近い値は、人間が使用している可能性を示しています
   - スコアが 0.0 に近い場合は、ボットアクティビティの可能性を示します

### Google reCAPTCHA Admin Console の使用

大規模法人ユーザーの場合、Google Cloud Console では詳細な分析を行うことができます。

1. [Google Cloud Console](https://console.cloud.google.com/) に移動します
2. **セキュリティ**/**reCAPTCHA** に移動します
3. サイトキーを選択
4. 評価チャートと統計のレビュー
5. 次を探します。
   - トラフィックパターン
   - スコア配分
   - 潜在的に不正な活動

標準の reCAPTCHA ユーザーの場合、基本的な統計情報は [reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin/) で入手できます。

### 実装の調整

検証結果に基づいて、以下を行います。

- 適切なユーザーがブロックされている場合は、しきい値スコアを下げることを検討します
- まだスパムを受信している場合は、しきい値スコアを増やすことを検討します
- 永続的な問題の場合は、reCAPTCHA の設定を確認し、すべてのキーが正しく入力されていることを確認します

reCAPTCHA は、機械学習を使用して時間の経過と共に改善を図るため、サイトのトラフィックパターンを学習すると、その有効性が高まる可能性があることに注意してください。

## トラブルシューティングと FAQ

| ![ 質問 ](/help/edge/docs/forms/universal-editor/assets/question.svg) | ![回答](/help/edge/docs/forms/universal-editor/assets/answer.svg) |
|:-------------:|:-------------:|
| **reCAPTCHA 設定を作成しない場合はどうなりますか？** | グローバルコンテナ内で設定が検索されます。 何も存在しない場合は、エラーが発生します。 |
| **複数の設定を作成するとどうなりますか？** | 最初に作成した設定が自動的に使用されます。 |
| **公開済みの URL に変更が表示されないのはなぜですか？** | 変更を加えた後は、必ずフォームを再公開してください。 |
| **サポートされている reCAPTCHA サービスはどれですか？** | Edge Delivery Services Formsは、スコアベースの reCAPTCHA サービスのみをサポートします。 |

## 次の手順

reCAPTCHA でフォームを保護したので、

- **実装の検証**:[ 検証手順 ](#-validating-your-recaptcha-integration) に従って、reCAPTCHA が正しく機能していることを確認します
- **パフォーマンスの監視**：疑わしいアクティビティやスコアの分布についてGoogle reCAPTCHA ダッシュボードを定期的に確認します
- **設定の微調整**：セキュリティニーズとユーザーエクスペリエンスのフィードバックに基づいてしきい値スコアを調整します
- **最新情報を入手**:Googleの最新のセキュリティ推奨事項を使用して、reCAPTCHA 実装を最新の状態に保ちます
- **チームの教育**:reCAPTCHA の仕組みと分析の解釈方法に関する知識を共有します
- **フィードバックを収集**：ユーザーエクスペリエンスを監視して、正当なユーザーがブロックされないようにします

効果的なフォーム保護は、定期的な監視と調整を必要とする継続的なプロセスです。


