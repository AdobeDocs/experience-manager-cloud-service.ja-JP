---
title: データ保護およびデータプライバシーに関する規制 - Adobe Experience Manager as a Cloud Service Sites の対応
description: EU 一般データ保護規則（GDPR）やカリフォルニア州消費者プライバシー法など、データ保護およびデータプライバシーに関する様々な規制に対する Adobe Experience Manager as a Cloud Service Sites のサポートと、新しい AEM as a Cloud Service プロジェクトを実装する際にこれらの規制に準拠する方法について説明します。
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 100%

---

# データ保護およびデータプライバシー規制に対する Adobe Experience Manager as a Cloud Service Sites の対応 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、自社の法務部門にお問い合わせください。

>[!NOTE]
>
>アドビのプライバシーに関する問題への対応と、アドビのお客様への影響について詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/jp/privacy.html)をご覧ください。

Adobe Experience Manager as a Cloud Service Sites は、データのプライバシーと保護に関するコンプライアンス義務の遂行でお客様を支援する用意が整っています。このページでは、AEM Sites でこのような要求を処理する手順について説明します。プライベートデータの格納場所や、それらのデータを手動で、またはコードを使用して削除する方法について説明します。

詳しくは、[アドビプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

>[!NOTE]
>
>詳しくは、[データ保護およびデータプライバシー規制に対する Adobe Experience Manager as a Cloud Service の対応](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)を参照してください。

## AEM オーサー層 {#aem-author-tier}

オーサーサーバー上のユーザーアカウントと UGC コンテンツについては、[AEM の基盤に関するドキュメント](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)を参照してください。

## AEM パブリッシュ層 {#aem-publish-tier}

サイト上で訪問者の認証に使用されるユーザーアカウント、およびパブリッシュサーバー上の UGC コンテンツについては、[AEM の基盤に関するドキュメント](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)を参照してください。

AEM Sites コンポーネントはデフォルトでは、訪問者から入力されたフォームデータをパブリッシュサーバーに保存しません。サードパーティのシステムまたは Adobe Campaign にデータを転送してさらに処理を行うことをお勧めします。

## オプトイン／オプトアウト {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager には、ユーザーのオプトイン／オプトアウトの管理に使用される cookie オプトアウトサービスが適用されます。

オプトアウトするには：

1. 次の URL に移動します。
   [アドビプライバシーセンター - アドビのプライバシーに関する選択肢](https://www.adobe.com/jp/privacy/opt-out.html)

1. 下にスクロールして、**サービス**／**Experience Cloud サービスの使用状況データ**&#x200B;に移動します。

1. 参照先のリンクをクリックします。現在は、**こちらから**&#x200B;というリンクになっています。

1. 以下の詳細と、オプトアウトまたはオプトインのオプションが表示されます。

   * このサイトへのユーザーの訪問に関するデータ集計および解析をオプトアウトするには、ブラウザーに cookie をインストールする必要があります。この cookie はユーザーがオプトアウトしたことを識別します。

      オプトアウト cookie を削除する、またはコンピューターまたは Web ブラウザーを変更する場合は、再度オプトアウトする必要があります。

      オプトアプト - ユーザーを訪問者セッション集計や解析から除外 (`amcglobal.sc.omtrdc.net` オプトアウト cookie をインストール) - ここをクリック

      オプトイン - ユーザーを訪問者セッション集計や解析に含める (`amcglobal.sc.omtrdc.net` オプトアウト cookie をインストールしない) - ここをクリック
   上記の手順に従って、実際のリンクにアクセスします。

   >[!NOTE]
   >
   > **2. プライバシー**&#x200B;の節（[アドビ基本利用条件](https://www.adobe.com/jp/legal/terms.html)の第 2 条）にさらに詳しい説明があります。

## Analytics Foundation {#analytics-foundation}

AEM Sites には、Adobe Analytics On-demand Services 内の機能を使用した Analytics Foundation との統合（オプション）が含まれています。

Adobe Analytics に関連するデータ主体からの要求の管理について詳しくは、[Adobe Analytics とデータ保護](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html?lang=ja)を参照してください。

## Personalization Foundation by Target {#personalization-foundation-by-target}

AEM Sites には、Adobe Target On-demand Services 内の機能を使用した Personalization Foundation by Target との統合（オプション）が含まれています。

Adobe Target に関連する データサブジェクトリクエストの管理についての詳細は、[Adobe Target - プライバシーと一般データ保護規則](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=ja)を参照してください。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM には、ContextHub を使用するオプションのデータレイヤーが用意されています。ContextHub を使用する場合、訪問者固有のデータがブラウザー内に格納され、そのデータに基づいてルールベースのパーソナライゼーションが実行されます。

この訪問者データはデフォルトでは AEM に格納されません。ブラウザー内でパーソナライゼーションに関する決定を行うためのルールが、AEM からデータレイヤーに送信されます。

### オプトイン／オプトアウトの実装 {#implementing-opt-in-opt-out}

サイトの所有者は、オプトアウトコンポーネントを実装する際、以下のガイドラインに従う必要があります。

これらのガイドラインでは、デフォルトでオプトインが実装されます。そのため、Web サイトの訪問者は、個人データがブラウザーの（クライアントサイド）永続ストレージに格納される前に、明確に同意する必要があります。

* オプトアウトコンポーネントは、ContextHub コンポーネントを組み込むたびに必ず組み込んでください。
* Web サイトのデータ保護およびプライバシーに関連する利用条件を Web サイトの訪問者に表示して、訪問者が以下を行えるようにする必要があります。

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

* ContextHub がオプトアウトモードで動作しているかどうかを確認するには、ブラウザーのコンソールで次の呼び出しを行う必要があります。

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### ContextHub の永続性のプレビュー {#previewing-persistence-of-contexthub}

ContextHub で使用されている永続性をプレビューするには、次の方法があります。

* ブラウザーのコンソールを使用する。以下に例を示します。

   * Chrome:

      * デベロッパー ツール／Application／Storage を選択

         * ローカルストレージ／（Web サイト）／ContextHubPersistence
         * Session Storage／（Web サイト）／ContextHubPersistence
         * Cookie／（Web サイト）／SessionPersistence
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

      * `ContextHub.Utils.Persistence.Modes.LOCAL`（デフォルト）
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      どの永続性レイヤーが使用されるかは ContextHub ストアに定義されているので、永続性の現在の状態を確認するには、すべてのレイヤーをチェックする必要があります。


例えば、ローカルストレージに格納されているデータを表示するには、次のようにします。

ContextHub で使用されている永続性をプレビューするには、次の方法があります。

* ブラウザーのコンソールを使用する。以下に例を示します。

   * Chrome の場合：デベロッパー ツール／Application／Storage を選択

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * Session Storage／（Web サイト）／ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence
   * Firefox の場合：開発ツールを表示／ストレージを選択

      * ローカルストレージ／（Web サイト）／ContextHubPersistence
      * Session Storage／（Web サイト）／ContextHubPersistence
      * Cookie／（Web サイト）／SessionPersistence


* ブラウザーのコンソールで ContextHub API を使用する。

   * ContextHub には次のデータ永続性レイヤーが用意されています。

      * `ContextHub.Utils.Persistence.Modes.LOCAL`（デフォルト）
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

   * `ContextHub.Utils.Persistence.Modes.LOCAL`（デフォルト）
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
