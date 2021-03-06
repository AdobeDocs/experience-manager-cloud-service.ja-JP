---
title: Commerce Integration Framework を使用した AEM と Commerce の統合に関する FAQ
description: Commerce Integration Framework を使用した AEM と Commerce の統合に関する FAQ
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 100%

---

# Commerce Integration Framework を使用した AEM と Commerce の統合に関する FAQ

## 1. CIF GraphQL はコマースのためにのみ使用されますか。それとも、AEM JCR で作成されたコンテンツのクエリに使用できますか。

アドビでは、Adobe Commerce の GraphQL API を、すべてのコマース関連データの公式コマース API として採用しています。したがって、AEM は、I/O Runtime を介して Adobe Commerce および任意のコマースエンジンとコマースデータを交換するために GraphQL を使用します。この GraphQL API は、コンテンツフラグメントにアクセスする AE M GraphQL API とは独立しています。

## 2. 製品アセット（画像）は、Adobe Commerce 管理者を介して AEM から保存および参照できますか。Dynamic Media のアセットはどのように使用できますか。

AEM Assets と Adobe Commerce の統合で、正式に利用できるものはありません。[Marketplace](https://marketplace.magento.com/bounteous-dam.html)で利用できるパートナーコネクタがあります。

回避策として、製品アセット（画像）を AEM Assets に格納できますが、アセット URL を手動で Adobe Commerce に格納する必要があります。Dynamic Media は AEM Assets の一部となったので、同じように機能します。

## 3. コマースソリューションをどこにデプロイするかは重要ですか（オンプレミスまたはクラウド内）。

いいえ、コマースソリューションをどこにデプロイするかは重要ではありません。CIF および AEM ストアフロントは、デプロイメントモデルに関係なく機能します。ただし、推奨される E2E 参照アーキテクチャを使用してソリューションをデプロイする場合、E2E テストは、一般的なエンタープライズ顧客プロファイルを表すパフォーマンス KPI に対して実行できます。これにより、ベンチマークとして使用できる追加情報が得られます。

## 4. AEM でカタログページや製品ページを作成する方法を教えてください。AEM でどのように持続されますか。

カタログページと製品ページは、汎用のカタログおよび製品ページのテンプレートに基づいて、AEM 内で動的に作成およびキャッシュされます。製品やカタログのデータは AEM には読み込まれず、AEM には保存されません。

## 5. コマースソリューションで製品データがアップデートされる場合、それは AEM に対するリアルタイムのプッシュですか。それともバッチ処理ですか。

AEM Cloud Service で使用する CIF アドオンでは、コマースソリューションから AEM にオンデマンドでデータを送信できます。したがって、コマースソリューション内にアップデートがある場合、これはリアルタイムプッシュ処理やバッチ処理ではありません。

## 6. CIF を含んだ AEM でサポートされているカタログサイズは何ですか。

これは、さらに考慮する必要がある以下のいくつかの事項によって異なります。カタログデータとページのキャッシュ率ピーク時に予想される同時リクエストの数コマースソリューションの API はどの程度の拡張性がありますか？

## 7. PIM はこのフレームワークでどのように機能しますか。

PIM データは、GraphQL 要求を介して AEM およびクライアントに公開されます。PIM データをコマースエンジンから取得できるように、PIM をコマースエンジン（Adobe Commerce など）と統合することをお勧めします。

## 8. Dispatcher を使用して、価格や他のデータもキャッシュしますか。キャッシュ無効化の課題が頻繁に発生しませんか。

Dispatcher には、価格や在庫などの動的データはキャッシュされません。動的データは、GraphQL API を介し、Web コンポーネントを使用してクライアントサイドで直接フェッチされます。静的データ（製品やカテゴリデータなど）のみが Dispatcher にキャッシュされます。製品データを変更する場合、キャッシュの無効化が必要です。

## 9. AEM Dispatcher のキャッシュ無効化は、AEM とコマースでどのように機能しますか。

Dispatcher にキャッシュされたページに対しては、TTL ベースのキャッシュ無効化を設定することをお勧めします。価格や在庫などの動的な情報については、クライアントサイドで日付を処理することをお勧めします。TTL ベースのキャッシュの無効化について詳しくは、[AEM Dispatcher](https://helpx.adobe.com/jp/experience-manager/kb/optimizing-the-dispatcher-cache.html) を参照してください。

## 10. コマースでの、AEM コンテンツをまたぐ統合検索に関して推奨事項はありますか。

製品検索の参照の実装が提供されていますが、コンテンツに関する統合検索はありません。この機能は通常、顧客に特化したもので、プロジェクト固有のレベルでより適切に解決されます。

## 11.検索は、CIF を使用した AEM とコマースの統合でどのように機能しますか。

CIF には、検索バーと検索結果のコンポーネントが用意されています。検索バーコンポーネントは、検索語句を含んだ GraphQL リクエストをコマースソリューションに送信します。コマースソリューションは、製品名、価格、SLUG などを含んだ製品リストを返します。その後、検索結果コンポーネントは、AEM で作成された検索結果ページのギャラリー表示に検索結果を表示します。検索では、基本的なフルテキスト検索がサポートされています。PDP への参照を作成するには、SLUG/URL キーを使用します。

## 12. MSM や翻訳で製品データをどのように使用できますか。

通常、製品データは PIM または Adobe Commerce で既に翻訳されています。AEM と Adobe Commerce の統合では、複数の Adobe Commerce ストアおよびストア表示への接続をサポートしています。MSM の設定では、通常、1 つの AEM サイトが 1 つの Adobe Commerce ストア表示にリンクされます。

## 13. 商業文で製品データを充実させる方法はありますか。それはどこでできますか。AEM とコマースソリューションのどちらですか。

AEM でマーケティング関連のデータとコンテンツを管理することをお勧めします。コンテンツフラグメントを使用して、コマースソリューションの製品データを追加の属性で修飾するか、構造化されていないコンテンツ用のエクスペリエンスフラグメントを作成して製品とリンクします。

## 14. プレゼンテーションレイヤー全体に AEM を使用する場合、PCI への準拠をどのように確保できますか。

抽象化された支払い方法を使用することをお勧めします。これにより、ブラウザークライアントは支払いゲートウェイプロバイダーと直接通信し、アドビもコマースソリューションもカード所有者データを保持したり受け渡したりしないようになります。このアプローチには レベル 3 の PCI コンプライアンスのみ必要です。しかし、従業員がシステムやデータとやり取りする方法など、完全に PCI に準拠するには考慮されるべき点が他にもあります。Adobe Commerce PCI への準拠について詳しくは、[PCI コンプライアンス要件](https://business.adobe.com/jp/products/magento/pci-compliance.html)を参照してください。

## 15. AEM バージョンと Adobe Commerce クラウドバージョンを使用する場合、この共同ソリューションは PCI に準拠していますか。

はい、自己評価アンケート D とコンプライアンス証明がオンリクエストで利用できます。

## 16. I/O Runtime の体験版ライセンスをリクエストする方法を教えてください。

I/O Runtime を使用するための体験版ライセンスをリクエストするには、[こちら](https://developer.adobe.com/app-builder/trial/)をクリックしてください。
