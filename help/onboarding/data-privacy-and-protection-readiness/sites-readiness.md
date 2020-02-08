---
title: データ保護とデータプライバシーに関する規制 — クラウドサービスサイトの準備としてのAdobe Experience Manager
description: '様々なデータ保護およびデータプライバシー規制に対するクラウドサービスサイトのサポートとしてのAdobe Experience Managerについて説明します。EUのGDPR(General Data Protection Regulation)、カリフォルニア消費者プライバシー法、およびクラウドサービスとして新しいAEMを導入する際の準拠方法を含む。 '
translation-type: tm+mt
source-git-commit: 1130e8a07bc3826380483a7560ebda7e8a17e238

---


# クラウドサービスサイトでのデータ保護の準備とデータプライバシー規則としてのAdobe Experience Manager {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本書の内容は、法律上の助言とはならず、法律上の助言の代替としての意味も持たない。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、貴社の法務部にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するアドビの対応、およびアドビのお客様にとっての意味について詳しくは、アドビのプライバシーセ [ンターを参照してください](https://www.adobe.com/privacy.html)。

クラウドサービスサイトとしてのAdobe Experience Managerは、お客様のデータのプライバシーと保護コンプライアンスの義務を支援する準備が整っています。 このページでは、AEMサイトでこのような要求を処理する手順を説明します。 プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。

詳しくは、アドビプライバシーセ [ンターを参照してください](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>詳しく [は、Adobe Experience Manager as a Cloud Service Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) （データ保護の準備とデータプライバシー規制）を参照してください。

## AEM作成者層 {#aem-author-tier}

User accounts and UGC content on the author server are covered in the [AEM Foundation documentation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

## AEM Publish Tier {#aem-publish-tier}

User accounts used to authenticate visitors on the site, and UGC content on the publish server are covered in the [AEM Foundation documentation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

デフォルトでは、AEMサイトコンポーネントは、訪問者が発行サーバーで入力したフォームデータを保存しません。 サードパーティのシステムまたは Adobe Campaign にデータを転送してさらに処理をおこなうことをお勧めします。

## オプトイン／オプトアウト {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Managerには、ユーザーのオプトイン/オプトアウトの管理に使用されるcookieオプトアウトサービスが適用されます。

オプトアウトするには：

1. 次の URL に移動します。
   [アドビプライバシーセンター — オプトアウト](https://www.adobe.com/privacy/opt-out.html)

1. 「 **Services** - **Experience cloudサービスの使用状況データ」まで下にスクロールします**。

1. 参照先リンクを選択します。現在はここにタ **イトル**。

1. 以下の詳細と、オプトアウトまたはオプトインのオプションが表示されます。

   * このサイトへの訪問に関するデータの集計と分析をオプトアウトするには、ブラウザーにcookieをインストールする必要があります。 このcookieは、オプトアウトしたことを示します。

      オプトアウトCookieを削除した場合、またはコンピューターやWebブラウザーを変更した場合は、再度オプトアウトする必要があります。

      オプトアウト — 訪問者セッションの集計と分析から自分を除外(オプトアウトcookieをインス `amcglobal.sc.omtrdc.net` トール) — ここをクリックします。

      オプトイン — 訪問者セッションの集計と分析に含める(オプトアウトcookieをインストールしな `amcglobal.sc.omtrdc.net` いでください) — ここをクリックします。
   上記の手順に従って、実際のリンクにアクセスします。

   >[!NOTE]
   >
   > 利用条件の「プライバシーポリ **シー** 」セクションに詳 [細な説明があります](https://marketing.adobe.com/resources/help/en_US/terms.html)。

## Analytics Foundation {#analytics-foundation}

AEM Sitesには、Adobe Analyticsオンデマンドサービス内の機能を使用するAnalytics Foundationとの統合（オプション）が含まれています。

For further information on managing data subject requests related to Adobe Analytics see [Adobe Analytics and Data Privacy](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html).

## Target別Personalization Foundation {#personalization-foundation-by-target}

AEM Sitesには、Adobe targetオンデマンドサービス内の機能を使用するPersonalization Foundation by targetとの統合（オプション）が含まれています。

Adobe Target に関連する データサブジェクトリクエストの管理についての詳細は、[Adobe Target - プライバシーと一般データ保護規則](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)を参照してください。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEMは、ContextHubでオプションのデータレイヤーを提供します。 ContextHub を使用する場合、訪問者固有のデータがブラウザー内に格納され、そのデータに基づいてルールベースのパーソナライゼーションが実行されます。

この訪問者データはデフォルトでは AEM に格納されません。ブラウザー内でパーソナライゼーションに関する決定をおこなうためのルールが、AEM からデータレイヤーに送信されます。

### オプトイン／オプトアウトの実装 {#implementing-opt-in-opt-out}

サイトの所有者は、オプトアウトコンポーネントを実装する際、以下のガイドラインに従う必要があります。

これらのガイドラインでは、デフォルトでオプトインが実装されます。したがって、個人データがブラウザーの（クライアント側の）永続性に保存される前に、Webサイトの訪問者は明確に同意する必要があります。

* オプトアウトコンポーネントは、ContextHub コンポーネントを組み込むたびに必ず組み込んでください。
* Webサイトのデータ保護とプライバシーに関する利用条件をWebサイトの訪問者に表示し、次の操作を許可する必要があります。

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
