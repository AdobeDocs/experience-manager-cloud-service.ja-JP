---
title: Content Hubに関するよくある質問（FAQ）
description: コンテンツハブに関するよくある質問（FAQ）への回答を参照してください。
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 2%

---

# Content Hubに関するよくある質問 {#content-hub-frequently-asked-questions}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Content Hubに関するよくある質問 ](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## Content Hubとは {#what-is-content-hub}

Content HubはAdobe Experience Manager Assetsas a Cloud Serviceの機能です。

Content Hubを使用すると、より広範なチームが直感的なポータルを通じて関連性の高い承認済みアセットを簡単に見つけ、ニーズに合わせてすばやく調整できます。  さらに、Content Hubには、アセットを DAM にアップロードする際にセルフサービスを容易に行える取り込みメカニズムが用意されています。 これにより、ブランドの一貫性と適切な保護策への準拠を維持しながら、コンテンツ作成速度の向上に対する組織のニーズに直接対応できます。

## Cloud Manager プログラム/環境でContent Hubを有効にできないのはなぜですか？ {#cannot-enable-content-hub}

現在、Content Hubは、Assets ライセンスを含むAEM Cloud Manager実稼動プログラムでのみ使用できます。 [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) をクリックして有効にすると、デプロイされ、そのプログラム内のAEMのオーサー実稼動環境に関連付けられます。 詳細と前提条件については、[Content Hubのデプロイ ](/help/assets/deploy-content-hub.md) を参照してください。

サンドボックスプログラム/オーサー実稼動環境のContent Hubには、アーリーアクセスプログラムがあります。 詳しくは、[ サンドボックスプログラムの概要 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) を参照してください。 アーリーアクセスプログラムについて詳しくは、Adobeアカウントチームにお問い合わせください。

この段階では、Content Hubは実稼動以外の環境（ステージング環境、開発環境など）では使用できません。

## 実稼動プログラム/環境でContent Hubを有効にしましたが、無効にできますか？ {#can-i-disable-content-hub}

実稼動プログラムでContent Hubを有効にすると、実稼動インフラストラクチャの一部にデプロイされます。 AEM Cloud Managerでは、人的エラーによる実稼動環境の使用に対するリスクを最小限に抑えるために、実稼動インフラストラクチャを削除または無効にすることはできません。

デプロイ後にContent Hubをユーザーに提供しない場合は、Admin ConsoleでContent Hub製品プロファイルにユーザーを割り当てないでください。 詳しくは、[Content Hubのデプロイ ](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) を参照してください。

## 実稼動プログラム/実稼動オーサリング環境でのみ使用できるContent Hubを使用する場合、組織内で評価するにはどうすればよいですか？ {#how-can-i-evaluate-content-hub}

Content Hubは、Adobeが提供および維持管理する機能で、開発/ステージング/実稼動による通常の検証を必要とするカスタムコードはありません。 さらに、ユーザーの機能へのアクセスは管理者によって完全に制御されるので、すべてのユーザーに公開することなく評価できます。

AEM as a Cloud Service Assetsで管理されるユーザー/実稼動コンテンツに影響を与えずに、Content Hubを評価することができます。 評価手順は次のようになります。

* 実稼動環境で [Content Hubを有効にする ](/help/assets/deploy-content-hub.md#enable-content-hub) （Cloud Manager プログラム）
* 実稼動オーサーからContent Hub製品プロファイルに [AEM管理者ユーザーを追加 ](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) します。
* AEM Administrator[Content Hubの設定 ](/help/assets/configure-content-hub-ui-options.md)
* AEM実稼動オーサーのAEM管理者またはAEM ユーザー [Content Hubの多数のアセットを承認 ](/help/assets/approve-assets-content-hub.md) します。DAM の実稼動コンテンツを変更しない場合は、AEM オーサーインスタンスに別の評価用フォルダーを作成し、DAM からアセットのアップロード/タグ付けまたはコピーを行ってください。
* Admin Console管理者がContent Hub製品プロファイルに [ 選択したユーザー ](/help/assets/deploy-content-hub.md#onboard-content-hub-users) を追加して、評価を開始できるようにします。
* 評価が完了したら、オーサーインスタンスのAEM ユーザーがテストアセットの承認を解除し、Content Hubの実稼動アセットを承認し、Admin Console管理者がContent Hubへのアクセスと承認済みコンテンツを必要とするすべてのユーザーを追加できます。 おめでとうございます。Content Hubは今ライブです。

Adobeは、ステージング環境でのContent Hubへの早期アクセスプログラムも提供しています。[Cloud Manager プログラム/環境でContent Hubを有効にできないのはなぜですか？詳しくは、](#cannot-enable-content-hub) を参照してください。

## Content Hubにログオンした後にアセットが表示されないのはなぜですか？ {#no-assets-in-content-hub}

Assetsのas a Cloud Serviceで承認済みとしてマークされたアセットは、Content Hubで自動的に使用できます。 Content Hubにログオンした後にアセットが表示されない場合は、AEM as a Cloud Service オーサー環境を使用してアセットを承認し、Content Hubで利用できるようにします。 詳しくは、[Content Hubのアセットを承認 ](/help/assets/approve-assets-content-hub.md) を参照してください。

## Content Hubを使用して直接アップロードしたアセットや、Content Hubを使用してDropboxまたは OneDrive アカウントから読み込んだアセットが表示されるのはなぜですか？ {#no-assets-uploaded-from-content-hub}

Content Hubを使用してアップロードされたアセットの表示は、設定ユーザーインターフェイスで「[ 自動承認 ](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)」切り替えスイッチが有効になっているかどうかによって異なります。

* **自動承認** 切替スイッチが有効になっている場合は、Content Hubを使用してアップロードしたアセットを自動的に利用できます。

* **自動承認** の切り替えが無効になっている場合、Content Hubを使用してアップロードしたアセットは自動的には表示されません。 アセットは、Assetsas a Cloud Serviceの `hydrated-assets` フォルダーで使用できます。 フォルダーに移動して、Content Hubに表示するアセットのステータスを `Approved` 定する [ 一括編集 ](/help/assets/approve-assets-content-hub.md) を行います。

## AEM as a Cloud Service環境でContent Hubを使用してアップロードしたアセットをすばやく検索する方法を教えてください。 {#find-uploaded-assets-on-aem-cloud}

AEM as a Cloud Service環境でContent Hubを使用してアップロードされたアセットを素早く見つけるには、次の方法があります。

1. `hydrated-assets` フォルダーへの移動。

1. **[!UICONTROL アセットステータス]** フィールドで **[!UICONTROL フィルター]** をクリックして **[!UICONTROL ステータスなし]** を設定します。

1. **[!UICONTROL 変更日]** フィールドを使用したアセットの並べ替え。

## アセットをリミックスして新しいバリエーションを作成できるように、アセットカードの「Adobe Expressを使用して編集」オプションを表示しないのはなぜですか？ {#edit-using-express-not-available}

アセットカードで「Adobe Expressを使用して編集」オプションを表示するには、アセットを新しいバリエーションに混在させる権限を持つ [Content Hub Adobe Express向けの権限に加えて、ユーザーの使用権限が必要 ](#onboard-content-hub-users-add-assets) す。 Adobe Expressは、Adobe Experience ManagerがデプロイされているAdobeAdmin Console と同じ組織にデプロイする必要があります。

## 組織のブランドガイドラインがホームページにリンクとして表示されるようにContent Hubを設定できますか？ {#content-hub-setup-brand-guidelines}

Content Hubのホームページでは、標準のすべての「Assets」、「コレクション」、「インサイト」のタブに加えて、カスタムリンクを個別のタブとして追加できます。 設定方法について詳しくは、[ カスタムリンク ](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub) を参照してください。

## 既存のBrand Portalのお客様をContent Hubに移行する計画はありますか？ {#migration-brand-portal}

Adobeは、Brand PortalからContent HubへのAdobeサポートを提供しています。これは、移行サポートチケットを作成することで使用できます。

## Content Hubに「Product Settings/Configuration」オプションが表示されないのはなぜですか。 {#ui-configuration-option-missing}

[ 設定ユーザーインターフェイス ](/help/assets/configure-content-hub-ui-options.md) にアクセスするには、[Content Hub管理者 ](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator) である必要があります。 Adobe Admin Consoleの実稼動オーサーインスタンスでAEM Administrators 製品プロファイルに割り当てられていても設定オプションが表示されない場合は、AEM Administrators 製品プロファイルの名前が変更されていないことを確認してください。 詳しくは、[AEM as a Cloud Service チームおよび製品プロファイル ](/help/onboarding/aem-cs-team-product-profiles.md) を参照してください。
