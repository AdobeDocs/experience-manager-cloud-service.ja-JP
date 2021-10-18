---
title: コンテンツ転送ツールの前提条件
description: コンテンツ転送ツールの前提条件
exl-id: ef6d0e1a-0ed2-4485-adab-df6e0cf3ac4d
source-git-commit: fa7e5d07ed52a71999de95bbf6299ae5eb7af537
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 11%

---

# コンテンツ転送ツールの前提条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="コンテンツ転送ツール使用時の重要な考慮事項"
>abstract="Java と AEM のバージョン、サポートされるデータストアのタイプ、ユーザーグループの考慮事項など、コンテンツ転送ツールの使用に関する重要な考慮事項を確認します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#pre-reqs" text="コンテンツ転送ツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="ベストプラクティスとガイドライン"

次の表に、コンテンツ転送ツールを使用するための前提条件を示します。

以下に示すすべての考慮事項を確認してください。

| 検討事項 | 現在サポートされている内容 |
|--- |--- |
| AEM のバージョン | コンテンツ転送ツールは、AEM 6.3 以降のバージョンでのみ実行できます。 AEM 6.2 以前のバージョンでコンテンツ転送ツールを使用するには、コンテンツリポジトリをAEM 6.5 にインプレースアップグレードする必要があります。 このためにコードをAEM 6.5 にアップグレードする必要はありません。 |
| セグメントストアのサイズ | 現在、5,500 万個未満の JCR ノードと、最大 83 GB（オンライン圧縮サイズ）の *オーサー* 上、最大 31 GB の *パブリッシュ* 上の既存のリポジトリがサポートされています。 サポートチケットを作成し、Adobeカスタマーケアと共に、これらの制限を超えるセグメントストアのサイズに関するオプションについて話し合います。 |
| コンテンツリポジトリの合計サイズ <br>*（セグメントストア+データストア）* | コンテンツ転送ツールは、ファイルデータストアタイプのデータストアに対して最大 10 TB のコンテンツを転送するように設計されています。 現在、10 TB を超える容量はサポートされていません。 10 TB を超えるコンテンツのオプションについて話し合うために、Adobeカスタマーケアとサポートチケットを作成します。 <br>Amazon S3 および Azure Data Store タイプのデータストアの場合、オプションの pre-copystep を使用して、コンテンツ転送プロセスを大幅に高速化で [き、10 TB を超えるサイズのデータストアをサポートできま](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) す。 |
| 合計インデックスサイズ | 現在、最大 25 GB の合計インデックスサイズがサポートされています。 サポートチケットを作成し、Adobeカスタマーケアと共に、この制限を超えるインデックスサイズのオプションについて話し合います。 |
| ノード名の長さ | ノード名の長さは 150 バイト以下にする必要があります。 AEM as a Cloud Serviceのドキュメントノードストアでサポートされるように、150 バイトを超えるノード名を 150 バイト未満に短縮する必要があります。 これらの長いノード名が修正されていない場合、取り込みは失敗します。 |
| 不変パスのコンテンツ | コンテンツ転送ツールは、不変パスのコンテンツの移行には使用できません。 コンテンツを `/etc` から転送するには、特定の `/etc` パスのみを選択できますが、[AEM FormsをAEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets) にサポートする場合にのみ選択できます。 その他の使用例については、[ 一般的なリポジトリ再構築 ](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) を参照して、リポジトリ再構築の詳細を確認してください。 |
| MongoDB のノードプロパティ値 | MongoDB に格納するノードプロパティの値は 16 MB を超えることはできません。 これは MongoDB によって適用されます。 この制限を超えるプロパティ値がある場合、取り込みは失敗します。 抽出を実行する前に、次の [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) スクリプトを実行します。 すべての大きなプロパティ値を確認し、必要に応じて検証します。 16 MB を超える値は、バイナリ値に変換する必要があります。 |

## 次の手順 {#whats-next}

前提条件を確認し、移行プロジェクトでコンテンツ転送ツールを使用できるかどうかを判断したら、[ コンテンツ転送ツール ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en) の使用に関するガイドラインとベストプラクティスを参照してください。
