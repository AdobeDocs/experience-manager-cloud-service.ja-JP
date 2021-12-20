---
title: コンテンツ転送ツールの前提条件
description: コンテンツ転送ツールの前提条件
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 67%

---

# コンテンツ転送ツールの前提条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="コンテンツ転送ツール使用時の重要な考慮事項"
>abstract="Java と AEM のバージョン、サポートされるデータストアのタイプ、ユーザーグループの考慮事項など、コンテンツ転送ツールの使用に関する重要な考慮事項を確認します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#pre-reqs" text="コンテンツ転送ツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja#best-practices" text="ベストプラクティスとガイドライン"

次の表に、コンテンツ転送ツールを使用するための前提条件を示します。

以下に示す考慮事項をすべて確認してください。

| 検討事項 | 現在サポートされている内容 |
|--- |--- |
| AEM のバージョン | コンテンツ転送ツールは、AEM 6.3 以降のバージョンでのみ実行できます。 |
| セグメントストアのサイズ | 現在、5,500 万個未満の JCR ノードと、*オーサー*&#x200B;上で最大 83 GB（オンライン圧縮サイズ）、パブリッシュ上で最大&#x200B;*パブリッシュ*&#x200B;上で最大 31 GB の既存のリポジトリーがサポートされています。これらの制限を超えるセグメントストアのサイズに関するオプションについては、Adobe カスタマーケアでサポートチケットを作成してご相談ください。 |
| コンテンツリポジトリーの合計サイズ&#x200B;<br>*（セグメントストア+データストア）* | コンテンツ転送ツールは、ファイルデータストアタイプのデータストアに対して最大 20 TB のコンテンツを転送できるように設計されています。20 TB を超えるものは現在はサポートされていません。20 TB を超えるコンテンツのオプションについては、Adobe カスタマーケアでサポートチケットを作成してご相談ください。<br>大規模なリポジトリのコンテンツ転送プロセスを大幅に高速化するには、 [プリコピー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja#setting-up-pre-copy-step) ステップを使用できます。 これは、ファイルデータストア、Amazon S3、Azure データストアのタイプのデータストアに当てはまります。 Amazon S3 および Azure Data Store では、20 TB を超えるリポジトリサイズがサポートされます。 |
| 合計 Lucene インデックスサイズ | 現在、最大 25GB の Lucene インデックスの合計サイズがサポートされています。 この制限を超えるインデックスサイズのオプションについては、Adobe カスタマーケアでサポートチケットを作成してご相談ください。 |
| ノード名の長さ | ノード名の長さは 150 バイト以下にする必要があります。150 バイトを超えるノード名を AEM as a Cloud Service のドキュメントノードストアでサポートするには、150 バイト以下に短縮する必要があります。長いノード名が修正されていない場合、取り込みは失敗します。 |
| 不変パスのコンテンツ | コンテンツ転送ツールを使用して不変パスのコンテンツを移行することはできません。コンテンツを `/etc` から転送するには、特定の `/etc` パスのみを選択できますが、これは [AEM Forms から AEM Forms as Cloud Service をへの移行をサポート](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=ja#paths-of-various-aem-forms-specific-assets)するためのものです。その他の使用例については、[一般的なリポジトリーの再構築](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=ja#restructuring)を参照して、リポジトリー再構築の詳細を確認してください。 |
| MongoDB のノードプロパティ値 | MongoDB に保存するノードプロパティの値は 16MB を超えることはできません。 これは、MongoDB によって適用されます。 この制限を超えるプロパティ値がある場合、取り込みは失敗します。 抽出を実行する前に、次を実行します。 [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) スクリプト 大きなプロパティ値をすべて確認し、必要に応じて検証します。 16MB を超える値は、バイナリ値に変換する必要があります。 |

## 次の手順 {#whats-next}

前提条件を確認し、移行プロジェクトでコンテンツ転送ツールを使用できるかどうかを判断したら、 [コンテンツ転送ツール使用のガイドラインとベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
