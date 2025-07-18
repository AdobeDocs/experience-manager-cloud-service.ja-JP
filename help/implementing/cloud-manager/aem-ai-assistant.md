---
title: Adobe Experience Managerの AI アシスタント（プライベートベータ版）
description: Adobe Experience Managerの AI アシスタントを使用すると、回答の検索、トラブルシューティングおよび Sites、Assets、Dynamic Media、Cloud Manager、Formsの探索を行えます。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 0afd74120380c9ae3d02db9fb684189c2f19648f
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 1%

---

# Adobe Experience ManagerのAEM AI アシスタントについて {#aem-home}

AEM（Adobe Experience Manager）の AI アシスタントは、Adobe Experience Manager関連のクエリに対する回答の検索を合理化するように設計された対話型インターフェイスを提供します。 Experience Leagueの製品情報へのアクセス、問題のトラブルシューティングおよび情報探索に役立ちます。 プライベートベータ版プログラム中、AEM AI アシスタントは、Sites、Assets、Dynamic Media、Cloud Manager、FormsなどのAdobe Experience Manager as a Cloud Serviceをサポートします。

>[!IMPORTANT]
>Adobeで AI アシスタント機能を有効にしてプライベートベータプログラムをテストし、利用できるようにするため、利用許諾契約書を確認して送信する必要があります。
>
>ご不明な点は、Adobe IDに関連付けられたメールアドレスから [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) までお問い合わせください。

## プライバシー、セキュリティ、ガバナンス

AEM AI アシスタントは、プライバシー、セキュリティ、ガバナンスに重点を置いて設計されています。

この記事では、AEM AI アシスタントに期待できる信頼を中心とした機能の概要を説明します。

* AEM AI アシスタントがトレーニング目的を含め、個人データを使用することはありません。
* AEM AI アシスタントはコンシューマーデータにアクセスできません。
* AEM AI アシスタントとやり取りするには、明示的な権限が必要です。
* ユーザー指定のプロンプト（質問、クエリなど）は、他の顧客と共有されません。

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->


## AEM AI アシスタントの製品知識を学ぶ {#ai-prod-insights}

製品知識には、Adobe Experience League ドキュメントから派生した概念とトピックが含まれます。 これらの質問は、次のサブグループに分類できます。

| 製品に関する知識 | 例 |
| --- | --- |
| 先を見越した学習 | <ul><li>ユニバーサルエディターとは</li><li>Cloud Managerでプログラムを作成するにはどうすればよいですか？</li></ul> |
| 検出を開く | <ul><li>ユニバーサルエディターの使用方法</li><li>環境間でコンテンツをコピーする方法はありますか？</li></ul> |
| トラブルシューティング | <ul><li>ユニバーサルエディターにアクセスできないのはなぜですか？</li><li>パイプラインが失敗する理由</li></ul> |

AEM AI アシスタントの現在の対象範囲は、Adobe Experience Manager as a Cloud Serviceの製品ナレッジの問題への対処に重点を置いています。 これには、Sites、Assets、Forms、Cloud Managerなど、主要な領域に対する包括的なサポートが含まれます。

## 効果的な質問の作成方法 {#ai-craft-questions}

AEM AI アシスタントから最も正確な回答を受け取るには、質問に明確なコンテキストでフレーズを使用することが重要です。 次のヒントを使用して、クエリが明確で適切に構造化されていることを確認します。

* タスクまたは質問を簡潔に明確に述べます。
* あいまいな表現や複雑すぎる構文を避けて、理解を深めます。
* このアプローチは、AEM AI アシスタントがより正確で関連性の高い回答を提供するのに役立つので、タスクや質問に関する関連するコンテキストを含めます。
例えば、プロンプトでは、使用しているAEM ソリューション（Sites、Assets、Dynamic Media、Cloud Manager、Forms）に名前を付けるのに役立ちます。

### サポートされていない質問の例 {#ai-unsupported-questions}

| 領域グラフ | 例 |
| --- | --- |
| 運用インサイト | <ul><li>テナントに存在する開発環境の数</li><li>最後の実稼動パイプラインを開始したのは誰ですか？</li></ul> |
| トラブルシューティング | <ul><li>実稼動パイプラインが失敗する理由</li></ul> |
| タスクと自動処理 | <ul><li>開発ブランチからコード品質パイプラインを設定します。</li></ul> |


## AEM AI アシスタントの使用 {#ai-use}

### Admin Consoleを使用してAEM AI アシスタントのアクセスを有効にする

AEM AI アシスタントを使用するには、Admin Console レベルでオプトインする必要があります。 製品管理者がユーザーグループを作成（または選択）し、新しい「AI アシスタント」権限を付与します。 そのグループに追加されたユーザーは誰でも、AEM全体でアシスタントにすぐにアクセスできます。 企業全体での可用性が目標の場合、管理者はそのグループにすべてのユーザーを割り当てるだけです。

![Admin ConsoleのAEM AI アシスタント ](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

従業員の観点からは、組織内のAdobe Experience Managerの製品管理者を特定して、AI 対応のユーザーグループに追加するようリクエストするプロセスは簡単です。 そのグループに表示されると、次回ログインしたときにアシスタント アイコンが自動的に表示されます。

管理者は、通常のCloud Manager ガバナンスを念頭に置く必要があります。 プロファイルの作成、ユーザーグループの管理、権限の編集を行うには、Admin Consoleの製品管理者権限を保持している必要があります。 ユーザーがアシスタントの組み込みの **サポートチケットを作成** 機能も必要な場合は、同じ個人またはグループに標準の **サポート管理者** ロール（標準のAdmin Console ロール）を追加します。

![Admin ConsoleのAEM AI アシスタントでのテクニカルサポートチケットの作成 ](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

AEM as a Cloud Serviceでのユーザーとグループの設定に関するガイド付きのチュートリアルについては、[AEM as a Cloud Serviceへのアクセスの設定 ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/accessing/overview) を参照してください。

[ カスタム権限 ](/help/implementing/cloud-manager/custom-permissions.md) も参照してください。


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
