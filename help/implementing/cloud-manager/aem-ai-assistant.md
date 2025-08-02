---
title: Adobe Experience Managerの AI アシスタント（Beta）
description: AI アシスタントを使用して回答を見つけ、Adobe Experience Managerで使用可能なソリューションのトラブルシューティングを行います。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 71041c9e4d4afe964f549f193daf8ec72bd97a41
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 2%

---

# Adobe Experience Managerの AI アシスタント {#aem-home}

AEM（Adobe Experience Manager） AI アシスタントは、Adobe Experience Manager関連のクエリに対する回答の検索を合理化するように設計された対話型インターフェイスを提供します。 AEM製品に関する質問に即座に回答したり（*すべてのユーザーが利用できます*）、サポートチケットの自動作成を行ったり（*サポート管理者が利用できます*。

プライベートベータ版では、AEM AI アシスタントは、次のソリューションを含むAEM as a Cloud Serviceをサポートします。

* Sites
* Assets
* Dynamic Media
* Edge Delivery Services
* Cloud Manager
* Forms

AEMに直接埋め込まれ、AEM Experience Hub、Cloud Managerおよびオーサー UI からアクセスできます。

次の 3 分 39 秒のビデオでは、AEM AI アシスタントの手順を順を追って説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3470356?learn=on&captions=jpn)

>[!IMPORTANT]
>Adobeで AI アシスタント機能を有効にしてプライベートベータプログラムをテストし、利用できるようにするため、利用許諾契約書を確認して送信してください。
>
>ご不明な点は、Adobe IDに関連付けられたメールアドレスから [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) までお問い合わせください。

## 範囲 {#scope}

AEM AI アシスタントの現在の対象範囲は、Adobe Experience Manager as a Cloud Serviceの製品ナレッジの問題への対処に重点を置いています。 これには、Sites、Assets、Forms、Edge Delivery Services、Cloud Managerなど、主要な領域に対する包括的なサポートが含まれます。

* **サーフェス**:AEM Experience Hub、オーサー UI、Cloud Managerで使用可能です。
* **機能**：トラブルシューティングとガイダンスのための製品知識とファーストストップ、サポートチケットの自動作成とルックアップ。
* **価値**：時間を節約し、学習と価値を生み出すまでの時間を短縮し、サポートチケットを手動で作成する必要性を減らし、サポートチケットの作成を効率化します。

## プライバシー、セキュリティ、ガバナンス{#privacy-security-governance}

AEM AI アシスタントは、プライバシー、セキュリティ、ガバナンスに重点を置いて設計されています。

この記事では、AEM AI アシスタントに期待できる信頼を中心とした機能の概要を説明します。

* AEM AI アシスタントがトレーニング目的を含め、個人データを使用することはありません。
* AEM AI アシスタントはコンシューマーデータにアクセスできません。
* AEM AI アシスタントとやり取りするには、明示的な権限が必要です。
* ユーザー指定のプロンプト（質問、クエリなど）は、他の顧客と共有されません。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## AEM AI アシスタントの製品知識と自動サポートチケット作成機能について説明します {#ai-prod-insights}

製品知識には、Adobe Experience League ドキュメントから派生した概念とトピックが含まれます。 これらの質問は、次のサブグループに分類できます。


| 製品に関する知識 | すべてのユーザーが利用できる <br> 例 |
| :--- | :--- |
| 先を見越した学習 | <ul><li>ユニバーサルエディターとは</li><li>Cloud Managerでプログラムを作成するにはどうすればよいですか？</li></ul> |
| 検出を開く | <ul><li>ユニバーサルエディターの使用方法</li><li>環境間でコンテンツをコピーする方法はありますか？</li></ul> |
| トラブルシューティング | <ul><li>ユニバーサルエディターにアクセスできないのはなぜですか？</li><li>パイプラインが失敗する理由</li></ul> |
| **サポートチケットの作成** | **管理者のみをサポートできます&#x200B;**<br>**例** |
| AI アシスタントのチャット履歴とコンテキストをキャプチャする自動サポートチケット作成 | <ul><li>サポートチケットを作成する</li></ul> |
| サポートチケットのステータスの取得 | <ul><li>オープンしたサポートチケットを全て見せてください。</li><li>チケット「E---------- –」のステータスを表示</li></ul> |

{style="table-layout:auto"}


## 効果的な質問の作成方法 {#ai-craft-questions}

AEM AI アシスタントから最も正確な回答を受け取るには、質問に明確でコンテキストのあるフレーズを使用することが重要です。 次のヒントを使用して、クエリが明確で適切に構造化されていることを確認します。

* タスクまたは質問を簡潔に明確に述べます。
* あいまいな表現や複雑すぎる構文を避けて、理解を深めます。
* このアプローチは、AEM AI アシスタントがより正確で関連性の高い回答を提供するのに役立つので、タスクや質問に関する関連するコンテキストを含めます。
例えば、プロンプトでは、使用しているAEM ソリューション（Sites、Assets、Dynamic Media、Edge Delivery Services、Cloud Manager、Forms）に名前を付けるのに役立ちます。

### サポートされていない質問の例 {#ai-unsupported-questions}

| 領域 | 例 |
| --- | --- |
| 運用インサイト | <ul><li>テナントに存在する開発環境の数</li><li>最後の実稼動パイプラインを開始したのは誰ですか？</li></ul> |
| トラブルシューティング | <ul><li>実稼動パイプラインが失敗する理由</li></ul> |
| タスクと自動処理 | <ul><li>開発ブランチからコード品質パイプラインを設定します。</li></ul> |


## AEM AI アシスタントの使用 {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AEM AI Assistant access through Admin Console 

To use the AEM AI Assistant, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AEM AI Assistant in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AEM AI Assistant of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### 会話の開始またはリセット

トピックを変更する際には、AEM AI アシスタントをリセットして、新しい会話を開始することができます。 この機能は、失敗したクエリや誤った情報が提供されたクエリのトラブルシューティングを行う場合に特に役立ちます。

![[ 会話を開始 ] ボタン ](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**会話を開始またはリセットするには：**

1. AEM AI アシスタントで、![ 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。
1. 新しいトピックまたはトピックの変更をAEM AI アシスタントに通知するには、「**新しい会話を開始**」をクリックします。

### 検出性を使用

AEM AI アシスタントには、サポートされているトピックとカテゴリを検索するのに役立つ検出機能が含まれています。

![ アイデア電球アイコン ](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**検出性を使用するには：**

1. AEM AI アシスタントの右上隅にある ![ 学ぶアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) をクリックします。
1. カテゴリを選択して、関連するプロンプトのリストを表示します。
1. プロンプトを選択して、AEM AI アシスタントが回答できる質問の種類をより深く理解します。

### AEM AI アシスタントに関するフィードバックを提供する

AEM AI アシスタントのパフォーマンスと精度を向上させるために、入力した情報を使用します。

次のオプションを通じて、AEM AI アシスタントのエクスペリエンスに関するフィードバックをお寄せください。

![ サムズアップ、サムズダウン、フラグアイコン ](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| アイコン | 説明 |
| --- | --- |
| ![ サムズアップアウトインアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | うまくいったことを示したり、肯定的なフィードバックを共有するためにクリックします。 |
| ![ サムズダウンラインアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | クリックして、改善の提案を提供します。 エクスペリエンスに関する特定のコメントを追加し、それを毎日確認します。 |
| ![ フラグアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | クリックして懸念事項を報告するか、AEM AI アシスタントとのやり取りに関する詳細なフィードバックを提供します。 |

## AEM AI アシスタントに関するよくある質問（FAQ） {#ai-faq}

ここでは、AI アシスタントに関するよくある質問に対する回答を示します。

* **AEM AI アシスタントからリアルタイムで提供される情報はありますか？**\
  いいえ。AI Assistant は、Adobe Experience League のドキュメントからコンテンツを入手します。 コンテンツの更新が応答に反映されるまでに時間がかかる場合があります。
* **AEM AI アシスタントがサポートするAdobe アプリケーションは**\
  現在、AI アシスタントは、Sites、Assets、Dynamic Media、Cloud Manager、Formsなど、AEM as a Cloud Serviceでの製品に関する知識の照会をサポートしています。
* **AEM AI アシスタントの機能は何ですか？**\
  AEM AI アシスタントは、Adobe製品の知識に関する質問に回答するように設計されています。
* **AEM AI アシスタントで個人情報がトレーニング データに使用されますか？**\
  いいえ。AEMAI アシスタントは、トレーニング目的で個人情報を使用しません。 名前や連絡先の詳細など、自分自身や他の人に関する個人情報をAEM AI アシスタントと共有しないでください。


## AEM Forms AI アシスタント（Forms Experience Builder） {#ai-forms-builder}

AEMでは、製品の知識のための一般的なAEM AI アシスタントに加えて、専用の **[AEM Forms AI アシスタント（Forms Experience Builder）](/help/edge/docs/forms/forms-ai-assistant.md)** も提供しています。 この拡張アシスタントは、自然言語プロンプトを通じてフォームを作成および設定し、フォームに固有の質問に答えるのに積極的に役立ちます。

### 主な機能

AEM Forms AI アシスタントの主な機能を次に示します。

* **フォームの作成**：自然言語の説明を使用してゼロから新しいフォームを作成する。
* **デザインの読み込み**：既存のデザイン（PDF、Figma、画像）を機能的なAEM Formsに変換する。
* **フォーム設定**：フィールド、パネル、検証ルール、条件付きロジックを追加します。
* **レイアウト管理**：フォーム構造を整理し、異なるデバイス向けに最適化します。
* **統合設定**：フォーム送信とデータ処理を設定する。
* **製品知識**:AEM Formsの機能とベストプラクティスに関する質問に回答します。

### アクセス先

AEM Forms AI アシスタントは次の場所から利用できます。

* **ユニバーサルエディター**：ビジュアル編集機能を備えたEdge Delivery Services フォーム用。
* **アダプティブ Forms エディター**：詳細なフォーム設定と高度な機能のために使用します。
* **Forms Management UI**: フォームの作成および管理タスクの概要を示します。

### はじめに

>[!NOTE]
>
> AEM Forms AI アシスタント（Forms Experience Builder）は、非公開のベータ版プログラムで利用できます。 勤務先のアドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信して、アクセスをリクエストします。

AEM Forms AI アシスタントの使用について詳しくは、[AEM Forms AI アシスタント ](/help/edge/docs/forms/forms-ai-assistant.md) のドキュメントを参照してください。

### 使用例

* **「名前、メール、評価、コメントのフィールドを含んだ顧客フィードバックフォームの作成」**
* **「アップロードしたPDF アプリケーションフォームをデジタルアダプティブフォームに変換する」**
* **「配偶者の有無が「既婚」の場合にのみ配偶者の情報を表示する条件付きロジックを追加」**
* **顧客関係管理システムにデータを送信するためにこのフォームを設定する」**

この特化したAEM Forms AI アシスタントは、AI の機能をAEMの堅牢なフォーム機能と組み合わせて、フォーム作成ワークフローを合理化し、フォーム作成の次の進化を表します。
