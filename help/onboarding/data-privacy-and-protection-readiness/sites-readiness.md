---
title: データ保護とデータプライバシーに関する規制 — Adobe Experience Manager as a Cloud Serviceサイト対応準備
description: 様々なデータ保護およびデータプライバシー規制に対するCloud ServiceSitesのサポートとしてのAdobe Experience Managerについて説明します。EU一般データ保護規則(GDPR)、カリフォルニア州消費者プライバシー法、新しいAEM as a Cloud Serviceプロジェクトを実装する際の準拠方法を含みます。
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 46%

---

# Adobe Experience Manager as a Data Protection and Data Privacy RegulationsのCloud Serviceサイト対応に関する規制{#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、貴社の法務部門にお問い合わせください。

>[!NOTE]
>
>Adobeのプライバシーに関する問題への対応と、Adobeのお客様への影響について詳しくは、[Adobeのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

Adobe Experience Manager as aCloud ServiceSitesは、お客様がデータのプライバシーと保護に関するコンプライアンスの義務を果たすのを支援する準備が整っています。 このページでは、AEM Sitesでのこのような要求の処理手順を説明します。 プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。

詳しくは、[Adobeプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

>[!NOTE]
>
>詳しくは、データ保護およびデータプライバシー規制のCloud Service対応としての[Adobe Experience Manager](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)を参照してください。

## AEM オーサー層 {#aem-author-tier}

オーサーサーバー上のユーザーアカウントとUGCコンテンツについては、[AEM Foundationのドキュメント](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)を参照してください。

## AEM パブリッシュ層 {#aem-publish-tier}

サイトで訪問者の認証に使用されるユーザーアカウントと、パブリッシュサーバー上のUGCコンテンツについては、AEM Foundationのドキュメント](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)を参照してください。[

デフォルトでは、AEM Sitesコンポーネントは、訪問者がパブリッシュサーバーに入力したフォームデータを保存しません。 サードパーティのシステムまたは Adobe Campaign にデータを転送してさらに処理をおこなうことをお勧めします。

## オプトイン／オプトアウト {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Managerには、ユーザーのオプトイン/オプトアウトの管理に使用されるcookieオプトアウトサービスが適用されます。

オプトアウトするには：

1. 次の URL に移動します。
   [Adobeプライバシーセンター — オプトアウト](https://www.adobe.com/privacy/opt-out.html)

1. 下にスクロールして&#x200B;**サービス** - **Experience Cloudサービス使用状況データ**&#x200B;に移動します。

1. 参照先のリンクを選択します。現在、**ここ**&#x200B;にタイトルが付いています。

1. 以下の詳細と、オプトアウトまたはオプトインのオプションが表示されます。

   * このサイトへの訪問に関するデータの集計や分析をオプトアウトするには、ブラウザーにcookieをインストールする必要があります。 このCookieは、オプトアウトしたことを示します。

      オプトアウトCookieを削除した場合、またはコンピューターやWebブラウザーを変更した場合は、再度オプトアウトする必要があります。

      オプトアウト — 訪問者セッションの集計および分析から除外（`amcglobal.sc.omtrdc.net`オプトアウトCookieをインストール） — ここをクリックします。

      オプトイン — 訪問者セッションの集計と分析に含める（`amcglobal.sc.omtrdc.net`オプトアウトCookieをインストールしない） — ここをクリックします。
   上記の手順に従って、実際のリンクにアクセスします。

   >[!NOTE]
   >
   > **2には、さらに詳しい説明があります。 プライバシー.** 」の節を参照し [てください](https://www.adobe.com/jp/legal/terms.html)。

## Analytics Foundation {#analytics-foundation}

AEM Sitesには、Adobe Analytics On-demand Service内の機能を使用するAnalytics Foundationとのオプションの統合が含まれています。

Adobe Analyticsに関連するデータ主体リクエストの管理について詳しくは、[Adobe Analyticsおよびデータプライバシー](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html)を参照してください。

## Targetによるパーソナライゼーションの基盤{#personalization-foundation-by-target}

AEM Sitesには、Adobe Target On-demand Service内の機能を使用する、Personalization Foundation by Targetとのオプションの統合が含まれています。

Adobe Target に関連する データサブジェクトリクエストの管理についての詳細は、[Adobe Target - プライバシーと一般データ保護規則](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)を参照してください。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEMは、ContextHubを備えたオプションのデータレイヤーを提供します。 ContextHub を使用する場合、訪問者固有のデータがブラウザー内に格納され、そのデータに基づいてルールベースのパーソナライゼーションが実行されます。

この訪問者データはデフォルトでは AEM に格納されません。ブラウザー内でパーソナライゼーションに関する決定をおこなうためのルールが、AEM からデータレイヤーに送信されます。

### オプトイン／オプトアウトの実装 {#implementing-opt-in-opt-out}

サイトの所有者は、オプトアウトコンポーネントを実装する際、以下のガイドラインに従う必要があります。

これらのガイドラインでは、デフォルトでオプトインが実装されます。したがって、Webサイトの訪問者は、個人データをブラウザーの（クライアント側の）永続性に保存する前に、明確に同意する必要があります。

* オプトアウトコンポーネントは、ContextHub コンポーネントを組み込むたびに必ず組み込んでください。
* Webサイトのデータ保護とプライバシーに関連する利用条件をWebサイトの訪問者に表示し、次の操作を許可する必要があります。

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

### ContextHub の永続性のプレビュー  {#previewing-persistence-of-contexthub}

ContextHub で使用されている永続性をプレビューするには、次の方法があります。

* ブラウザーのコンソールを使用する。以下に例を示します。

   * Chrome:

      * デベロッパー ツール／Application／Storage を選択

         * Local Storage／（Web サイト）／ContextHubPersistence
         * Session Storage／（Web サイト）／ContextHubPersistence
         * Cookies／（Web サイト）／SessionPersistence
   * Firefox:

      * 開発ツールを表示／ストレージを選択

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * Session Storage／（Web サイト）／ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence
   * Safari:

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

### ContextHub の永続性の解除  {#clearing-persistence-of-contexthub}

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
