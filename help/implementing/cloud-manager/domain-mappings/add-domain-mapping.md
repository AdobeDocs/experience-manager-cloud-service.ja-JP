---
title: ドメインマッピングの追加
description: Edge Delivery サイトまたはCloud Manager環境用のドメインマッピングを追加する方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 64%

---


# ドメインマッピングの追加について {#add-domain-mapping}

プログラム内でアドビが管理する CDN の SSL 証明書を持つドメインをリンクするには、CDN（コンテンツ配信ネットワーク）設定を追加する必要があります。

アドビが管理する CDN の場合、DV SSL 証明書を使用する際は、ACME 検証済みのサイトのみが許可されます。

>[!IMPORTANT]
>
>[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)と [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)をそれぞれ行いましたか？そうでない場合は、CDN 設定を追加する前に、これらの 2 つのタスクを完了する必要があります。

詳しくは、[アドビが管理する CDN](https://www.aem.live/docs/byo-cdn-adobe-managed) も参照してください。

**ドメインマッピングを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. ユースケースに応じて、次のいずれかの操作を行います。

   | ユースケース | ステップ |
   | --- | --- |
   | Cloud Manager の&#x200B;*既存*&#x200B;の Edge Delivery サイトに CDN 設定を追加したいと考えている | a. 左側のサイドメニューの&#x200B;**サービス**&#x200B;で、![web ページアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery Sites**」をクリックします。<br>b. Edge Delivery テーブルで、ドメインが関連付けられていない行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。<br>c. 「**CDN を設定**」をクリックします。 |
   | Cloud Manager に CDN 設定を追加したいと考えている | 左側のサイドメニューの&#x200B;**サービス**&#x200B;で、![ソーシャルネットワークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg)「**ドメインマッピング**」をクリックします。<br>b. ドメインマッピングページの右上隅付近にある「**追加**」をクリックします。 |

1. **ドメインを CDN にマッピング** ダイアログボックスで、次のいずれかを選択して、CDN タイプおよび関連する設定を選択します。

   | CDN タイプ | 設定の詳細 |
   | --- | --- |
   | Adobeの管理による CDN （推奨） | **設定の詳細**&#x200B;で、次の操作を行います。<br>a. **ドメイン**&#x200B;ドロップダウンリストで、使用するドメイン名を選択します。<br>ドロップダウンリストに使用可能な検証済みドメインがありませんか？詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。<br>b.<!-- In the **SSL certificate** drop-down list, select a certificate that you want to use.<br>No SSL certificates available in the drop-down list? See [Add an SSL certificate](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).--> |
   | その他 CDN プロバイダー | 使用可能なアドビが管理する CDN ではなく、独自の CDN プロバイダーを使用している場合は、このオプションを選択します。<br>**設定の詳細**&#x200B;の&#x200B;**ドメイン**&#x200B;ドロップダウンリストで、使用するドメイン名を選択します。<br>ドロップダウンリストに使用可能な検証済みドメインがありませんか？詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。 |

   ![Adobeの管理による CDN ラジオボタンが選択されている状態でドメインを CDN にマッピング ダイアログボックス ](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png)

   <!-- OLD IMAGE/UI (/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)-->

1. 「**ドメイン**」フィールドに、提供する顧客向けのホスト名を入力します（例：`www.example.com`）
1. **接触チャネル** ドロップダウンリストで、次のいずれかを選択します。

   | 「接触チャネル」ドロップダウンリスト | 説明 |
   | --- | --- |
   | Sites | Edge Delivery サイトを選択します。 |
   | 環境 | AEM 設定内でターゲットとする特定の Cloud Service 環境を選択します。<br>**層**&#x200B;ドロップダウンリストで、次のいずれかを選択します。<br>• 「**パブリッシュ**」を選択して、コンテンツがエンドユーザーに配信されるライブの本番環境をターゲットにします。<br>• 運用開始前に変更をテストするステージング環境または本番環境以外では、「**プレビュー**」を選択します。 |

1. **設定を保存** をクリックします。

   Adobeでは、ドメインマッピングをテストすることをお勧めします。

## ドメインマッピングのテスト {#test-domain-mapping}

パブリック DNS の伝達を待たずに、Adobeが管理する CDN に新しいドメインマッピングが有効であることを確認できます。

DNS の解決を上書きし、CDN エッジを直接指す **curl** コマンドを実行します。

```bash
curl -svo /dev/null https://www.example.com \
--resolve www.example.com:443:151.101.3.10
```

* `www.example.com` を自分のドメインに置き換えます。
* IP アドレス `151.101.3.10` は、AEM Cloud Service へのアクセスに使用できる IP の 1 つです。 [APEX レコード ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-apex-record) も参照してください。

`--resolve` フラグは、ドメインの証明書とルーティングが正しくインストールされた後にのみ、指定された IP への要求を強制し、成功を返します。

