---
title: コンテンツ転送ツールの前提条件
description: コンテンツ転送ツールの前提条件
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: bf69ee0a033412e632236975cc772b91c554fd87
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 17%

---

# コンテンツ転送ツールの前提条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="コンテンツ転送ツール使用時の重要な考慮事項"
>abstract="Java と AEM のバージョン、サポートされるデータストアのタイプ、ユーザーグループの考慮事項など、コンテンツ転送ツールの使用に関する重要な考慮事項を確認します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="コンテンツ転送ツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="ベストプラクティスとガイドライン"

次の表に、コンテンツ転送ツールを使用するための前提条件を示します。

以下に示すすべての考慮事項を確認してください。

| 検討事項 | 現在サポートされている内容 |
|--- |--- |
| AEM のバージョン | コンテンツ転送ツールは、AEM 6.3以降のバージョンでのみ実行できます。 AEM 6.2以前のバージョンでコンテンツ転送ツールを使用するには、コンテンツリポジトリをAEM 6.5にインプレースアップグレードする必要があります。 このためにコードをAEM 6.5にアップグレードする必要はありません。 |
| セグメントストアのサイズ | 現在、*オーサー*&#x200B;では最大83 GB、*パブリッシュ*&#x200B;では最大31 GBがサポートされています。 サポートチケットを作成し、Adobeカスタマーケアと共に、これらの制限を超えるセグメントストアのサイズに関するオプションについて話し合います。 |
| コンテンツリポジトリの合計サイズ&#x200B;<br>*（セグメントストア+データストア）* | コンテンツ転送ツールは、ファイルデータストアタイプのデータストアに対して最大10 TBのコンテンツを転送するように設計されています。 10 TBを超える値は、現在はサポートされていません。 10 TBを超えるコンテンツのオプションについて話し合うために、Adobeカスタマーケアとサポートチケットを作成します。 <br>Amazon S3およびAzure Data Storeタイプのデータストアの場合は、オプションのpre-copystepを使用し [て、コンテンツ転送プロセスを大幅に高速化](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) し、10 TBを超えるサイズのデータストアをサポートできます。 |
| 不変パスのコンテンツ | コンテンツ転送ツールを使用して不変パスのコンテンツを移行することはできません。 コンテンツを`/etc`から転送するには、特定の`"/etc"`パスのみを選択できますが、[AEM FormsをCloud ServiceとしてAEM Formsにサポートするには](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets)のみを選択します。 その他の使用例については、 [一般的なリポジトリ再構築](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring)を参照して、リポジトリ再構築の詳細を確認してください。 |

## 次の手順 {#whats-next}

前提条件を確認し、移行プロジェクトでコンテンツ転送ツールを使用できるかどうかを判断したら、コンテンツ転送ツールの使用時に[追加のベストプラクティスと考慮事項](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)を参照してください。
