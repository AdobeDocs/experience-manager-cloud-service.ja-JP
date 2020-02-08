---
title: オーサリング時の AEM のトラブルシューティング
description: AEM を使用する際に発生する可能性のあるいくつかの問題です
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# オーサリング時の AEM のトラブルシューティング {#troubleshooting-aem-when-authoring}

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

## 古いページバージョンが公開されたサイト上にまだある {#old-page-version-still-on-published-site}

* **問題**：
   * You have made changes to a page and published the page to the publish site, but the *old* version of the page is still being shown on the publish site.
* **原因**：
   * いくつかの原因が考えられます。キャッシュ（ローカルブラウザーまたは Dispatcher のキャッシュ）が原因である場合がほとんどですが、レプリケーションキューに問題があることもあります。
* **解決策**：
   * これには、様々な原因が考えられます。
   * ページが正しくレプリケートされていることを確認します。ページのステータスや、必要に応じてレプリケーションキューの状態をチェックします。
   * ローカルブラウザーのキャッシュをクリアして、ページに再度アクセスします。
   * ペー `?` ジURLの末尾に追加します。例：
      * `http://<host>:<port>/sites.html/content?`
      *  これによって、ページが AEM から直接リクエストされ、Dispatcher がスキップされます。更新されたページを受け取った場合、Dispatcher のキャッシュをクリアする必要があることを表しています。
   * システム管理者に問い合わせて、レプリケーションキューに問題があることを伝えます。

## コンポーネントのアクションがツールバーに表示されない {#component-actions-not-visible-on-toolbar}

* **問題**：
   * オーサー環境でのコンテンツページの編集中に、使用可能なすべてのコンポーネントのアクションが表示されません。
* **原因**：
   * まれに、前のアクションがツールバーに影響を及ぼすことがあります。
* **解決策**：
   * ページを更新します。
