---
title: OpenAPI 機能を備えたDynamic Mediaに関するよくある質問
description: OpenAPI 機能を備えたDynamic Mediaに関するよくある質問
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 2%

---

# OpenAPI 機能を備えたDynamic Mediaに関するよくある質問 {#new-dynaminc-media-apis-frequently-asked-questions}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

+++**Experience Manager Assetsas a Cloud Serviceリポジトリー内のすべてのアセットは、OpenAPI 機能と共にDynamic Mediaを使用した検索および配信で使用できますか？**

いいえ。OpenAPI 機能を備えたDynamic Mediaを使用して検索および配信できるのは [ 承認済みの最新バージョンのアセット ](/help/assets/approve-assets.md) のみで、すべてのチャネルとアプリケーションでブランドの一貫性が確保されます。

+++

+++**管理者は、フォルダーに追加された新しいアセットや既存のアセットを「承認済み」としてマークするにはどうすればよいですか？**

Experience Manager Assetsのアセットのステータスは、プロパティ `jcr:content/metadata/dam:status` 制御されます。 このプロパティの値は次のとおりです。

* 承認済み

* 却下

* 変更が要求されました

次の管理者およびアセット表示の画像に示すように、Experience Manager Assetsはアセットカードで使用可能な承認済みアイコンを使用して、承認済みステータスを区別します。

**管理ビュー**

![ 管理ビューの承認済みアセット ](/help/assets/assets/approved-assets-thumbs-up.png)

**アセットビュー**

![Assets表示の承認済みアセット ](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


フォルダー内のすべてのアセットを承認するには、[ フォルダー内のアセットを一括承認する方法 ](/help/assets/approve-assets.md#bulk-approve-assets) の手順を参照してください。 また、プロセス全体を示すビデオもあります。

一括承認用のフォルダーを設定すると、フォルダーに追加された新しいアセットはすべて自動的に承認されます。 既存のアセットはすべて、アセットの再処理後に承認されます。 アセットの再処理方法については、[ デジタルアセットの再処理 ](/help/assets/reprocessing.md) を参照してください。 他のフォルダーから未承認のアセットをコピーまたは移動する場合は、[ アセットを再処理 ](/help/assets/reprocessing.md) する必要があります。

管理者が `Rejected` または `Changes requested` の値を指定した場合、アセットは `Rejected` とマークされます。 Experience Manager Assetsは、管理ビューのアセットカードで使用できる ![Assetsを却下 ](/help/assets/assets/do-not-localize/reject-assets.svg) を使用して、却下ステータスを区別します。

同様に、Experience Manager Assetsは、アセットカードの次の却下ステータスを使用して、Assets ビューで却下ステータスを区別します。

![Assets ビューで却下されたアセット ](/help/assets/assets/rejected-assets-admin-view.png)


+++

+++**配信や検索のエクスペリエンスを保護するために、Adobe IMS（AdobeIdentity Management サービス）のユーザー ID またはグループ ID を取得してExperience Manager管理者ビューでアセットのロールを設定するにはどうすればよいですか？**

Experience Managerオーサー環境にアクセスする必要があるユーザーは、AdobeのAdmin ConsoleでAdobe IMSユーザーとして管理されます。 Adobe IMS ユーザーの概要、およびAdmin Consoleでのアクセスおよび管理方法については、[Adobe IMS ユーザー ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en) を参照してください。

+++

+++**フォルダー内で複数のアセットを同時に承認することはできますか？**

はい。1 つのフォルダー内で複数のアセットを同時に承認できます。

[!DNL Experience Manager Assets Admin view] で複数のアセットを同時に承認するには、次の手順を実行します。

1. アセットを選択し、「**[!UICONTROL プロパティ]**」をクリックします。
1. 「**[!UICONTROL 基本]**」タブで、下にスクロールして **[!UICONTROL レビューステータス]** を表示します。
1. レビューステータスを **[!UICONTROL 承認済み]** に変更します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

同様に、Assets ビューでフォルダー内の複数のアセットを同時に承認するには、次の手順を実行します。

1. アセットを選択し、**[!UICONTROL 一括メタデータ編集]** をクリックします。

1. 右側のペインの **[!UICONTROL プロパティ]** セクションで使用可能な **[!UICONTROL ステータス]** フィールドの [!UICONTROL  承認済み ] を選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。


+++

+++**アセット配信のセキュリティを確保してDynamic Media OpenAPI を検索するにはどうすればよいですか？**

Experience Managerのアセットガバナンスを一元化すると、DAM 管理者またはブランド管理者はアセットへのアクセスを管理できます。 作成者は、ロールを設定するか、オーサリング側（特にAEM as a Cloud Service オーサーインスタンス）で承認済みアセットのアクティベーションとアクティベーション解除の時間を設定して、アクセスを制限できます。

エンドユーザーが配信 URL を検索または利用する際に、認証プロセスを正常に通過することで、制限付きアセットにアクセスできます。

詳しくは、[Experience Managerー内のアセットへのアクセスの制限 ](restrict-assets-delivery.md#authoring) を参照してください。

+++

+++**アセットの承認ステータスを編集する権限を取得するにはどうすればよいですか？**

DAM ユーザーには、「アセットを承認 [ する権限がない場合があ ](approve-assets.md#approve-assets) ます。 アセットの承認ステータスを編集する権限を取得するために、管理者は、アセットフォルダーに適用されているデフォルトまたはその他のメタデータスキーマを編集して、「**[!UICONTROL ステータスを確認]**」フィールドに編集権限を付与できます。 詳しくは、[ レビューステータスの編集を無効にする方法 ](approve-assets.md#configuration) フィールドを参照してください。

+++

+++**OpenAPI 機能を備えたDynamic MediaとDynamic Media ソリューションの違い**

OpenAPI 機能を備えたDynamic MediaとDynamic Mediaは、それぞれ独自のソリューションであり、それぞれが独自の配信機能を提供します。 特定の要件を徹底的に見直して、ニーズに合った最適なソリューションを決定することが不可欠です。

統合からの一般的なガイダンスは、Adobeのユースケース（ファーストパーティまたはサードパーティのアプリ）でDynamic Mediaと OpenAPI スタックを活用することです。 Dynamic Media スタックとの統合が既に存在する場合は、OpenAPI スタック URL の構造が異なるので、変更しないことをお勧めします。 新しい統合の使用例でのみ、OpenAPI スタックを活用します。 OpenAPI スタックで利用できない高度な修飾子が必要なユースケースの場合は、Adobeがギャップを埋めるまで OpenAPI スタックを避けます。 AEM Assets Cloud Serviceからの基本的なネイティブ配信の場合でも、OpenAPI スタックで使用可能な修飾子でユースケースがカバーされている限り、OpenAPI スタックを評価できます。 最後に、ユースケースの性質に応じて、Dynamic Mediaと OpenAPI スタックを組み合わせたDynamic Mediaを共存させることができます。

OpenAPI 機能を備えたDynamic MediaとDynamic Mediaの主な違いの一部を次に示します。

| OpenAPI 機能を備えたDynamic Media | Dynamic Media |
|---|---|
| [Assetsas a Cloud Serviceでのみ使用可能 ](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | 追加の設定およびプロビジョニング手順を備えたオンプレミスまたはAdobeManaged Servicesでも利用できます。 |
| [ 幅、高さ、回転、反転、画質、形式など、サポートされる画像修飾子の限定されたセット ](/help/assets/deliver-assets-apis.md) | 利用可能な画像修飾子の豊富なセット |
| [ ユーザー、役割、日時に基づいてアセット配信が制限される ](/help/assets/restrict-assets-delivery.md) | Dynamic Mediaに公開されたAssetsには、すべてのユーザーがアクセスできます |
| ほとんどの開発者は、OpenAPI の仕様に精通しています。 AEM Assetsの拡張性は、[ マイクロフロントエンドアセットセレクター ](/help/assets/overview-asset-selector.md) を使用すると、非常にシンプルになります。 | SOAP ベースの API。統合のカスタマイズを開発する際に障壁になる。 |
| バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに加えられた変更は、自動的に配信 URL に反映されます。 CDN を介して OpenAPI 機能を備えたDynamic Mediaに 10 分の短期間有効（TTL）値が設定されていると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。 | 推奨される 10 時間の CDN TTL。 キャッシュ無効化アクションを使用して、TTL 値を上書きできます。 |
| ダウンストリームアプリケーションへのアセット配信には承認済みのアセットのみを使用でき、デジタルエクスペリエンスでブランド承認済みアセットを有効化できます。 | Dynamic Mediaで公開済みアセットを更新すると、承認ワークフローなしで自動公開されるので、デジタルエクスペリエンスでブランドが承認したアセットに適用されるわけではありません。 |
| 配信されたアセット数に基づく使用状況レポート。 この機能は間もなく利用できるようになります。 | 使用状況レポートは使用できません。 この機能は間もなく利用できるようになります。 |
| Assetsのas a Cloud Serviceリポジトリーで期限切れとマークされたAssetsは、ダウンストリームアプリケーションでは使用できなくなりました。 | 固有のアセットの有効期限はありません。 アセットは、AEM as a Cloud Service リポジトリから削除されるまで、公開されたままになります。 |
| 画像プリセットおよびビデオスマート切り抜き機能はサポートしていません。 | 画像プリセットおよびビデオスマート切り抜き機能をサポートします。 |
| ダイナミックビデオエンコード：入力ビデオに基づいて最適なエンコードが確実に提供されます。 ネイティブビデオ配信の設定は不要です。 | 標準 3 エンコード （入力ビデオに関係なくエンコード） （ビデオ配信のパフォーマンスに影響を与える可能性があります）。 ビデオのビットレートごとに異なるエンコードを手動で設定する必要があります。 |
| アセットのUIDに基づく URL を推測するのは困難ですが（URL の不明化を有効にします）、SEO に最適化されています。 | URL の不明化は、URL クエリパラメーターでのみ使用できます。 URL 内のAssets ID （アセット名）は認識できます。 |

+++

+++**OpenAPI 機能を備えたDynamic Mediaは、Connected Assets機能の制限にどのように対応しますか？**

次の表に、2 つのソリューションの主な違いの概要を示します。

| OpenAPI 機能を備えたDynamic Media | 接続されたアセット |
|---|---|
| リモート DAM デプロイメントのAssetsは、AEM as a Cloud Serviceで利用できます。 | リモート DAM デプロイメント上のAssetsは、AEM as a Cloud ServiceまたはAdobe Managed Servicesで利用できます。 |
| リモート DAM デプロイメント上のアセットがAEM Sites インスタンスで使用可能な場合、アセットバイナリはコピーされません。 | リモート DAM デプロイメント上のアセットがAEM Sites インスタンスで使用可能な場合、アセットバイナリはコピーされます。 |
| AEM Assetsでサポートされているすべてのアセット形式タイプのサポート。 | ビデオはサポートされていません。 |
| リモート DAM デプロイメントからアセットを取得しながら、ローカル Sites デプロイメントでDynamic Mediaを使用できます。 | ローカルの Sites デプロイメントのDynamic Mediaは読み取り専用です。 |
| リモート DAM デプロイメントに接続されるAEM Sites インスタンスの数に関する制限はありません。 リモート DAM で承認されたアセットに対して、[ 役割を設定して、Sites インスタンス上のアセットへのアクセスを制限 ](/help/assets/restrict-assets-delivery.md) できます。 | リモート DAM デプロイメントに接続できるAEM Sites インスタンスの数は 4 つまでです。 数を増やすには、追加のテストが必要です。 |
| OpenAPI 機能を持つアセットセレクターとDynamic Mediaは両方とも、カスタム統合を可能にするために拡張できます。 | Connected Assets API は、カスタム統合を許可するように拡張することはできません。 |
| バージョンの更新やメタデータの変更など、リモート DAM デプロイメントで使用可能な承認済みアセットに加えられた変更は、Sites インスタンスの有効期間（TTL）の値が 10 分以内に自動的に反映されます。 | リモート DAM デプロイメントのアセットの更新はライフサイクルイベントで自動的に処理されますが、OpenAPI 機能を備えたDynamic Mediaと比較して、はるかに時間がかかります。 |
| リモート DAM のアセットメタデータは、AEM Sites インスタンスでも使用できます。 | リモート DAM のアセットメタデータは、AEM Sites インスタンスでは使用できません。 |

+++
