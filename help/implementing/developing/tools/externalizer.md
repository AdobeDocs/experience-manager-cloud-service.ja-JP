---
title: URL の外部化
description: Externalizerは、プログラムによってリソースパスを外部URLおよび絶対URLに変換できるOSGiサービスです。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: ce43bdc94f14faa69add16139e22ea3f34dfc52f
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 16%

---

# URL の外部化 {#externalizing-urls}

AEMの&#x200B;**Externalizer**&#x200B;は、リソースパス(例えば、`/path/to/my/page`)を外部URLと絶対URL（例えば、`https://www.mycompany.com/path/to/my/page`）に埋め込みます。

AEM as a Cloud Serviceインスタンスは、外部から表示されるURLを認識できず、場合によってはリクエスト範囲外でリンクを作成する必要があるので、このサービスは、外部URLを設定して作成するための一元的な場所を提供します。

この記事では、Externalizerサービスの設定方法と使用方法を説明します。 このサービスの技術的な詳細については、[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)を参照してください。

## Externalizerのデフォルトの動作と{#default-behavior}のオーバーライド方法

Externalizerサービスは、初期設定で`author-p12345-e6789.adobeaemcloud.com`や`publish-p12345-e6789.adobeaemcloud.com`などの値を持ちます。

このような値を上書きするには、 AEM用のOSGiのCloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)の説明に従って、Cloud Manager環境変数を使用し、事前定義された`AEM_CDN_DOMAIN_AUTHOR`変数と`AEM_CDN_DOMAIN_PUBLISH`変数を設定します。[

## Externalizerサービスの設定{#configuring-the-externalizer-service}

Externalizerサービスを使用すると、リソースパスにプログラム的にプレフィックスを付けるのに使用できるドメインを一元的に定義できます。 Externalizerサービスは、1つのドメインを持つアプリケーションにのみ使用する必要があります。

>[!NOTE]
>
>AEM as aCloud Serviceに[OSGi設定を適用する場合と同様に、](/help/implementing/deploying/overview.md#osgi-configuration)次の手順をローカル開発者インスタンスで実行し、デプロイメント用にプロジェクトコードにコミットする必要があります。

Externalizer サービスのドメインマッピングを定義するには：

1. 次の方法でConfiguration Managerに移動します。

   `https://<host>:<port>/system/console/configMgr`

1. **Day CQ Link Externalizer**&#x200B;をクリックして、設定ダイアログボックスを開きます。

   ![Externalizer OSGiの設定](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >設定への直接リンクは`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`です。

1. **ドメイン**&#x200B;マッピングを定義します。 マッピングは、ドメイン、スペース、ドメインを参照するコードで使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **`scheme`** は通常、httpまたはhttpsですが、別のプロトコルを指定することもできます。

      * httpsリンクを強制するには、httpsを使用することをお勧めします。
      * URLの外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。
   * **`server`** はホスト名（ドメイン名またはipアドレス）です。
   * **`port`** （オプション）はポート番号です。
   * **`contextpath`** （オプション）は、AEMがWebアプリとして別のコンテキストパスでインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前に定義されており、AEMがこれらを利用するため常に設定する必要があります。

   * `local`  — ローカルインスタンス
   * `author`  — オーサリングシステムのDNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、`production`、`staging`などの新しいカテゴリや、`my-internal-webservice`などの外部のAEM以外のシステムを追加できます。 このようなURLをプロジェクトのコードベースの異なる場所にハードコーディングするのを防ぐのに役立ちます。

1. 「**保存**」をクリックして変更を保存します。

### Externalizerサービスの使用{#using-the-externalizer-service}

ここでは、Externalizer サービスの使用方法に関するいくつかの例を紹介します。

>[!NOTE]
>
>HTMLのコンテキストでは絶対リンクを作成しないでください。 したがって、このユーティリティは、このような場合には使用しないでください。

* **「publish」ドメインを付与してパスを外部化する：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `publish https://www.website.com`

   * `myExternalizedUrl` 値で終わる

   * `https://www.website.com/contextpath/my/page.html`

* **「author」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `author https://author.website.com`

   * `myExternalizedUrl` 値で終わる

   * `https://author.website.com/contextpath/my/page.html`

* **「local」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` 値で終わる

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>他の例については、関連する [Javadoc](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
