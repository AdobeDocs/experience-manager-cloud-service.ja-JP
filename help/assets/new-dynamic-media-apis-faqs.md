---
title: OpenAPI 機能を備えたDynamic Mediaに関するよくある質問
description: OpenAPI 機能を備えたDynamic Mediaに関するよくある質問
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# OpenAPI 機能を備えたDynamic Mediaに関するよくある質問 {#new-dynaminc-media-apis-frequently-asked-questions}

+++**Experience Manager Assetsas a Cloud Serviceのすべてのアセットは、Dynamic Mediaで OpenAPI 機能を使用して検索および配信できますか？**

いいえ、のみ [アセットの承認済みの最新バージョン](/help/assets/approved-assets.md) は、OpenAPI 機能を備えたDynamic Mediaを使用した検索および配信で利用でき、すべてのチャネルとアプリケーションでブランドの一貫性を確保します。

+++

+++**管理者は、フォルダーに追加された新規アセットや既存のアセットをどのように承認済みとしてマークできますか？**

Experience Manager Assetsのアセットのステータスは、次のように管理されます `jcr:content/metadata/dam:status` プロパティ。 このプロパティの値は次のとおりです。

* 承認済み

* 却下

* 変更が要求されました

Experience Manager Assetsは、次を使用して承認済みステータスを区別します ![アセットの承認](assets/thumbs-up-icon.svg) 次の画像に示すように、アセットカードで使用できます。

![承認済みアセットのアイコン](/help/assets/assets/approved-assets-thumbs-up.png)

フォルダー内のすべてのアセットを承認するには、の手順を参照してください [フォルダー内のアセットの一括承認方法](/help/assets/approved-assets.md#bulk-approve-assets). また、プロセス全体を示すビデオもあります。

一括承認用のフォルダーを設定すると、フォルダーに追加された新しいアセットはすべて自動的に承認されます。 既存のアセットはすべて、アセットの再処理後に承認されます。 参照： [デジタルアセットの再処理](/help/assets/reprocessing.md) アセットを再処理する手順については、を参照してください。 他のフォルダーから未承認のアセットをコピーまたは移動する場合は、以下が必要です [アセットの再処理](/help/assets/reprocessing.md).

アセットはとしてマークされます `Rejected`管理者がを指定した場合 `Rejected` または `Changes requested` 値。 Experience Manager Assetsが、次を使用して却下ステータスを区別します ![アセットを却下](/help/assets/assets/do-not-localize/reject-assets.svg) アセットカードで使用可能です。

+++

+++**配信や検索のエクスペリエンスを保護するために、Adobe IMS（AdobeIdentity Management サービス）のユーザーまたはグループ ID を取得してExperience Manager管理者ビューでアセットのロールを設定する方法を教えてください。**

Experience Managerオーサー環境にアクセスする必要があるユーザーは、AdobeのAdmin ConsoleでAdobe IMSユーザーとして管理されます。 Adobe IMSユーザーの概要と、Admin Consoleでのアクセスおよび管理方法については、を参照してください。 [Adobe IMSユーザー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**1 つのフォルダー内で複数のアセットを同時に承認することはできますか？**

はい。1 つのフォルダー内で複数のアセットを同時に承認できます。

複数のアセットを同時に承認するには、次の手順を実行します [!DNL Experience Manager Assets]:

1. アセットを選択し、 **[!UICONTROL プロパティ]**.
1. が含まれる **[!UICONTROL 基本]** タブ、下にスクロール **[!UICONTROL レビューステータス]**.
1. レビューステータスをに変更します。 **[!UICONTROL 承認済み]**.
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

+++

+++**アセット配信の保護とDynamic Media OpenAPI の検索方法を教えてください。**

Experience Managerのアセットガバナンスを一元化すると、DAM 管理者またはブランド管理者はアセットへのアクセスを管理できます。 オーサリング側、特にAEMas a Cloud Serviceオーサーインスタンスで承認済みアセットの役割を設定することで、アクセスを制限できます。

エンドユーザーが配信 URL を検索または利用する際に、認証プロセスを正常に通過することで、制限付きアセットにアクセスできます。

詳しくは、を参照してください [Experience Managerー内のアセットへのアクセスを制限する](restrict-assets-delivery.md#authoring).

+++

+++**アセットの承認ステータスを編集する権限を取得するにはどうすればよいですか？**

DAM ユーザーの場合は、次の権限がない可能性があります [アセットの承認](approved-assets.md#approve-assets). アセットの承認ステータスを編集する権限を取得するために、管理者は、アセットフォルダーに適用されているデフォルトまたはその他のメタデータスキーマを編集して、次の権限を編集できます **[!UICONTROL レビューステータス]** フィールド。 詳しくは、を参照してください [レビューステータスの編集を無効にする方法](approved-assets.md#configuration) フィールド。

+++

+++**OpenAPI 機能を備えたDynamic MediaとDynamic Media ソリューションの違いは何ですか？**

OpenAPI 機能を備えたDynamic MediaとDynamic Mediaは、それぞれ独自のソリューションであり、それぞれが独自の配信機能を提供します。 特定の要件を徹底的に見直して、ニーズに合った最適なソリューションを決定することが不可欠です。

OpenAPI 機能を備えたDynamic MediaとDynamic Mediaの主な違いの一部を次に示します。

| OpenAPI 機能を備えたDynamic Media | Dynamic Media |
|---|---|
| [アセットas a Cloud Serviceでのみ使用可能](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | 追加の設定およびプロビジョニング手順を備えたオンプレミスまたはAdobeManaged Servicesでも利用できます。 |
| [サポートされる画像修飾子の限定的なセット（幅、高さ、回転、反転、画質、形式など）](/help/assets/deliver-assets-apis.md) | 利用可能な画像修飾子の豊富なセット |
| [ユーザーと役割に基づいて制限されたアセット配信](/help/assets/restrict-assets-delivery.md) | Dynamic Mediaに公開されたアセットには、すべてのユーザーがアクセスできます |
| 画像スマート切り抜きをサポートします。 | 画像およびビデオスマート切り抜きをサポートします。 |
| ほとんどのデベロッパーが準拠している OpenAPI の仕様に基づいたスタック。 を使用すると、AEM Assetsの拡張性が非常にシンプルになります [マイクロフロントエンドアセットセレクター](/help/assets/asset-selector.md). | SOAP ベースの API。統合カスタマイズの開発時に障壁となる。 |
| バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに加えられた変更は、自動的に配信 URL に反映されます。 CDN を介して OpenAPI 機能を備えたDynamic Mediaに 10 分の短期間有効（TTL）値が設定されていると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。 | 推奨される 10 時間の CDN TTL。 キャッシュ無効化アクションを使用して、TTL 値を上書きできます。 |
| ダウンストリームアプリケーションへのアセット配信には承認済みのアセットのみを使用でき、デジタルエクスペリエンスでブランド承認済みアセットを有効化できます。 配信済みアセットは、AEMas a Cloud Serviceリポジトリのオーサーインスタンスのアセットの有効期限ステータスに従います。 | Dynamic Mediaで公開済みアセットを更新すると、承認ワークフローなしで自動公開されるので、デジタルエクスペリエンスでブランドが承認したアセットに適用されるわけではありません。 固有のアセットの有効期限はありません。 アセットは、AEMas a Cloud Serviceリポジトリーから削除されるまで、公開されたままになります。 |
| 配信されたアセット数に基づく使用状況レポート。 | 使用状況レポートは使用できません。 |

+++

+++**OpenAPI 機能を備えたDynamic Mediaで Connected Assets 機能の制限に対処する方法**

次の表に、2 つのソリューションの主な違いの概要を示します。

| OpenAPI 機能を備えたDynamic Media | Connected Assets |
|---|---|
| リモート DAM デプロイメント上のアセットは、AEMas a Cloud Serviceで利用可能です。 | リモート DAM デプロイメント上のアセットは、AEMas a Cloud ServiceまたはAdobeのManaged Servicesで利用できます。 |
| リモート DAM デプロイメント上のアセットがAEM Sites インスタンスで使用可能な場合、アセットバイナリはコピーされません。 | リモート DAM デプロイメント上のアセットがAEM Sites インスタンスで使用可能な場合、アセットバイナリはコピーされます。 |
| AEM Assetsでサポートされているすべてのアセット形式タイプのサポート。 | ビデオはサポートされていません。 |
| 画像スマート切り抜きをサポートします。 | Dynamic Media画像のスマート切り抜きと画像プリセットのサポート。 |
| リモート DAM デプロイメントからアセットを取得しながら、ローカル Sites デプロイメントでDynamic Mediaを使用できます。 | ローカルの Sites デプロイメントのDynamic Mediaは読み取り専用です。 |
| リモート DAM デプロイメントに接続されるAEM Sites インスタンスの数に関する制限はありません。 次のことができます [役割を設定して Sites インスタンス上のアセットへのアクセスを制限する](/help/assets/restrict-assets-delivery.md) （リモート DAM の承認済みアセットの場合）。 | リモート DAM デプロイメントに接続できるAEM Sites インスタンスの数は 4 つまでです。 数を増やすには、追加のテストが必要です。 |
| OpenAPI 機能を持つアセットセレクターとDynamic Mediaは両方とも、カスタム統合を可能にするために拡張できます。 | Connected Assets API は、カスタム統合を許可するように拡張することはできません。 |
| バージョンの更新やメタデータの変更など、リモート DAM デプロイメントで使用可能な承認済みアセットに加えられた変更は、Sites インスタンスの有効期間（TTL）の値が 10 分以内に自動的に反映されます。 | リモート DAM デプロイメントのアセットの更新はライフサイクルイベントで自動的に処理されますが、OpenAPI 機能を備えたDynamic Mediaと比較して、はるかに時間がかかります。 |
| リモート DAM のアセットメタデータは、AEM Sites インスタンスでも使用できます。 | リモート DAM のアセットメタデータは、AEM Sites インスタンスでは使用できません。 |

+++



