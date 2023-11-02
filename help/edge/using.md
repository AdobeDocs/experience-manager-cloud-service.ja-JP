---
title: 使用Edge Delivery Services
description: Edge Delivery Services(EDS) の使用
feature: Edge Delivery Services
exl-id: 41999302-b4c9-4f5a-b659-6e7398a3c4f4
source-git-commit: 34965338015df868778a95582524df08a7c5f136
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# 使用Edge Delivery Services {#usingedge}

Edge Delivery を使用すると、作成者がコンテンツをすばやく更新および公開でき、新しいサイトを迅速に起動できる、迅速な開発環境を作成できます。 そのため、同じ Web サイト上で複数のコンテンツソースを操作でき、選択したソースに関係なく、シームレスに公開を効率化できます。 したがって、編集からインターネット上のコンテンツが表示されるまでに、数秒しかかかりません。

## オーサリング {#authoring-edge}

Edge 配信を利用すると、オーサリングが簡単で迅速で柔軟なものになります。 オーサリングには、Edge Delivery Servicesのコンテキスト内で 2 つの異なる方法を使用できます。

* ドキュメントベースのオーサリング (Microsoft Word やGoogleドキュメントなど ) - [詳しくは、このリンクを参照してください。](https://www.hlx.live/docs/authoring).
* ページエディター/ユニバーサルエディター — 担当のAdobe営業にお問い合わせください。

ドキュメントベースのオーサリングの場合、Microsoft Word やGoogle Docs など、様々なソースを使用できます。 これらのソースからのドキュメントは、Web サイト上のページになります。 見出し、リスト、画像、フォント要素、ビデオはすべて、初期ソースから Web サイトに転送できます。 SEO 用にメタデータを追加したり、ブロックを使用して構造化コンテンツを操作したり、機能を追加したりできます。

## 公開 {#publishing-edge}

Edge 配信を利用すると、コンテンツソースに関係なく、コンテンツの公開をシームレスにおこなえます。 プロセスは次のとおりです。 [サイドキック拡張機能](#using-sidekick) 公開メカニズムとコンテンツが Web サイト上で数秒で有効になるのをトリガーします。

## Edge Delivery Servicesと GitHub {#github-edge}

Edge 配信では GitHub を活用するので、顧客は GitHub リポジトリから直接コードを管理およびデプロイできます。 例えば、Google Docs またはMicrosoft Word にコンテンツを書き込み、GitHub で CSS と JavaScript を使用してサイトの機能を開発することができます。 コンテンツのプレビューから実稼動環境まで、ブランチごとに Web サイトが自動的に作成されます。 GitHub リポジトリに配置したすべてのリソースは、ビルドプロセスなしで Web サイト上で使用できます。

## Sidekickの使用 {#using-sidekick}

AEMサイドキックには、コンテキストに応じたオプションを備えたツールバーが用意されており、これを使用して、コンテンツの編集、プレビューおよび公開を簡単に行うことができます。 後 [インストール](https://www.hlx.live/docs/sidekick-extension) AEM sidekick 拡張機能は、プロジェクト環境で、またはコンテンツの編集時 ( 例えば、Google Docs 内 ) に使用できます。 環境に応じて、プレビュー、再読み込み、編集、公開など、いくつかのアクションを使用できます。 プレビューから実稼動に移行するサイドキックを使用する場合は環境を切り替えることもできます。逆の場合も同様です。

**公開するには**&#x200B;をクリックし、プレビューページでサイドキックを開き、「公開」アクションを使用します。 「公開」をクリックすると、ページの現在のプレビューバージョンが実稼動環境と実稼動環境で使用できるようになります。

## AEM Assetsとドキュメントベースのオーサリングの統合 {#integrate-assets-edge}

Edge 配信を使用すると、Microsoft Word またはGoogleドキュメントでドキュメントをオーサリングする際に、AEM Assetsリポジトリで使用可能な画像を使用できます。

ドキュメント内で画像を使用するオプションは、 [AEM Assets sidekick プラグインの設定](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

AEM Assetsのサイドキックプラグインは、次へのアクセスをサポートしています。

* AEM Assets as a Cloud Service

* AEM Assets Essentials

AEM Assetsのサイドキックプラグインを設定した後、次の操作を実行できます。 [GoogleドキュメントまたはMicrosoft Word ドキュメント内で画像の使用を開始する](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## 参考情報 {#further-reading}

詳しくは、次のページを参照してください。

* Edge 配信の開始方法について詳しくは、 [ビルド](https://www.hlx.live/docs/#build) の節を参照してください。
* Edge 配信を使用してコンテンツをオーサリングおよび公開する方法については、 [セクションを公開](https://www.hlx.live/docs/authoring).
* サイドキック拡張機能の使用方法については、 [サイドキックの使用](https://www.hlx.live/docs/sidekick) ページに貼り付けます。
* AEMオーサリングの場合は、 [オーサリングの概念ページ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html)
