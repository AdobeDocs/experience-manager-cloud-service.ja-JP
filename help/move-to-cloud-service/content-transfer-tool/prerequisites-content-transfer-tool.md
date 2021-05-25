---
title: コンテンツ転送ツールの前提条件
description: コンテンツ転送ツールの前提条件
source-git-commit: ea179642442b7b246df3096fa52d94f9b5e865ac
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# コンテンツ転送ツールの前提条件 {#prerequisites}

次の表に、コンテンツ転送ツールを使用するための前提条件を示します。

以下に示すすべての考慮事項を確認してください。

| 検討事項 | 現在サポートされている内容 |
|--- |--- |
| AEM のバージョン | コンテンツ転送ツールは、AEM 6.3以降のバージョンでのみ実行できます。 AEM 6.2以前のバージョンでコンテンツ転送ツールを使用するには、コンテンツリポジトリをAEM 6.5にインプレースアップグレードする必要があります。 このためにコードをAEM 6.5にアップグレードする必要はありません。 |
| セグメントストアのサイズ | コンテンツ転送ツールは、現在、*オーサー*&#x200B;では最大83 GBをサポートし、*パブリッシュ*&#x200B;では最大31 GBをサポートしています。 |
| コンテンツリポジトリの合計サイズ&#x200B;<br>*（セグメントストア+データストア）* | コンテンツ転送ツールは、最大10 TBのコンテンツを転送するように設計されています。 10 TBを超える値は、現在はサポートされていません。 10 TBを超えるコンテンツのオプションについて話し合うために、Adobeカスタマーケアとサポートチケットを作成します。 |
| 不変パスのコンテンツ | コンテンツ転送ツールは、`“/etc”`などの不変パスのコンテンツを移行する場合には使用できません。 特定の`"/etc"`パスを選択できますが、[AEM FormsをCloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets)としてAEM Formsにサポートする必要があります。 その他の使用例については、 [一般的なリポジトリ再構築](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring)を参照して、リポジトリ再構築の詳細を確認してください。 |

## 次の手順{#whats-next}

前提条件を確認し、移行プロジェクトでコンテンツ転送ツールを使用できるかどうかを判断したら、コンテンツ転送ツールの使用時に[追加のベストプラクティスと考慮事項](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)を参照してください。
