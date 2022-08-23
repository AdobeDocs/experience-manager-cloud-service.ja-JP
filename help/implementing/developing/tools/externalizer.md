---
title: URL の外部化
description: Externalizer は、プログラムによってリソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: 28903c1cbadece9d0ef575cdc0f0d7fd32219538
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 80%

---

# URL の外部化 {#externalizing-urls}

AEM の **Externalizer** は、プログラムによってリソースパス（例：`/path/to/my/page`）を外部の絶対 URL（例：`https://www.mycompany.com/path/to/my/page`）に変換できるようにする OSGi サービスであり、その変換はパスに事前設定済みの DNS をプレフィックスとして付けることで実現します。

AEM as a Cloud Service インスタンスには自分の外部向け URL がわからず、また、場合によってはリンクをリクエストスコープの範囲外で作成する必要があるので、このサービスは、そのような外部 URL を設定して作成するための一元的な場所を提供します。

この記事では、Externalizer サービスの設定方法と使用方法について説明します。このサービスの技術的な詳細については、[Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer のデフォルトの動作とオーバーライド方法 {#default-behavior}

Externalizer サービスは、初期設定で、一部のドメイン識別子を、環境用に生成されたAEMサービス URL に一致する絶対 URL プレフィックス（例： ）にマッピングします `author https://author-p12345-e6789.adobeaemcloud.com` および `publish https://publish-p12345-e6789.adobeaemcloud.com`. これらの各デフォルトドメインのベース URL は、Cloud Manager で定義された環境変数から読み取られます。

参照用に、のデフォルトの OSGi 設定 `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` 効果的には次のようになります。

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>デフォルト `local`, `author`, `preview`、および `publish` OSGi 設定の Externalizer ドメインマッピングは、元の `$[env:...]` 上記の値。
>
>カスタムのデプロイ `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` ファイルをAEMにas a Cloud Serviceし、これらの標準のドメインマッピングを省略すると、予期しないアプリケーション動作が発生する可能性があります。

を上書きするには、 `preview` および `publish` の値を使用する場合は、Cloud Manager の環境変数を使用します。詳しくは、この記事を参照してください。 [AEM as a Cloud Service用の OSGi の設定](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) および事前定義済みの `AEM_CDN_DOMAIN_PUBLISH` および `AEM_CDN_DOMAIN_PREVIEW` 変数。

## Externalizer サービスの設定 {#configuring-the-externalizer-service}

Externalizer サービスでは、プログラムでリソースパスにプレフィックスを付けるために使用可能なドメインを一元的に定義できます。Externalizer サービスは、1 つのドメインを持つアプリケーションにのみ使用してください。

>[!NOTE]
>
>[AEM as a Cloud Service に OSGi 設定を適用](/help/implementing/deploying/overview.md#osgi-configuration)する場合と同様に、ローカル開発者インスタンスで次の手順を実行し、デプロイメント用のプロジェクトコードにコミットする必要があります。

Externalizer サービスのドメインマッピングを定義するには：

1. 次の方法で設定マネージャーに移動します。

   `https://<host>:<port>/system/console/configMgr`

1. 「**Day CQ Link Externalizer**」をクリックして設定ダイアログボックスを開きます。

   ![Externalizer の OSGi 設定](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >この設定に直接アクセスするためのリンクは `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` です。

1. **ドメイン**&#x200B;マッピングを定義します。マッピングは、次のように、コード内でドメインを参照するために使用できる一意の名前、スペース、ドメインから構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`

   ここで、

   * **`scheme`** は通常、http または https ですが、別のプロトコルを指定することもできます。

      * https リンクを強制するには、https を使用することをお勧めします。
      * URL の外部化を要求する際にクライアントコードがスキームを上書きしない場合に使用されます。
   * **`server`** はホスト名（ドメイン名または IP アドレス）です。
   * **`port`**（オプション）はポート番号です。
   * **`contextpath`**（オプション）は、AEM が異なるコンテキストパスの下の Web アプリケーションとしてインストールされている場合に限り設定します。

   例：`production https://my.production.instance`

   次のマッピング名は事前定義されており、AEM で使用されるので、常に設定されている必要があります。

   * `local` - ローカルインスタンス
   * `author` - オーサリングシステムの DNS
   * `publish` - 公開 Web サイトの DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、`production` や `staging` などの新しいカテゴリや、`my-internal-webservice` などの AEM 以外の外部システムを追加できます。このような URL をプロジェクトのコードベースの様々な場所にハードコーディングするのを防ぐのに役立ちます。

1. 「**保存**」をクリックして変更を保存します。

### Externalizer サービスの使用 {#using-the-externalizer-service}

ここでは、Externalizer サービスの使用方法に関するいくつかの例を紹介します。

>[!NOTE]
>
>HTML のコンテキストでは絶対リンクを作成しないでください。したがって、このユーティリティは、そのような場合には使用しないでください。

* **「publish」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `publish https://www.website.com`

   * `myExternalizedUrl` が次の値で終わる。

   * `https://www.website.com/contextpath/my/page.html`

* **「author」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `author https://author.website.com`

   * `myExternalizedUrl` が次の値で終わる。

   * `https://author.website.com/contextpath/my/page.html`

* **「local」ドメインを付与してパスを外部化するには：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   ドメインマッピングが次のような場合：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` が次の値で終わる。

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>他の例については、関連する [Javadoc](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
