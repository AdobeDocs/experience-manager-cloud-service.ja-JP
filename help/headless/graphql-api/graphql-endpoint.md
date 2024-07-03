---
title: AEM の GraphQL エンドポイントの管理
description: ヘッドレスコンテンツ配信用に Adobe Experience Manager as a Cloud Service の GraphQL エンドポイントを管理する方法を説明します。
feature: Headless, Content Fragments,GraphQL API
exl-id: f7164ae3-4074-4db7-8c43-a79cc2ef00b1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '512'
ht-degree: 100%

---

# AEM の GraphQL エンドポイントの管理 {#graphql-aem-endpoint}

エンドポイントは、AEM 用 GraphQL へのアクセスに使用するパスです。このパスを使用すると、以下が可能になります。

* GraphQL スキーマへのアクセス
* GraphQL クエリの送信
* （GraphQL クエリに対する）応答の受信

AEM には次の 2 種類のエンドポイントがあります。

* グローバル
   * すべてのサイトで使用できます。
   * このエンドポイントは、（[設定ブラウザー](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)で定義された）すべての Sites 設定のすべてのコンテンツフラグメントモデルを使用できます。
   * Sites 設定間で共有する必要があるコンテンツフラグメントモデルがある場合は、それらをグローバル Sites 設定の下に作成する必要があります。
* Sites 設定：
   * [設定ブラウザー](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)で定義されている Sites 設定に対応します。
   * 指定したサイト／プロジェクトに固有です。
   * Sites 設定固有のエンドポイントは、その特定の Sites 設定のコンテンツフラグメントモデルと、グローバル Sites 設定のコンテンツフラグメントモデルを使用します。

>[!CAUTION]
>
>コンテンツフラグメントエディターを使用すると、Sites 設定のコンテンツフラグメントから別の Sites 設定のコンテンツフラグメントを（ポリシーを介して）参照できます。
>
>この場合、Sites 設定固有のエンドポイントを使用してすべてのコンテンツを取得できるわけではありません。
>
>コンテンツ作成者がこのシナリオを制御する必要があります。例えば、共有コンテンツフラグメントモデルをグローバルサイト設定の下に配置すると便利です。

AEM グローバルエンドポイント用 GraphQL のリポジトリーパスは次のとおりです。

`/content/cq:graphql/global/endpoint`

アプリは、リクエスト URL で次のパスを使用できます。

`/content/_cq_graphql/global/endpoint.json`

AEM 用 GraphQL のエンドポイントを有効にするには、次の操作が必要です。

* [GraphQL エンドポイントの有効化](#enabling-graphql-endpoint)
* [GraphQL エンドポイントの公開](#publishing-graphql-endpoint)

## GraphQL エンドポイントの有効化 {#enabling-graphql-endpoint}

GraphQL エンドポイントを有効にするには、まず適切な設定が必要です。「[コンテンツフラグメント - 設定ブラウザー ](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)」を参照してください。

>[!CAUTION]
>
>[コンテンツフラグメントモデルの使用が有効になっていない](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)場合、「**作成**」オプションは使用できません。

対応するエンドポイントを有効にするには、以下を行います。

1. **ツール**／**一般** に移動し、「**GraphQL**」を選択します。
1. 「**作成**」を選択します。
1. **新しい GraphQL エンドポイントを作成**&#x200B;ダイアログが表示されます。以下を指定します。
   * **名前**：エンドポイントの名前。任意のテキストを入力できます。
   * **次により提供される GraphQL スキーマを使用**：ドロップダウンリストを使用して、必要なサイト／プロジェクトを選択します。

   >[!NOTE]
   >
   >ダイアログには次の警告が表示されます。
   >
   >* *慎重に管理しないと、GraphQL エンドポイントでデータのセキュリティとパフォーマンスに関する問題が発生する可能性があります。エンドポイントの作成後に、適切な権限が設定されていることを確認します。*

1. 「**作成**」で確定します。
1. **次の手順**&#x200B;ダイアログには、セキュリティコンソールへの直接リンクが表示されるので、作成したエンドポイントに適切な権限が付与されているか確認できます。

   >[!CAUTION]
   >
   >エンドポイントは、すべてのユーザーがアクセスできます。そのため、GraphQL クエリがサーバーに大きな負荷をかける可能性があるので、特にパブリッシュインスタンスでは、セキュリティ上の問題が発生するおそれがあります。
   >
   >使用例に適した ACL をエンドポイントに設定できます。

## GraphQL エンドポイントの公開 {#publishing-graphql-endpoint}

新しいエンドポイントを選択し、「 **公開**」を選択して、すべての環境で完全に使用できるようにします。

>[!CAUTION]
>
>エンドポイントは、すべてのユーザーがアクセスできます。
>
>GraphQL クエリがサーバーに大きな負荷をかける可能性があるので、パブリッシュインスタンスでは、セキュリティ上の問題が発生する恐れがあります。
>
>[ユースケースに適した ACL](/help/headless/security/permissions.md) をエンドポイントに設定します。
