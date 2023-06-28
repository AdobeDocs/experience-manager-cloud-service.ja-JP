---
title: コンテンツ転送ツールの前提条件
description: コンテンツ転送ツールの前提条件
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 41%

---

# コンテンツ転送ツールの前提条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="コンテンツ転送ツール使用時の重要な考慮事項"
>abstract="Java™およびAEMのバージョン、サポートされるデータストアのタイプ、ユーザーグループの考慮事項など、コンテンツ転送ツールの使用に関する重要な考慮事項を確認します。"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja" text="コンテンツ転送ツール使用時の重要な考慮事項"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#best-practices" text="ベストプラクティスとガイドライン"

次の表に、コンテンツ転送ツールを使用するための前提条件を示します。

以下に示すすべての考慮事項を確認します。

| 考慮事項 | 現在サポートされている内容 |
|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM のバージョン | コンテンツ転送ツールは、AEM 6.3 以降のバージョンでのみ実行できます。 |
| セグメントストアのサイズ | 現在、5,500 万個未満の JCR ノードと、*オーサー*&#x200B;上で最大 250 GB（オンライン圧縮サイズ）、パブリッシュ上で最大&#x200B;*パブリッシュ*&#x200B;上で最大 50 GB の既存のリポジトリーがサポートされています。サポートチケットを作成してAdobeカスタマーケアを使用し、これらの制限を超えるセグメントストアのサイズに関するオプションについて話し合うことができます。 |
| コンテンツリポジトリーの合計サイズ&#x200B;<br>*（セグメントストア+データストア）* | コンテンツ転送ツールは、ファイルデータストアタイプのデータストアに対して最大 20 TB のコンテンツを転送するように設計されています。 20 TB を超える値は、現在サポートされていません。 20 TB を超えるコンテンツのAdobeを話し合えるよう、サポートチケットを作成します。 <br>大規模なリポジトリーのコンテンツ転送プロセスを大幅に高速化するには、オプションで [事前コピー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step) 手順を使用できます。このプロセスは、ファイルデータストア、Amazon S3、Azure データストアのタイプのデータストアに適用されます。 Amazon S3 および Azure Data Store では、20 TB を超えるリポジトリサイズがサポートされます。 |
| Lucene インデックスの合計サイズ | 最大 25 GB の Lucene インデックスの合計サイズ（を除く） `/oak:index/lucene` および `/oak:index/damAssetLucene` はサポートされています。 サポートチケットを作成し、Adobeカスタマーケアと共に、この制限を超えるインデックスサイズのオプションについて話し合うことができます。 |
| ノード名の長さ | ノードの親パスが 350 バイト以上の場合、ノード名の長さは 150 バイト以下にする必要があります。AEM as a Cloud Serviceのドキュメントノードストアでサポートされるように、これらのノード名を &lt;= 150 バイトに短縮する必要があります。 これらの長いノード名が修正されていない場合、取り込みは失敗します。 |
| 不変パスのコンテンツ | コンテンツ転送ツールを使用して不変パスのコンテンツを移行することはできません。コンテンツの転送元 `/etc`を選択すると、 `/etc` パス（ただし、サポートするパスのみ） [AEM FormsからAEM Formsへのas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). その他の使用例については、 [一般的なリポジトリ再構築](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) リポジトリの再構築の詳細を参照してください。 |
| MongoDB のノードプロパティ値 | MongoDB に保存されるノードプロパティの値は 16 MB を超えることはできません。このルールは MongoDB によって適用されます。 この制限を超えるプロパティ値がある場合、取り込みは失敗します。 抽出を実行する前に、[oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) スクリプトを実行します。大きなプロパティ値をすべて確認し、必要に応じて検証します。16 MB を超える値は、バイナリ値に変換する必要があります。 |

## 次の手順 {#whats-next}

前提条件を確認し、移行プロジェクトでコンテンツ転送ツールを使用できるかどうかを判断したら、 [コンテンツ転送ツール使用のガイドラインとベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja).
