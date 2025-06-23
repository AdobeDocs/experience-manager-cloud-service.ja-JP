---
title: コンテンツ転送ツールの前提条件
description: コンテンツ転送ツールの前提条件を確認
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
feature: Migration
role: Admin
source-git-commit: 3e3d018dfd4babce9abef858e487bf1c116ed3a6
workflow-type: ht
source-wordcount: '441'
ht-degree: 100%

---


# コンテンツ転送ツールの前提条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="コンテンツ転送ツール使用時の重要な考慮事項"
>abstract="Java™ と AEM のバージョン、サポートされるデータストアのタイプ、ユーザーグループの考慮事項など、コンテンツ転送ツールの使用に関する重要な考慮事項を確認します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=ja" text="コンテンツ転送ツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja#best-practices" text="ベストプラクティスとガイドライン"

次の表に、コンテンツ転送ツールを使用するための前提条件を示します。

以下に示す考慮事項をすべて確認してください。

| 考慮事項 | 現在サポートされている内容 |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM のバージョン | コンテンツ転送ツールは、AEM 6.3 以降のバージョンでのみ実行できます。 |
| セグメントストアのサイズ | 現在、7 億 5,000 万個未満の JCR ノードと、*オーサー*&#x200B;上で最大 500 GB（オンライン圧縮サイズ）、*パブリッシュ*&#x200B;上で 50 GB の既存のリポジトリがサポートされています。これらの制限を超えるセグメントストアのサイズに関するオプションについては、アドビカスタマーケアでサポートチケットを作成してご相談ください。 |
| コンテンツリポジトリーの合計サイズ&#x200B;<br>*（セグメントストア + データストア）* | コンテンツ転送ツールは、ファイルデータストアタイプのデータストアに対して最大 20 TB のコンテンツを転送するように設計されています。現在、20 TB を超えるコンテンツはサポートされていません。20 TB を超えるコンテンツのオプションについては、アドビカスタマーケアでサポートチケットを作成してご相談ください。<br>大規模なリポジトリーのコンテンツ転送プロセスを大幅に高速化するには、オプションで[事前コピー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja#setting-up-pre-copy-step)手順を使用できます。このプロセスは、ファイルデータストア、Amazon S3、Azure データストアタイプのデータストアに適用されます。Amazon S3 および Azure データストアの場合、20 TB を超えるリポジトリサイズがサポートされます。 |
| Lucene インデックスの合計サイズ | `/oak:index/lucene` および `/oak:index/damAssetLucene` を除く、最大 25 GB の Lucene インデックスの合計サイズがサポートされます。この制限を超えるインデックスサイズのオプションについては、アドビカスタマーケアでサポートチケットを作成してご相談ください。 |
| 不変パスのコンテンツ | コンテンツ転送ツールを使用して不変パスのコンテンツを移行することはできません。`/etc` からコンテンツを転送するには、特定の `/etc` パスを選択できますが、[AEM Forms as a Cloud Service への AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=ja#paths-of-various-aem-forms-specific-assets) のみをサポートします。その他のすべてのユースケースについては、[共通リポジトリの再構築](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html?lang=ja)を参照して、リポジトリの再構築の詳細を確認してください。 |
| MongoDB のノードプロパティ値 | MongoDB に保存されるノードプロパティの値は 16 MB を超えることはできません。このルールは、MongoDB によって適用されます。この制限を超えるプロパティ値がある場合、取り込みは失敗します。抽出を実行する前に、[oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) スクリプトを実行します。大きなプロパティ値をすべて確認し、必要に応じて検証します。16 MB を超える値は、バイナリ値に変換する必要があります。 |

## 次の手順 {#whats-next}

前提条件を確認し、移行プロジェクトでコンテンツ転送ツールを使用できるかどうかを判断したら、[コンテンツ転送ツール使用のガイドラインとベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=ja)を参照してください。