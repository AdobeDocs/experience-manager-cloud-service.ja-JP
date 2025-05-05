---
title: Content Credentials の統合
description: AEM Assets に統合され、アセットビュー内に表示される Content Credentials を使用すると、アセットの作成方法や作成に関わったユーザーなど、アセットの履歴に関するコンテキストを提供できます。デジタルコンテンツの栄養ラベルと同様に、Content Credentials は透明性を高め、オーディエンスとの信頼関係を構築するのに役立ちます。
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 94%

---

# Content Credentials {#content-credentials}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

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
   1. **コンテンツの概要：**&#x200B;アセットの一部または全部が AI によって生成されたかどうか、または編集方法を示します。

      ![Content Credentials](/help/assets/assets/content-credentials1.png)
   1. **プロセス**：アセットの生成に使用されたアプリケーション、デバイス、AI ツール（Adobe Firefly など）と、その後に行われた変更について詳しく説明します。

      ![プロセス](/help/assets/assets/CR-Process.png)
   1. **この Content Credentials について：**&#x200B;発行者の名前と発行日時。

      ![発行者](/help/assets/assets/CR-issuer.png)
