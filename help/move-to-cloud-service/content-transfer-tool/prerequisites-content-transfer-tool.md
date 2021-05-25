---
title: コンテンツ転送ツールの前提条件
description: コンテンツ転送ツールの前提条件
source-git-commit: f70959efd9d0382c083ac05b9ccd63cf79947bc2
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 1%

---

# コンテンツ転送ツールの前提条件 {#prerequisites}

次の表に、コンテンツ転送ツールを使用するための前提条件を示します。

以下に示すすべての考慮事項を確認してください。

| 検討事項 | 現在サポートされている内容 |
|--- |--- |
| AEM のバージョン | コンテンツ転送ツールは、AEM 6.3以降のバージョンでのみ実行できます。 AEM 6.2以前のバージョンでコンテンツ転送ツールを使用するには、コンテンツリポジトリをAEM 6.5にインプレースアップグレードする必要があります。 このためにコードをAEM 6.5にアップグレードする必要はありません。 |
| セグメントストアのサイズ | コンテンツ転送ツールは、現在、*オーサー*&#x200B;では最大83 GBをサポートし、*パブリッシュ*&#x200B;では最大31 GBをサポートしています。 |
| コンテンツリポジトリの合計サイズ&#x200B;<br>*（コンテンツストア+データストア）* | コンテンツ転送ツールは、最大10 TBのコンテンツを転送するように設計されています。 10 TBを超える値は、現在はサポートされていません。 10 TBを超えるコンテンツのオプションについて話し合うために、Adobeカスタマーケアとサポートチケットを作成します。 |
| 不変パスのコンテンツ | コンテンツ転送ツールは、`“/etc”`などの不変パスのコンテンツを移行する際には機能しません。 <br>リポジトリの再構 [築とワークフ](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) ローモデルについて詳しくは、「共通リポジトリの再構築」を参照してください。 |

## 次の手順{#whats-next}

前提条件を確認したら、コンテンツ転送ツールの実行方法を学習できます。 詳しくは、[コンテンツ転送ツールの使用](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)を参照してください。
