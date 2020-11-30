---
title: AEM - Commerce Integration Framework を使用した Magento 統合 FAQ
description: AEM - Commerce Integration Framework を使用した Magento 統合 FAQ
translation-type: tm+mt
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 100%

---


# AEM - Commerce Integration Framework を使用した Magento 統合 FAQ


## 1. GraphQL は Magento のためにのみ使用されますか。それとも、AEM JCR で作成されたコンテンツのクエリに使用できますか。

当社は、Magento の GraphQL API を、すべてのコマース関連データの公式コマース API として採用しています。したがって、AEM は、I/O Runtime を介して Magento および任意のコマースエンジンとコマースデータを交換するために GraphQL を使用します。

## 2. Adobe I/O の役割を教えてください。AEM は Magento と直接接続しますか。

AEM は、I/O Runtime 層を使用せずに Magento に直接接続できます。Magento 以外のコマースバックエンド（サードパーティソリューション）を AEM と統合する必要がある場合、I/O Runtime プラットフォームを使用してマッピング層をホストし、Magento GraphQL API を任意のサードパーティソリューション API に接続できます。詳細については、[参照用実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)を参照してください。Magento 以外のソリューションの場合、AEM は I/O Runtime エンドポイントを指すように構成されます。

I/O Runtime プラットフォームは、コマースサービスの拡張やカスタマイズにも使用できます。この使用例では、I/O Runtime エンドポイントを呼び出して、それぞれのサービスのカスタマイズされた実装をホストします。統合と拡張機能の使用例は組み合わせ可能です。

## 3. 製品アセット（画像）は、Magento 管理者を介して AEM から保存および参照できますか。Dynamic Media のアセットはどのように使用できますか。

現在、AEM Assets と Magento の統合はありません。回避策として、製品アセット（画像）を AEM Assets に格納できますが、アセット URL を手動で Magento に格納する必要があります。Dynamic Media は AEM Assets の一部となったので、同じように機能します。

## 4. Magento のデプロイ先は重要ですか（オンプレミスまたはクラウド内）。

Magento のデプロイ先は重要でありません。統合と新しい AEM Venia ストアフロントは、デプロイメントモデルに関係なく機能します。ただし、承認された E2E 参照用アーキテクチャに基づいてデプロイされた場合、E2E テストは、収集され法人顧客のプロファイルを表すパフォーマンス KPI と比較して実行されます。これにより追加情報が得られ、ベンチマークとして使用できます。

## 5. AEM でカタログページや製品ページを作成する方法を教えてください。AEM でどのように持続されますか。

カタログページと製品ページは、汎用のカタログおよび製品ページのテンプレートに基づいて、AEM 内で動的に作成およびキャッシュされます。製品やカタログのデータは AEM には読み込まれず、AEM には保存されません。

## 6. Dispatcher を使用して、価格や他のデータもキャッシュしますか。キャッシュ無効化の課題が頻繁に発生しませんか。

Dispatcher には、価格や在庫などの動的データはキャッシュされません。動的データは、GraphQL API を介し、Web コンポーネントを使用してクライアントサイドで直接フェッチされます。静的データ（製品やカテゴリデータなど）のみが Dispatcher にキャッシュされます。製品データを変更する場合、キャッシュの無効化が必要です。

## 7. AEM Dispatcher のキャッシュの無効化は、AEM-Magento でどのように動作しますか。

Dispatcher にキャッシュされたページに対しては、TTL ベースのキャッシュ無効化を設定することをお勧めします。価格や在庫などの動的な情報については、クライアントサイドで日付をレンダリングすることをお勧めします。TTL ベースのキャッシュの無効化について詳しくは、「[AEM Dispatcher](https://helpx.adobe.com/jp/experience-manager/kb/optimizing-the-dispatcher-cache.html)」を参照してください。

## 8. We.Retail を使用しないのはなぜですか。

（Magento が開発した）Venia モバイルテーマが最初に使用され、Magento の PWA に合わせて調整されます。Venia テーマは、CSS のスタイル設定と AEM のコアコンポーネントにおいて最新です。

## 9. Magento で製品データがアップデートされる場合、これは AEM に対するリアルタイムのプッシュですか。それともバッチ処理ですか。

AEM Cloud Service で使用する CIF アドオンでは、Magento から AEM にオンデマンドでデータを送信できます。したがって、Magento 内にアップデートがある場合、これはリアルタイムプッシュ処理やバッチ処理ではありません。

## 10. コマースでの、AEM コンテンツをまたぐ統合検索に関して推奨事項はありますか。

製品検索の参照の実装が提供されていますが、コンテンツに関する統合検索はありません。この機能は通常、顧客に特化したもので、プロジェクト固有のレベルでより適切に解決されます。

## 11. CIF を使用した AEM-Magento での検索はどのように動作しますか。

CIF には、検索バーと検索結果のコンポーネントが用意されています。検索バーコンポーネントは、検索語を含む GraphQL 要求を Magento に送信します。次に、Magento は製品名、価格、SLUG などを含む製品リストを返します。その後、検索結果コンポーネントは、AEM で作成された検索結果ページのギャラリー表示に検索結果を表示します。検索では、基本的なフルテキスト検索がサポートされています。PDP への参照を作成するには、SLUG/URL キーを使用します。

## 11. MSM や翻訳で製品データをどのように使用できますか。

通常、製品データは PIM または Magento で既に翻訳されています。AEM-Magento 統合は、複数の Magento ストアおよびストア表示への接続をサポートします。MSM の設定では、通常、1 つの AEM サイトが 1 つの Magento ストア表示にリンクされます。

## 13. CIF は他のコマースプラットフォームとどのように連携しますか。

他のコマースソリューション（Magento 以外）などのサードパーティソリューションとの統合は、I/O Runtime プラットフォームを介しておこなわれます。  これがどのようにおこなわれるかを示すために、[参照用実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)が作成されています。Magento GraphQL API は、サードパーティのコマースプラットフォームの上に公開され、[AEM CIF Cloud Connector](https://github.com/adobe/commerce-cif-connector) と [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)を再利用できます。最大限の柔軟性と拡張性を提供するために、この統合レイヤーはサーバーレス [Adobe I/O Runtime プラットフォーム](https://www.adobe.io/apis/experienceplatform/runtime.html)上に配置されます。

## 14. 商業文で製品データを充実させる方法はありますか。どこでできますか。AEM ですか。Magento ですか。

これを実現する方法は複数あり、使用事例によって異なります。1 つの方法は、カスタム属性を操作することです。AEM の作成者は、AEM の製品エディターでこれらのフィールドを変更し、データを PIM に同期できます。また、製品ページに挿入される AEM エクスペリエンスフラグメントを活用する方法もあります。

## 15. Adobe I/O Runtime プラットフォームを使用すると、AEM と Magento の統合は変わりますか。

コマースサービスを拡張するお客様は、I/O Runtime プラットフォームでホストされるのと同じ統合および書き込みアクションシーケンスを使用して、ビジネスロジックを挿入し、コマースサービスを強化できます。

## 16. AEM では AEM の汎用テンプレートに基づいて動的に製品ページとカタログページが作成されるので、CRXDE Lite を開いてコンテンツをチェックするとどうなりますか。Magento 内の製品に基づいて、製品ツリー全体が表示されますか。表示されない場合、作成者はこれらのページをどのように強化できますか。

JCR のカタログページや製品のページはもうありません。質問 12 を参照してください。

## 17. SPA ストアのフロントは AEM SPA エディターで動作しますか。

AEM は、あらゆる種類のストアフロントでオーサリングツールとして使用できます。現在、新しいストアフロントでハイブリッドレンダリングが使用されています。今後、SPA および PWA でのオーサリングに AEM が使用される予定です。

## 18. PIM はこのフレームワークでどのように機能しますか。

PIM データは、GraphQL 要求を介して AEM およびクライアントに公開されます。PIM データをコマースエンジンから取得できるように、PIM をコマースエンジン（Magento など）と統合することをお勧めします。

## 19. プレゼンテーションレイヤー全体に AEM を使用する場合、PCI への準拠をどのように確保できますか。

AMS と Magento クラウドのデプロイに AEM を使用する場合は、抽象的な支払い方法を使用する必要があります。これにより、ブラウザークライアントは支払いゲートウェイプロバイダーと直接通信し、アドビも Magento クラウドもカード所有者データを保持したり受け渡したりしないようになります。このアプローチは、テクニカルスタックとデータセンターの PCI コンプライアンスをカバーします。しかし、従業員がシステムやデータとやり取りする方法など、完全に PCI に準拠するには考慮されるべき点が他にもあります。Magento PCI への準拠について詳しくは、https://magento.com/pci-compliance を参照してください。

## 20. I/O Runtime の体験版ライセンスをリクエストする方法を教えてください。

I/O Runtime を使用するための体験版ライセンスをリクエストするには、[こちら](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md)をクリックしてください。



