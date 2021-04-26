---
title: URL の外部化
description: ExternalizerはOSGiサービスです。このサービスを使用すると、リソースパスをプログラム的に外部URLと絶対URLに変換できます。
translation-type: tm+mt
source-git-commit: 4c584ceadaa358120d1d4b4cabd7e21ced814b31
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 16%

---


# URL の外部化 {#externalizing-urls}

AEMでは、**Externalizer**&#x200B;はOSGiサービスで、リソースパス(例えば、`/path/to/my/page`)を外部URLや絶対URL（例えば`https://www.mycompany.com/path/to/my/page`）に埋め込みます。

AEMのCloud Serviceインスタンスは、外部から表示されるURLを認識できず、要求範囲外でリンクを作成する必要がある場合があるので、このサービスは、これらの外部URLを設定して構築するための中央の場所を提供します。

この記事では、Externalizerサービスの設定方法と使用方法を説明します。 サービスの技術的な詳細については、[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)を参照してください。

## 外部化子のデフォルト動作と上書き方法{#default-behavior}

標準で、Externalizerサービスには`author-p12345-e6789.adobeaemcloud.com`や`publish-p12345-e6789.adobeaemcloud.com`などの値が既に設定されており、何の介入もなく、AEMをCloud Serviceインストールとして使用する場合にカスタムドメインが使用されます。

この値を上書きするには、「[AEM用のOSGiのCloud Serviceとしての設定](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)」の説明に従って、Cloud Manager環境変数を使用し、事前定義された`AEM_CDN_DOMAIN_AUTHOR`変数と`AEM_CDN_DOMAIN_PUBLISH`変数を設定します。

## Externalizerサービスの設定{#configuring-the-externalizer-service}

Externalizerサービスを使用すると、リソースパスをプログラム的にプレフィックス付けするのに使用できるドメインを一元的に定義できます。 Externalizerサービスは、1つのドメインを持つアプリケーションにのみ使用する必要があります。

>[!NOTE]
>
>AEM用の[OSGi設定をCloud Serviceとして適用する場合と同様に、](/help/implementing/deploying/overview.md#osgi-configuration)次の手順は、ローカル開発者インスタンスに対して実行し、配置用にプロジェクトコードにコミットする必要があります。

Externalizer サービスのドメインマッピングを定義するには：

1. 次の方法でConfiguration Managerに移動します。

   `https://<host>:<port>/system/console/configMgr`

1. 「**Day CQ Link Externalizer**」をクリックして、設定ダイアログボックスを開きます。

   ![Externalizer OSGiの設定](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >構成への直接リンクは`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`です

1. **ドメイン**&#x200B;マッピングを定義します。 マッピングは、ドメイン、スペース、ドメインを参照するコードで使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **`scheme`** は、通常httpまたはhttpsですが、別のプロトコルにすることもできます。

      * httpsリンクを強制するには、httpsを使用することをお勧めします。
      * URLの外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。
   * **`server`** はホスト名（ドメイン名またはipアドレス）です。
   * **`port`** （オプション）はポート番号です。
   * **`contextpath`** （オプション）は、AEMがwebappとして別のコンテキストパスでインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前に定義されており、AEMがそれらに依存しているため、常に設定する必要があります。

   * `local`  — ローカルインスタンス
   * `author`  — オーサリングシステムのDNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、`production`、`staging`などの新しいカテゴリや、`my-internal-webservice`などの外部のAEM以外のシステムを追加できます。 プロジェクトのコードベース内の異なる場所にまたがるこのようなURLのハードコーディングを避けると便利です。

1. 「**保存**」をクリックして変更を保存します。

### Externalizerサービスの使用{#using-the-externalizer-service}

ここでは、Externalizer サービスの使用方法に関するいくつかの例を紹介します。

>[!NOTE]
>
>HTMLのコンテキストでは絶対リンクを作成しないでください。 したがって、このユーティリティはこのような場合には使用しないでください。

* **「publish」ドメインを付与してパスを外部化する：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングの前提：

   * `publish https://www.website.com`

   * `myExternalizedUrl` は次の値で終わります。

   * `https://www.website.com/contextpath/my/page.html`

* **「author」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングの前提：

   * `author https://author.website.com`

   * `myExternalizedUrl` は次の値で終わります。

   * `https://author.website.com/contextpath/my/page.html`

* **「local」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   ドメインマッピングの前提：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` は次の値で終わります。

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>他の例については、関連する [Javadoc](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
