---
title: データ保護とデータのプライバシーに関する規制 —Cloud Serviceサイトの準備Adobe Experience Manager
description: 'データ保護およびデータプライバシーに関する様々な規制に対するCloud ServiceサイトのサポートとしてのAdobe Experience Managerについて説明します。 EU General Data Protection Regulation(GDPR)、California Consumer Privacy Act（カリフォルニア消費者プライバシー法）、およびCloud Serviceプロジェクトとして新しいAEMを導入する際の準拠方法を含む。 '
translation-type: tm+mt
source-git-commit: 7b5a427853075054d56bc7ea6569d5d839e282a1
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 45%

---


# Cloud Serviceサイトに対するデータ保護の準備とデータのプライバシーに関する規制のAdobe Experience Manager {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法律上の助言とはならず、法律上の助言の代わりとしての意味も持たない。
>
>データ保護およびデータのプライバシーに関する規制に関するアドバイスについては、会社の法務部にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するアドビの対応、およびアドビのお客様にとっての意味について詳しくは、アドビのプライバシーセンター [を参照してください](https://www.adobe.com/privacy.html)。

Cloud ServiceサイトとしてのAdobe Experience Managerは、お客様がデータのプライバシーと保護に関するコンプライアンスの義務を守るのを支援する準備が整っています。 このページでは、AEM Sitesでリクエストを処理する手順を説明します。 プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。

詳しくは、 [アドビプライバシーセンターを参照してください](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>詳細は、『Data Protection and Data Privacy Regulations [』の「Data Readiness for Data Protection」と「Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) 」の「Adobe Experience Manager」を参照してください。

## AEM オーサー層 {#aem-author-tier}

User accounts and UGC content on the author server are covered in the [AEM Foundation documentation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

## AEM パブリッシュ層 {#aem-publish-tier}

User accounts used to authenticate visitors on the site, and UGC content on the publish server are covered in the [AEM Foundation documentation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

デフォルトでは、AEM Sitesコンポーネントは、訪問者が入力したフォームデータを発行サーバーに保存しません。 サードパーティのシステムまたは Adobe Campaign にデータを転送してさらに処理をおこなうことをお勧めします。

## オプトイン／オプトアウト {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Managerには、ユーザーのオプトイン/オプトアウトの管理に使用されるcookieオプトアウトサービスが適用されます。

オプトアウトするには：

1. 次の URL に移動します。
   [アドビプライバシーセンター — オプトアウト](https://www.adobe.com/privacy/opt-out.html)

1. 「 **Services** - **Experience Cloudサービスの使用状況データ」まで下にスクロールします**。

1. 参照先リンクを選択します。 現在、 **ここにタイトルが付いています**。

1. 次の詳細と、に関するオプションが表示されオプトアウトます。

   * このサイトへの訪問に関するデータの集計や分析をオプトアウトするには、ブラウザーにcookieをインストールする必要があります。 このCookieは、オプトアウトが行われたことを示します。

      オプトアウトCookieを削除した場合、またはコンピューターやWebブラウザーを変更した場合は、再度オプトアウトする必要があります。

      オプトアウト —訪問者セッションの集計と分析（オプトアウトCookieのインストール）から自分を除外する — ここをクリックします。 `amcglobal.sc.omtrdc.net`

      オプトイン —訪問者セッションの集計と分析に含める（オプトアウトCookieをインストールしない） — ここをクリックします。 `amcglobal.sc.omtrdc.net`
   実際のリンクにアクセスするには、上記の手順に従います。

   >[!NOTE]
   >
   > 2に詳しい説明があり **ます。 プライバシー.** 」の節を参照し [てください](https://www.adobe.com/jp/legal/terms.html)。

## Analytics財団 {#analytics-foundation}

AEM Sitesには、アドビのAnalyticsオンデマンドサービス内の機能を使用する、Analytics財団とのオプションの統合が含まれています。

For further information on managing data subject requests related to Adobe Analytics see [Adobe Analytics and Data Privacy](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html).

## Target別パーソナライゼーション基盤 {#personalization-foundation-by-target}

AEM Sitesには、Adobe Targetオンデマンドサービス内の機能を使用するTarget別のPersonalization Foundationとの統合（オプション）が含まれます。

Adobe Target に関連する データサブジェクトリクエストの管理についての詳細は、[Adobe Target - プライバシーと一般データ保護規則](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)を参照してください。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEMは、ContextHubを使用してオプションのデータレイヤーを提供します。 ContextHub を使用する場合、訪問者固有のデータがブラウザー内に格納され、そのデータに基づいてルールベースのパーソナライゼーションが実行されます。

この訪問者データはデフォルトでは AEM に格納されません。ブラウザー内でパーソナライゼーションに関する決定をおこなうためのルールが、AEM からデータレイヤーに送信されます。

### オプトイン／オプトアウトの実装 {#implementing-opt-in-opt-out}

サイトの所有者は、オプトアウトコンポーネントを実装する際、以下のガイドラインに従う必要があります。

これらのガイドラインでは、デフォルトでオプトインが実装されます。したがって、個人データがブラウザーの（クライアント側の）永続性に保存される前に、Webサイトの訪問者は明確に同意する必要があります。

* オプトアウトコンポーネントは、ContextHub コンポーネントを組み込むたびに必ず組み込んでください。
* Webサイトのデータ保護とプライバシーに関連する利用条件をWebサイトの訪問者に表示し、次のことを許可する必要があります。

   * 同意
   * 拒否
   * 以前の選択の変更

* サイト訪問者がサイトの利用条件に同意する場合は、次のようにして、ContextHub のオプトアウト Cookie を削除する必要があります。

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* サイト訪問者がサイトの利用条件に同意しない場合は、次のようにして、ContextHub のオプトアウト Cookie を設定する必要があります。

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* ContextHub がオプトアウトモードで動作しているかどうかを確認するには、ブラウザーのコンソールで次の呼び出しをおこなう必要があります。

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### ContextHub の永続性のプレビュー {#previewing-persistence-of-contexthub}

ContextHub で使用されている永続性をプレビューするには、次の方法があります。

* ブラウザーのコンソールを使用する。以下に例を示します。

   * Chrome の場合：

      * デベロッパー ツール／Application／Storage を選択

         * Local Storage／（Web サイト）／ContextHubPersistence
         * Session Storage／（Web サイト）／ContextHubPersistence
         * Cookies／（Web サイト）／SessionPersistence
   * Firefox の場合：

      * 開発ツールを表示／ストレージを選択

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * Session Storage／（Web サイト）／ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence
   * Safari の場合：

      * 環境設定／詳細／メニューバーに“開発”メニューを表示を選択
      * 開発／JavaScriptコンソールを表示を選択

         * コンソール／ストレージ／ローカルストレージ／（Web サイト）／ContextHubPersistence
         * コンソール／ストレージ／セッションストレージ／（Web サイト）／ContextHubPersistence
         * コンソール／ストレージ／Cookie／（Web サイト）／ContextHubPersistence
   * Internet Explorer:

      * F12 開発者ツール／コンソールを選択

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* ブラウザーのコンソールで ContextHub API を使用する。

   * ContextHub には次のデータ永続性レイヤーが用意されています。

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (デフォルト値)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      どの永続性レイヤーが使用されるかは ContextHub ストアに定義されているので、永続性の現在の状態を確認するには、すべてのレイヤーをチェックする必要があります。


例えば、ローカルストレージに格納されているデータを表示するには、次のようにします。

ContextHub で使用されている永続性をプレビューするには、次の方法があります。

* ブラウザーのコンソールを使用する。以下に例を示します。

   * Chrome の場合：デベロッパー ツール／Application／Storage を選択

      * Local Storage／（Web サイト）／ContextHubPersistence
      * Session Storage／（Web サイト）／ContextHubPersistence
      * Cookies／（Web サイト）／SessionPersistence
   * Firefox の場合：開発ツールを表示／ストレージを選択

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * Session Storage／（Web サイト）／ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence


* ブラウザーのコンソールで ContextHub API を使用する。

   * ContextHub には次のデータ永続性レイヤーが用意されています。

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (デフォルト値)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      どの永続性レイヤーが使用されるかは ContextHub ストアに定義されているので、永続性の現在の状態を確認するには、すべてのレイヤーをチェックする必要があります。


例えば、ローカルストレージに格納されているデータを表示するには、次のようにします。

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### ContextHub の永続性の解除 {#clearing-persistence-of-contexthub}

ContextHub の永続性を解除するには：

* 現在読み込まれているストアの永続性を解除するには、以下を実行します。

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 特定の永続性レイヤー（例：セッションストレージ）を解除するには、以下を実行します。

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* ContextHub のすべての永続性レイヤーを解除するには、以下のすべてのレイヤーに対して適切なコードを呼び出す必要があります。

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (デフォルト値)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
