---
title: OpenAPI 機能を備えた Dynamic Media に関するよくある質問
description: OpenAPI 機能を備えた Dynamic Media に関するよくある質問
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: c36938e80d0b159c5f89d450aaa228c37c4f5276
workflow-type: ht
source-wordcount: '1600'
ht-degree: 100%

---

# OpenAPI 機能を備えた Dynamic Media に関するよくある質問 {#new-dynaminc-media-apis-frequently-asked-questions}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>OpenAPI 機能搭載 Dynamic Media のガイドを、PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE OpenAPI 機能搭載 Dynamic Media ガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

+++**Experience Manager Assets as a Cloud Service リポジトリ内のすべてのアセットは、OpenAPI 機能を備えた Dynamic Media を使用した検索および配信で使用できますか？**

いいえ、OpenAPI 機能を備えた Dynamic Media を使用した検索および配信に使用できるのは、[承認済みの最新バージョンのアセット](/help/assets/approve-assets.md)のみで、すべてのチャネルとアプリケーションでブランドの一貫性が確保されます。

+++

+++**管理者は、フォルダーに追加された新規および既存のアセットを承認済みとしてマークするにはどうすればよいですか？**

Experience Manager Assets 内のアセットのステータスは、`jcr:content/metadata/dam:status` プロパティによって管理されます。このプロパティの値は次のとおりです。

* 承認済み

* 却下

* リクエストされた変更

Experience Manager Assets では、次の管理ビューとアセットビューの画像に示すように、アセットカードで使用できる承認済みアイコンを使用して承認済みステータスを区別します。

**管理ビュー**

![管理ビューの承認済みアセット](/help/assets/assets/approved-assets-thumbs-up.png)

**アセットビュー**

![アセットビューの承認済みアセット](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


フォルダー内のすべてのアセットを承認するには、[フォルダー内のアセットを一括承認する方法](/help/assets/approve-assets.md#bulk-approve-assets)の手順を参照してください。また、プロセス全体を示すビデオもあります。

一括承認用のフォルダーを設定すると、フォルダーに追加したすべての新しいアセットが自動的に承認されます。既存のアセットはすべて、アセットの再処理後に承認されます。アセットの再処理方法について詳しくは、[デジタルアセットの再処理](/help/assets/reprocessing.md)を参照してください。未承認のアセットを他のフォルダーからコピーまたは移動する場合は、[アセットを再処理](/help/assets/reprocessing.md)する必要があります。

管理者が `Rejected` または `Changes requested` の値を指定した場合、アセットは `Rejected` としてマークされます。Experience Manager Assets では、管理ビューのアセットカードで使用可能な![アセットを却下](/help/assets/assets/do-not-localize/reject-assets.svg)を使用して却下ステータスを区別します。

同様に、Experience Manager Assets では、アセットカードの次の却下ステータスを使用して、アセットビューの却下ステータスを区別します。

![アセットビューの却下アセット](/help/assets/assets/rejected-assets-admin-view.png)


+++

+++**配信と検索のエクスペリエンスの保護で、Experience Manager 管理ビューでアセットの役割を設定するために使用する Adobe IMS（Adobe Identity Management サービス）ユーザー ID またはグループ ID を取得するにはどうすればよいですか？**

Experience Manager オーサー環境へのアクセスを必要とするユーザーは、アドビの Admin Console の Adobe IMS ユーザーとして管理されます。Adobe IMS ユーザーの概要と、Admin Console でのアクセスと管理の方法について詳しくは、[Adobe IMS ユーザー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=ja)を参照してください。

+++

+++**フォルダー内で複数のアセットを同時に承認できますか？**

はい、フォルダー内の複数のアセットを同時に承認できます。

[!DNL Experience Manager Assets Admin view] で複数のアセットを同時に承認するには、次の手順を実行します。

1. アセットを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
1. 「**[!UICONTROL 基本]**」タブで、「**[!UICONTROL レビューステータス]**」まで下にスクロールします。
1. レビューステータスを「**[!UICONTROL 承認済み]**」に変更します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

同様に、アセットビューのフォルダー内で複数のアセットを同時に承認するには、次の手順を実行します。

1. アセットを選択し、「**[!UICONTROL 一括メタデータ編集]**」をクリックします。

1. 右側のパネルの「[!UICONTROL プロパティ]」セクションにある「**[!UICONTROL ステータス]**」フィールドで「**[!UICONTROL 承認済み]**」を選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。


+++

+++**アセット配信のセキュリティを確保して Dynamic Media OpenAPI を検索するにはどうすればよいですか？**

Experience Manager のアセットガバナンスを一元化すると、DAM 管理者またはブランド管理者はアセットへのアクセスを管理できます。役割を設定するか、オーサリング側、具体的には AEM as a Cloud Service オーサーインスタンスで承認済みアセットのアクティブ化と非アクティブ化の時間を設定して、アクセスを制限できます。

配信 URL を検索または利用するエンドユーザーは、認証プロセスを正常に通過すると、制限付きアセットにアクセスできます。

詳しくは、[Experience Manager でのアセットへのアクセスの制限](restrict-assets-delivery.md#authoring)を参照してください。

+++

+++**アセットの承認ステータスを編集する権限を取得するにはどうすればよいですか？**

DAM ユーザーには、[アセットを承認](approve-assets.md#approve-assets)する権限がない可能性があります。アセットの承認ステータスを編集する権限を取得するには、管理者はアセットフォルダーに適用されているデフォルトまたはその他のメタデータスキーマを編集して、「**[!UICONTROL レビューステータス]**」フィールドに編集権限を付与できます。詳しくは、[レビューステータスの編集を無効にする方法](approve-assets.md#configuration)フィールドを参照してください。

+++

+++**サポートされているビデオのファイルサイズはどれくらいですか？**

OpenAPI 機能を備えた Dynamic Media は、ロングフォームのビデオをサポートしています。ビデオは、最大 50 GB および 2 時間をサポートできます。

+++

+++**OpenAPI 機能を備えた Dynamic Media は、Dynamic Media ソリューションとどのように異なりますか？**

OpenAPI 機能を備えた Dynamic Media と Dynamic Media はそれぞれ独自のソリューションで、それぞれが特殊な配信機能を提供します。必要に応じて最も適切なソリューションを決定するには、特定の要件を徹底的に検討することが不可欠です。

アドビからの一般的なガイダンスは、あらゆる統合ユースケース（ファーストパーティアプリまたはサードパーティアプリ）に OpenAPI スタックを備えた Dynamic Media を活用することです。Dynamic Media スタックとの統合が既に存在する場合は、OpenAPI スタック URL の構造が異なるので、変更しないことをお勧めします。まったく新しい統合ユースケースの場合にのみ、OpenAPI スタックを活用します。ユースケースで OpenAPI スタックでは使用できない高度な修飾子が必要な場合は、アドビがそのギャップを埋めるまで OpenAPI スタックを回避します。AEM Assets Cloud Services からの基本的なネイティブ配信の場合でも、ユースケースが OpenAPI スタックで使用可能な修飾子で対象とされている限り、OpenAPI スタックを評価できます。最後に、ユースケースの性質に応じて、Dynamic Media と OpenAPI スタックを備えた Dynamic Media は共存できます。

OpenAPI 機能を備えた Dynamic Media と Dynamic Media の主な違いは次のとおりです。

| OpenAPI 機能を備えた Dynamic Media | Dynamic Media |
|---|---|
| [Assets as a Cloud Service でのみ使用可能](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | また、追加の設定手順とプロビジョニング手順を使用して、オンプレミスまたは Adobe Managed Services でも使用可能です。 |
| [幅、高さ、回転、反転、画質、形式など、サポートされている画像修飾子の限定的セット](/help/assets/deliver-assets-apis.md) | 使用可能な画像修飾子の豊富なセット |
| [ユーザー、役割、日付、時間に基づいた制限付きのアセット配信](/help/assets/restrict-assets-delivery.md) | Dynamic Media に公開されたアセットには、すべてのユーザーがアクセスできます。 |
| ほとんどの開発者は、OpenAPI の仕様に精通しています。[マイクロフロントエンドのアセットセレクター](/help/assets/overview-asset-selector.md)を使用すると、AEM Assets の拡張性が非常にシンプルになります。 | 統合カスタマイズの開発時に障壁となる SOAP ベースの API。 |
| バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに行われた変更は、配信 URL に自動的に反映されます。CDN 経由の OpenAPI 機能を備えた Dynamic Media に 10 分という短い有効期限（TTL）値を設定すると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。 | 推奨される CDN TTL は 10 時間です。キャッシュ無効化アクションを使用して TTL 値を上書きできます。 |
| 承認済みアセットのみがダウンストリームアプリケーションへのアセット配信に使用可能で、デジタルエクスペリエンスでブランド承認済みアセットが有効になります。 | Dynamic Media で公開済みアセットに対する更新は、承認ワークフローなしで自動公開されるので、デジタルエクスペリエンスでブランド承認済みアセットが確実に公開されるわけではありません。 |
| 配信済みアセット数に基づく使用状況レポート。この機能は、間もなく利用できるようになります。 | 使用状況レポートは利用できません。この機能は、間もなく利用できるようになります。 |
| Assets as a Cloud Service リポジトリで有効期限切れとしてマークされたアセットは、ダウンストリームアプリケーションでは使用できなくなります。 | 固有のアセットの有効期限はありません。アセットは、AEM as a Cloud Service リポジトリから削除されるまで公開されたままになります。 |
| 画像プリセットとビデオのスマート切り抜き機能はサポートされていません。 | 画像プリセットとビデオのスマート切り抜き機能はサポートされています。 |
| 入力ビデオに基づいて最適なエンコードが提供される Dynamic Video エンコード。ネイティブビデオ配信の設定は不要です。 | 標準 3 は、入力ビデオに関係なくエンコードします（ビデオ配信のパフォーマンスに影響を与える可能性があります）。異なるビデオのビットレートごとに様々なエンコードを手動で設定する必要があります。 |
| アセット UID ベースの URL は推測が困難（URL の不明化が可能）ですが、SEO が最適化されています。 | URL の不明化は、URL クエリパラメータに対してのみ使用できます。URL 内のアセット ID（アセット名）は認識可能です。 |

+++

+++**OpenAPI 機能を備えた Dynamic Media は、接続されたアセット機能の制限にどのように対処しますか？**

次の表に、2 つのソリューションの主な違いの概要を示します。

| OpenAPI 機能を備えた Dynamic Media | 接続されたアセット |
|---|---|
| リモート DAM デプロイメント上のアセットは、AEM as a Cloud Service で使用できます。 | リモート DAM デプロイメント上のアセットは、AEM as a Cloud Service または Adobe Managed Services で使用できます。 |
| リモート DAM デプロイメント上のアセットが AEM Sites インスタンスで使用可能な場合、アセットバイナリはコピーされません。 | リモート DAM デプロイメント上のアセットが AEM Sites インスタンスで使用可能な場合、アセットバイナリがコピーされます。 |
| AEM Assets でサポートされているすべてのアセット形式タイプをサポートします。 | ビデオはサポートされていません。 |
| リモート DAM デプロイメントからアセットを取得しながら、ローカル Sites デプロイメントで Dynamic Media を使用できます。 | ローカル Sites デプロイメントの Dynamic Media は読み取り専用です。 |
| リモート DAM デプロイメントに接続される AEM Sites インスタンスの数に制限はありません。リモート DAM 上の承認済みアセットの[役割を設定して、Sites インスタンス上のアセットへのアクセスを制限](/help/assets/restrict-assets-delivery.md)できます。 | リモート DAM デプロイメントに接続できる AEM Sites インスタンスは 4 つまでに制限されます。数が増えると、追加のテストが必要になります。 |
| アセットセレクターと OpenAPI 機能を備えた Dynamic Media は両方とも拡張可能で、カスタム統合が可能です。 | Connected Assets API は、カスタム統合を可能にするほど拡張できません。 |
| バージョンの更新やメタデータの変更など、リモート DAM デプロイメントで使用可能な承認済みアセットに行われた変更は、10 分という短い有効期間（TTL）値内に Sites インスタンスに自動的に反映されます。 | リモート DAM デプロイメントでのアセットの更新はライフサイクルイベントによって自動的に処理されますが、OpenAPI 機能を備えた Dynamic Media と比較すると、はるかに時間がかかります。 |
| リモート DAM 上のアセットメタデータは、AEM Sites インスタンスでも使用できます。 | リモート DAM 上のアセットメタデータは、AEM Sites インスタンスでは使用できません。 |

+++
