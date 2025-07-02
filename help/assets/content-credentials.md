---
title: Content Credentials の統合
description: AEM Assets に統合され、アセットビュー内に表示される Content Credentials を使用すると、アセットの作成方法や作成に関わったユーザーなど、アセットの履歴に関するコンテキストを提供できます。デジタルコンテンツの栄養ラベルと同様に、Content Credentials は透明性を高め、オーディエンスとの信頼関係を構築するのに役立ちます。
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: fb7ce7dbb58be9fef5ab087441457770828d73c8
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 100%

---

# Content Credentials {#content-credentials}

ブランドは、コンテンツの透明性、AI の開示、アセットの改ざん防止について、これまで以上に関心を寄せています。アドビのコンテンツ認証イニシアチブ（CAI）は、[Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model)（C2PA）技術標準に準拠したツールを作成しています。新しい種類の暗号化された改ざん防止メタデータである Content Credentials は、閲覧者がコンテンツの系統を理解し、ブランドアセットの整合性を確保するのに役立ちます。これらには、デジタルアセットの履歴に関するインサイトを提供する様々な来歴データを含めることができます。

この情報には次が含まれる場合があります。

* **発行者または署名者：**&#x200B;アセットを認証または署名するためにデジタル署名を発行したエンティティまたは会社に関する情報。
* **発行日：** Content Credentials がアセットに適用された日付。
* **クレジットと使用状況：**&#x200B;名前、ソーシャルメディアのハンドル、その他の ID 関連情報など、アセットのプロデューサーに関する情報。
* **プロセス：**&#x200B;アセットに対して行われた編集または変更の記録。
* **デバイスの詳細：**&#x200B;アセットの作成または編集に使用されたアプリまたはデバイスに関する情報。
* **使用された AI ツール：**&#x200B;アセットの編集または作成に生成 AI を使用した場合、使用されたモデルの名前が含まれることがあります。
* **その他の関連情報：**&#x200B;アセットの履歴に関する詳細なコンテキストを提供するために、追加データも含まれる場合があります。

完全なビューを得るために、[Verify](https://contentcredentials.org/verify) ではアセット履歴に関するより包括的なインサイトを提供できます。

Adobe Experience Manager Assets は Content Credentials をサポートするようになり、ユーザーは AEM のアセットビュー内で Content Credentials を直接確認できるようになりました。アセットの詳細を確認すると、Content Credentials を持つ画像（生成 AI サービスで作成されたイメージなど）では、専用のパネルにマニフェストの詳細が表示されます。アセットをダウンロード、公開、または共有した場合、Content Credentials はアセットと共にそのまま残ります。

![アセット](/help/assets/assets/content-credentials.png)

## Content Credentials へのアクセス {#access-content-credentials}

1. アセットビュー UI に移動し、左側のパネルから「**アセット**」をクリックします。
1. フォルダーに移動して、目的のアセットを選択します。
1. 「**詳細**」をクリックして、右端のパネルから「`Cr pin`」を選択します。「Content Credentials」タブには、アセットに関する次の情報が表示されます。
   1. **生成された画像**：Content Credentials が適用された日時。
   1. **コンテンツの概要：**アセットの一部または全部が AI によって生成されたかどうか、または編集方法を示します。
      ![Content Credentials](/help/assets/assets/content-credentials1.png)
   1. **プロセス**：アセットの生成に使用されたアプリケーション、デバイス、AI ツール（Adobe Firefly など）と、その後に行われた変更について詳しく説明します。
      ![プロセス](/help/assets/assets/CR-Process.png)
   1. **この Content Credentials について：**発行者の名前と発行日時。
      ![発行者](/help/assets/assets/CR-issuer.png)
