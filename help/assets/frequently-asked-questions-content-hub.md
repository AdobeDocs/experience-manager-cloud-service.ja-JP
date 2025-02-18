---
title: コンテンツハブに関するよくある質問（FAQ）
description: コンテンツハブに関するよくある質問（FAQ）への回答を参照してください。
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1112'
ht-degree: 100%

---

# コンテンツハブに関するよくある質問 {#content-hub-frequently-asked-questions}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![コンテンツハブに関するよくある質問](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## コンテンツハブとは何ですか？ {#what-is-content-hub}

コンテンツハブは、Adobe Experience Manager Assets as a Cloud Service の機能です。

コンテンツハブを使用すると、より広範なチームが直感的なポータルを通じて関連性のある承認済みアセットを簡単に見つけて、ニーズに迅速に適応させることができます。さらに、コンテンツハブは、ユーザーがアセットを DAM にアップロードする際に簡単にセルフサービスできる取り込みメカニズムを提供します。これにより、ブランドの一貫性と適切な保護措置への準拠を維持しながら、コンテンツ作成速度の向上に対する組織のニーズに直接対応できます。

## Cloud Manager プログラム／環境でコンテンツハブを有効にできないのはなぜですか？ {#cannot-enable-content-hub}

現時点では、コンテンツハブは Assets ライセンス（Assets Cloud Service、Assets Ultimate、Assets Prime）を含む AEM Cloud Manager 実稼動プログラムでのみ使用できます。[コンテンツハブ](/help/assets/deploy-content-hub.md#enable-content-hub)をクリックして有効にすると、コンテンツハブがデプロイされ、そのプログラム内の AEM のオーサー実稼動環境に関連付けられます。詳細と前提条件について詳しくは、[コンテンツハブのデプロイ](/help/assets/deploy-content-hub.md)を参照してください。

## 実稼動プログラム／環境でコンテンツハブを有効にしましたが、無効にできますか？ {#can-i-disable-content-hub}

実稼動プログラムでコンテンツハブを有効にすると、実稼動インフラストラクチャの一部としてデプロイされます。AEM Cloud Manager では、人為的エラーによる実稼動環境の使用に対するリスクを最小限に抑えるには、実稼動インフラストラクチャを削除または無効にすることはできません。

コンテンツハブをデプロイした後にユーザーに提供しない場合は、Admin Console でコンテンツハブ製品プロファイルにユーザーを割り当てないでください。詳しくは、[コンテンツハブのデプロイ](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)を参照してください。

## コンテンツハブは実稼動プログラム／実稼動オーサリング環境でのみ使用できますが、組織内で評価するにはどうすればよいですか？ {#how-can-i-evaluate-content-hub}

コンテンツハブは、アドビが提供および保守する機能で、開発／ステージング／実稼動環境での通常の検証を必要とするカスタムコードはありません。さらに、ユーザーによる機能へのアクセスは管理者によって完全に制御されるので、すべてのユーザーに公開せずに評価できます。

AEM as a Cloud Service Assets で管理されているユーザー／実稼動コンテンツに影響を与えることなく、コンテンツハブを評価できます。評価手順は次のようになります。

* 実稼動環境（Cloud Manager プログラム）で[コンテンツハブを有効にします](/help/assets/deploy-content-hub.md#enable-content-hub)。
* 実稼動オーサーからコンテンツハブ製品プロファイルに [AEM 管理者ユーザーを追加します](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator)。
* AEM 管理者が[コンテンツハブを設定します](/help/assets/configure-content-hub-ui-options.md)。
* AEM 管理者または AEM 実稼動オーサーの AEM ユーザーが[コンテンツハブのアセットの数を承認します](/help/assets/approve-assets-content-hub.md)。DAM の実稼動コンテンツを変更しない場合は、AEM オーサーインスタンスに別の評価フォルダーを作成し、DAM からいくつかのアセットをアップロード／タグ付けまたはコピーすることをお勧めします。
* Admin Console 管理者は、[選択した数名のユーザー](/help/assets/deploy-content-hub.md#onboard-content-hub-users)をコンテンツハブ製品プロファイルに追加して、評価を開始できるようにします。
* 評価が完了すると、オーサーインスタンスの AEM ユーザーはテストアセットの承認を削除し、コンテンツハブの実稼動アセットを承認できます。その後、Admin Console 管理者はコンテンツハブと承認済みコンテンツへのアクセスが必要なすべてのユーザーを追加できます。これで完了です。コンテンツハブはライブになりました。

サンドボックスプログラムとそのオーサー実稼動環境には、コンテンツハブへの早期アクセスプログラムがあります。詳しくは、[サンドボックスプログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)を参照してください。早期アクセスプログラムについて詳しくは、アドビアカウントチームにお問い合わせください。

コンテンツハブは、実稼動以外の環境（ステージングおよび開発）ではまだ使用できません。Assets Ultimate のステージング／開発環境での提供開始は 2025年3月を予定しています。

## コンテンツハブにログオンした後、アセットが表示されないのはなぜですか？ {#no-assets-in-content-hub}

Assets as a Cloud Service で承認済みとしてマークされたアセットは、コンテンツハブで自動的に使用できます。コンテンツハブにログオンした後、アセットが表示されない場合は、AEM as a Cloud Service オーサー環境を使用してアセットを承認し、コンテンツハブで使用できるようにします。詳しくは、[コンテンツハブ向けアセットの承認](/help/assets/approve-assets-content-hub.md)を参照してください。

## コンテンツハブを使用して直接アップロードしたアセットや、コンテンツハブを使用して Dropbox または OneDrive アカウントから読み込んだアセットが表示されないのはなぜですか？ {#no-assets-uploaded-from-content-hub}

コンテンツハブを使用してアップロードしたアセットの表示は、設定ユーザーインターフェイスで使用可能な[自動承認](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)切替スイッチを有効にしているかどうかによって異なります。

* **自動承認**&#x200B;切替スイッチが有効になっている場合、コンテンツハブを使用してアップロードしたアセットは自動的に使用できます。

* **自動承認**&#x200B;切替スイッチが無効になっている場合、コンテンツハブを使用してアップロードしたアセットは自動的に表示されません。アセットは、Assets as a Cloud Service 環境の `hydrated-assets` フォルダーで使用できます。フォルダーに移動し、これらのアセットのステータスを[一括編集](/help/assets/approve-assets-content-hub.md)して `Approved` にすると、これらのアセットがコンテンツハブに表示されます。

## AEM as a Cloud Service 環境でコンテンツハブを使用してアップロードされたアセットをすばやく見つけるにはどうすればよいですか？ {#find-uploaded-assets-on-aem-cloud}

AEM as a Cloud Service 環境でコンテンツハブを使用してアップロードされたアセットは、次の手順ですばやく見つけることができます。

1. `hydrated-assets` フォルダーに移動します。

1. 「**[!UICONTROL フィルター]**」をクリックし、「**[!UICONTROL アセットステータス]**」フィールドに&#x200B;**[!UICONTROL ステータスなし]**&#x200B;を設定します。

1. 「**[!UICONTROL 変更日]**」フィールドを使用して、アセットを並べ替えます。

## アセットをリミックスして新しいバリエーションを作成できるように、アセットカードで Adobe Express オプションを使用して編集を表示できないのはなぜですか？ {#edit-using-express-not-available}

アセットカードで Adobe Express オプションを使用して編集内容を表示するには、[アセットを新しいバリエーションにリミックスする権限を持つコンテンツハブユーザー](#onboard-content-hub-users-add-assets)の権限に加えて、Adobe Express 権限も必要です。Adobe Express は、Adobe Experience Manager がデプロイされている Adobe Admin Console の同じ組織にデプロイする必要があります。

## 組織のブランドガイドラインがホームページのリンクとして表示されるようにコンテンツハブを設定できますか？ {#content-hub-setup-brand-guidelines}

コンテンツハブのホームページにある標準の「すべてのアセット」タブ、「コレクション」タブ、「インサイト」タブに加えて、カスタムリンクを個別のタブとして追加できます。設定方法について詳しくは、[カスタムリンク](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)を参照してください。

## 既存の Brand Portal のお客様をコンテンツハブに移行する予定はありますか？ {#migration-brand-portal}

アドビでは、アドビサポートチケットを作成することで使用できる Brand Portal からコンテンツハブへの移行サポートを提供しています。

## コンテンツハブに「製品設定」オプションや「設定」オプションが表示されないのはなぜですか？ {#ui-configuration-option-missing}

[設定ユーザーインターフェイス](/help/assets/configure-content-hub-ui-options.md)にアクセスするには、[コンテンツハブ管理者](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator)である必要があります。Adobe Admin Console の実稼動オーサーインスタンスで AEM 管理者製品プロファイルに割り当てられているにもかかわらず、設定オプションが表示されない場合は、AEM 管理者製品プロファイルの名前が変更されていないことを確認してください。詳しくは、[AEM as a Cloud Service チームおよび製品プロファイル](/help/onboarding/aem-cs-team-product-profiles.md)を参照してください。
