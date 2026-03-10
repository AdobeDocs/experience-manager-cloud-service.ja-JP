---
title: コンテンツハブに関するよくある質問（FAQ）
description: コンテンツハブに関するよくある質問（FAQ）への回答を参照してください。
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 59f97fc6ded4274c27400f56b50b4a3329cc471a
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 67%

---

# コンテンツハブに関するよくある質問 {#content-hub-frequently-asked-questions}

![コンテンツハブに関するよくある質問](assets/content-hub-faqs.png)

## AEM Assets Content Hubとは {#what-is-content-hub}

AEM Assets Content Hubは、Adobe Experience Manager Assets as a Cloud Serviceの機能です。

コンテンツハブを使用すると、より広範なチームが直感的なポータルを通じて関連性のある承認済みアセットを簡単に見つけて、ニーズに迅速に適応させることができます。さらに、コンテンツハブは、ユーザーがアセットを DAM にアップロードする際に簡単にセルフサービスできる取り込みメカニズムを提供します。これにより、ブランドの一貫性と適切な保護措置への準拠を維持しながら、コンテンツ作成速度の向上に対する組織のニーズに直接対応できます。

<!--

## Why cannot I enable Content Hub on my Cloud Manager program/environment? {#cannot-enable-content-hub}

Content Hub is at this point is only available on AEM Cloud Manager Production programs, which include an Assets license (Assets Cloud Service, Assets Ultimate, Assets Prime). When you click [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) to enable it, it is deployed and associated with the author production environment of AEM in that program. See [Deploy Content Hub](/help/assets/deploy-content-hub.md) for details and prerequisites.

-->

## 実稼動プログラム/環境でAEM Assets Content Hubを有効にしましたが、無効にできますか？ {#can-i-disable-content-hub}

実稼動プログラムでAEM Assets Content Hubを有効にすると、実稼動インフラストラクチャの一部にデプロイされます。 AEM Cloud Manager では、人為的エラーによる実稼動環境の使用に対するリスクを最小限に抑えるには、実稼動インフラストラクチャを削除または無効にすることはできません。

コンテンツハブをデプロイした後にユーザーに提供しない場合は、Admin Console でコンテンツハブ製品プロファイルにユーザーを割り当てないでください。詳しくは、[コンテンツハブのデプロイ](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)を参照してください。

## 組織内でAEM Assets Content Hubを評価するにはどうすればよいですか？ {#how-can-i-evaluate-content-hub}

AEM Assets Content Hubは、Adobeが提供および維持管理する機能で、開発/ステージング/実稼働による通常の検証を必要とするカスタムコードはありません。 さらに、ユーザーによる機能へのアクセスは管理者によって完全に制御されるので、すべてのユーザーに公開せずに評価できます。

AEM as a Cloud Service Assets で管理されているユーザー／実稼動コンテンツに影響を与えることなく、コンテンツハブを評価できます。評価手順は次のようになります。

* 本番環境（Cloud Manager プログラム）で[コンテンツハブを有効にします](/help/assets/deploy-content-hub.md#enable-content-hub)。
* 実稼動オーサーからコンテンツハブ製品プロファイルに [AEM 管理者ユーザーを追加します](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator)。
* AEM 管理者が[コンテンツハブを設定します](/help/assets/configure-content-hub-ui-options.md)。
* AEM 管理者または AEM 実稼動オーサーの AEM ユーザーが[コンテンツハブのアセットの数を承認します](/help/assets/approve-assets-content-hub.md)。DAM の実稼動コンテンツを変更しない場合は、AEM オーサーインスタンスに別の評価フォルダーを作成し、DAM からいくつかのアセットをアップロード／タグ付けまたはコピーすることをお勧めします。
* Admin Console 管理者は、[選択した数名のユーザー](/help/assets/deploy-content-hub.md#onboard-content-hub-users)をコンテンツハブ製品プロファイルに追加して、評価を開始できるようにします。
* 評価が完了すると、オーサーインスタンスの AEM ユーザーはテストアセットの承認を削除し、コンテンツハブの実稼動アセットを承認できます。その後、Admin Console 管理者はコンテンツハブと承認済みコンテンツへのアクセスが必要なすべてのユーザーを追加できます。これで完了です。コンテンツハブはライブになりました。

サンドボックスプログラムとそのオーサー本番環境には、コンテンツハブへの早期アクセスプログラムがあります。詳しくは、[サンドボックスプログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)を参照してください。早期アクセスプログラムについて詳しくは、アドビアカウントチームにお問い合わせください。

## AEM Assets Content Hubにログオンした後にアセットが表示されないのはなぜですか？ {#no-assets-in-content-hub}

Assets as a Cloud Service で承認済みとしてマークされたアセットは、コンテンツハブで自動的に使用できます。コンテンツハブにログオンした後、アセットが表示されない場合は、AEM as a Cloud Service オーサー環境を使用してアセットを承認し、コンテンツハブで使用できるようにします。詳しくは、[コンテンツハブ向けアセットの承認](/help/assets/approve-assets-content-hub.md)を参照してください。

## AEM Assets Content Hubを使用して直接アップロードするか、Content Hubを使用してDropboxまたは OneDrive アカウントから読み込んだアセットが表示されるのはなぜですか？ {#no-assets-uploaded-from-content-hub}

AEM Assets Content Hubを使用してアップロードされたアセットの表示は、設定ユーザーインターフェイスで「[ 自動承認 ](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)」切り替えスイッチが有効になっているかどうかによって異なります。

* **自動承認**&#x200B;切替スイッチが有効になっている場合、コンテンツハブを使用してアップロードしたアセットは自動的に使用できます。

* **自動承認**&#x200B;切替スイッチが無効になっている場合、コンテンツハブを使用してアップロードしたアセットは自動的に表示されません。アセットは、Assets as a Cloud Service 環境の `hydrated-assets` フォルダーで使用できます。フォルダーに移動し、これらのアセットのステータスを[一括編集](/help/assets/approve-assets-content-hub.md)して `Approved` にすると、これらのアセットがコンテンツハブに表示されます。

## AEM as a Cloud Service環境でAEM Assets Content Hubを使用してアップロードしたアセットをすばやく検索する方法を教えてください。 {#find-uploaded-assets-on-aem-cloud}

AEM as a Cloud Service環境でAEM Assets Content Hubを使用してアップロードされたアセットを素早く見つけるには、次の方法があります。

1. `hydrated-assets` フォルダーに移動します。

1. 「**[!UICONTROL フィルター]**」をクリックし、「**[!UICONTROL アセットステータス]**」フィールドに&#x200B;**[!UICONTROL ステータスなし]**&#x200B;を設定します。

1. 「**[!UICONTROL 変更日]**」フィールドを使用して、アセットを並べ替えます。

## アセットをリミックスして、AEM Assets Content Hubを使用して新しいバリエーションを作成できるように、アセットカードに「Adobe Expressを使用して編集」オプションが表示されるのはなぜですか？ {#edit-using-express-not-available}

AEM Assets Content Hubのアセットカードで **Adobe Expressを使用して編集** オプションを表示するには、[Content Hub ユーザーの権限（アセットを新しいバリエーションにリミックスする権限を持つ）に加えて、Adobe Express Enterprise または Teams の使用権限（](https://www.adobe.com/jp/express/pricing) プラン [ を参照）が必要です ](#onboard-content-hub-users-add-assets)。

ユーザーを [!DNL Content Hub] および [!DNL Adobe Express] に割り当てるには、いくつかの設定方法があります。

1. 組織が [Assets Ultimate](/help/assets/assets-ultimate-overview.md) または [Assets Prime](/help/assets/assets-prime.md) のライセンスを保有し、Adobe Express のエンタイトルメント（共同作業者またはパワーユーザー）を含む Admin Consoleで、Experience Manager プロファイルの 1 つにユーザーが割り当てられている。この統合は、追加の設定を行わなくても機能します。

1. [!DNL Adobe Express] が、[!DNL Content Hub] を使用して [!DNL Experience Manager Assets] と同じ [!DNL Adobe Admin Console] にデプロイされている。この統合は、追加の設定を行わなくても機能します。

1. [!DNL Adobe Express] が、[!DNL Content Hub] を使用して [!DNL Experience Manager Assets] とは異なる [!DNL Adobe Admin Console] にデプロイされている。この場合、[!DNL Assets] 管理者は、統合が機能するように設定できます（[ドキュメント](/help/assets/connect-assets-with-creative-cloud.md)を参照）。

   >[!NOTE]
   >
   >2 つの Admin Console で Express および Assets の製品プロファイルに割り当てられたユーザーは、同一のメールアドレスと、**個人**&#x200B;アカウントではなく、ビジネス&#x200B;**エンタープライズまたはスクール**&#x200B;アカウントを使用する必要があります。理想的な設定は、両方の Admin Console を **Federated ID** として設定し、コンソール間の信頼関係を確立し、シームレスなシングルサインオンエクスペリエンスを実現することです。一部の Express プラン（Express Teams など）では、Federated ID／シングルサインオンはサポートされていません。

コンテンツハブの Adobe Express 統合では、適切な製品の使用権限に加えて、割り当てられたユーザーが、コンテンツハブを動作させる Assets オーサー環境（少なくとも **[#UICONTROL /content/dam/hydrated-assets/]** フォルダー階層）で[!UICONTROL 編集可能]の権限を持っている必要があります。このフォルダー階層では、コンテンツハブユーザーは Express を使用して作成したコンテンツを保存できます。詳しくは、管理ビュー（タッチ UI）の [権限管理](/help/security/touch-ui-principal-view.md)または簡易版の [アセットビューの権限管理](https://experienceleague.adobe.com/ja/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions)を参照してください。

## 組織のブランドガイドラインがホームページにリンクとして表示されるようにAEM Assets Content Hubを設定できますか？ {#content-hub-setup-brand-guidelines}

AEM Assets Content Hubのホームページでは、標準のすべての「Assets」、「コレクション」、「インサイト」のタブに加えて、カスタムリンクを個別のタブとして追加できます。 設定方法について詳しくは、[カスタムリンク](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)を参照してください。

## 既存のBrand Portalのお客様をAEM Assets Content Hubに移行する計画はありますか？ {#migration-brand-portal}

Adobeは、Brand PortalからAEM Assets Content Hubへの移行サポートを提供しています。このサポートを使用するには、Adobe サポートチケットを作成します。

## AEM Assets Content Hubに「Product Settings/Configuration」オプションが表示されないのはなぜですか。 {#ui-configuration-option-missing}

AEM Assets Content Hubで [Configuration ユーザーインターフェイス ](/help/assets/configure-content-hub-ui-options.md) にアクセスするには、[Content Hub管理者 ](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator) である必要があります。 Adobe Admin Console の実稼動オーサーインスタンスで AEM 管理者製品プロファイルに割り当てられているにもかかわらず、設定オプションが表示されない場合は、AEM 管理者製品プロファイルの名前が変更されていないことを確認してください。詳しくは、[AEM as a Cloud Service チームおよび製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md)を参照してください。

## AEM Assets Content HubでBrand Portalの制限に対処する方法 {#content-hub-brand-portal-comparison}


次の表に、AEM Assets Content HubとBrand Portalの主な違いの概要を示します。

| 領域 | 機能 | コンテンツハブ | Brand Portal |
|---|---|----|----|
| 配布エクスペリエンスの設定 | フィルター、アセットの詳細、アセットの追加ページ用のメタデータを設定する | ✓ | − |
|  | ポータルからの外部リンクを設定する | ✓ | − |
|  | バナーメッセージを設定する | ✓ | ✓ |
|  | ブランディング用のバナー画像を設定する | ✓ | ✓ |
|  | ブランディング要件に従って、UI のプライマリカラーとセカンダリカラーを設定する | ✓ | − |
| DAM からのアセットの共有 | DAMから承認済みのオリジナルアセットの共有 | ✓ | ✓ |
|  | 承認済みのアセットの変更は自動的に同期される | ✓ | − |
| 検索とフィルター | 動的フィルター（オプションは、表示されたアセットに基づいて動的に表示される） | ✓ | − |
|  | 検索履歴 | ✓ | − |
| アセットのアップロード | ローカルドライブ | ✓ | ✓ |
|  | アセットのアップロード時に設定可能なメタデータを追加する | ✓ | − |
| ダウンロードとアップロード | 元のアセットをダウンロードする | ✓ | ✓ |
|  | DAM からの静的レンディションを共有しダウンロードする | ✓ | ✓ |
|  | 動的レンディション（プリセットおよびスマート切り抜き）をダウンロードする | ✓ | ✓ |
|  | 期限切れアセットの表示とダウンロードを制限する機能 | ✓ | − |
| リンク共有とコレクション | ログインしたユーザーのリンク共有 | ✓ | ✓ |
|  | 公開コレクション | ✓ | ✓ |
|  | コレクション内の検索 | ✓ | − |
|  | 匿名リンク共有 | ✓ | ✓ |
|  | プライベートコレクション | ✓ | ✓ |
| 権限 | ACLベースの権限 | − | ✓ |
|  | 属性ベースのアクセス制御 | ✓ | − |
| Express 統合 | Adobe Expressでコンテンツハブアセットを編集して DAM に保存する | ✓ | − |
| ダッシュボードとレポート | Insights ダッシュボード | ✓ | − |
| UI 拡張機能 | アセットの詳細ページのカスタム拡張ポイント | 限定提供 | − |
| 近日リリース予定の革新的機能 | ユーザー別のお気に入りのコレクション | ✓ | − |
|  | 管理者によってピン留めされたコレクション | ✓ | − |
|  | セマンティック検索 | ✓ | − |
|  | ローカライズされた検索とメタデータの表示 | ✓ | − |

## AEM Assets Content Hubで選択した環境のアセットのみを表示するリポジトリを選択する方法を教えてください。 {#select-repository-multiple-environments}

AEM Assets Content Hubを実稼動用に設定し、同じプログラムに対して他の下位環境を設定した場合は、リポジトリを選択し、選択した環境のアセットを表示できます。 次の手順を実行します。

1. 右側のパネルでユーザーアイコンをクリックします。

1. 「**[!UICONTROL 製品設定]**」セクションで、「**[!UICONTROL リポジトリを選択]**」を選択します。

1. **[!UICONTROL リポジトリ]**&#x200B;ドロップダウンメニューからリポジトリを選択し、「**[!UICONTROL OK]**」をクリックして確認します。

   コンテンツハブには、選択した環境のアセットが表示されるようになりました。

## AEM Assets Content Hubでは、.ZIP ファイルタイプのサムネールプレビューをどのように表示できますか？ {#thumbnail-preview-zip-file}

AEM Assets Content Hubで.ZIP などのファイルタイプのサムネールプレビューを提供するには、.ZIP が使用可能なAEM as a Cloud Service オーサリング環境のパスのルートに、`cq5dam.preview.jpg` または `cq5dam.preview.png` という名前のレンディションを追加します。

レンディションとして追加する画像：

* JPG、JPEG または PNG 形式が使用できます。

* 50 MB 未満にする必要があります

コンテンツハブで使用可能な場合、その画像はコンテンツハブ上の .ZIP ファイルのプレビューサムネールとして表示されます。


