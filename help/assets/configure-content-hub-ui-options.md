---
title: コンテンツハブユーザーインターフェイスの設定
description: コンテンツハブユーザーインターフェイスの設定
source-git-commit: 7224cca950e61bea298f246245bdb221fd8fa22e
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 7%

---

# コンテンツハブユーザーインターフェイスの設定 {#configure-content-hub-user-interface}

<!-- ![Download assets](assets/download-asset.jpg) -->
![Content Hubでのアセットの設定](assets/configure-assets.png)

Experience Manager Assetsを使用すると、管理者は、Content Hub ユーザーインターフェイスで使用できるオプションを設定できます。 管理者が選択した設定オプションに基づいて、Content Hub ユーザーはContent Hubでフィールドを表示できます。 設定オプションは次のとおりです。

* アセットの検索中にユーザーが使用できるフィルター。

* 各アセットで使用できるアセットの詳細またはプロパティ。

* Content Hubへのアセットの追加中にユーザーが使用できるメタデータフィールド。

* Content Hubで検索できるアセットメタデータフィールド。

* 組織に表示する必要があるブランディングコンテンツ。

* アセット、コレクション、インサイトに加えて、Content Hubに含める必要のあるカスタムリンク。

## 前提条件 {#prerequisites-configuration-ui}

[Content Hub管理者](/help/assets/deploy-content-hub.md#step-3-onboard-content-hub-administrator) 組織内の他のユーザーに対して設定オプションを設定できます。

## Content Hubの設定オプションへのアクセス {#access-configuration-options-content-hub}

Content Hubの設定オプションにアクセスするには：

1. 右側のパネルでユーザーアイコンをクリックします。

1. が含まれる **[!UICONTROL 製品設定]** セクションで選択 **[!UICONTROL 設定]**.

   ![Content Hubの設定オプションへのアクセス](assets/access-content-hub-configuration-ui.png)

## Content Hubで設定オプションを管理する {#manage-configuration-options}

ユーザーに対して次の設定オプションを管理します。

* [import](#configure-import-options-content-hub)

* [フィルター](#configure-filters-content-hub)

* [アセットの詳細](#configure-asset-details-content-hub)

* [検索](#configure-metadata-search-content-hub)

* [ブランディング](#configure-branding-content-hub)

* [カスタムリンク](#configure-custom-links-content-hub)

### import {#configure-import-options-content-hub}

Content Hub ポータルへのアセットのアップロードまたはインポート時にユーザーに表示されるメタデータフィールド（キャンペーン名、キーワード、チャネル、期間、地域など）を設定できます。 これを行うには、次の手順を実行します。

1. 日 [設定](#access-configuration-options-content-hub) ユーザ インタフェース、クリック **[!UICONTROL インポート]**.

1. クリック **[!UICONTROL メタデータを追加]**.

1. プロパティのラベルを指定し、 **[!UICONTROL メタデータ]** フィールドに入力し、新しいアセットメタデータの入力タイプを選択します。

1. 「」をクリックします **[!UICONTROL 必須フィールド]** 新しいアセットのアップロード時に、新しいメタデータフィールドを必須にしてユーザーに指定するように切り替えます。

1. クリック **[!UICONTROL 確認]**. 新しいメタデータが、既存のアセットプロパティのリストに表示されます。

1. 「**[!UICONTROL 保存]**」をクリックして、変更内容を適用します。

同様に、 ![編集アイコン](assets/do-not-localize/edit_icon.svg)使用可能な各プロパティの横にあるを使用して、ラベルを編集するには、アセットをアップロードする際に、ユーザーがこれらのフィールドを必須または非必須にします **[!UICONTROL 必須フィールド]** メタデータプロパティを削除するには、切り替えるか、削除アイコンをクリックします。

「」をクリックします **[!UICONTROL 自動承認]** Content Hubですぐに使用できるように、Experience Manager Assets リポジトリーに追加するすべてのアセットを自動承認する必要がある場合は、切り替えます。 それ以外の場合は、DAM 作成者または管理者が手動でアセットを承認して、Content Hubで使用できるようにする必要があります。 切り替えは、デフォルトでオフ状態に設定されています。

クリック **[!UICONTROL 保存]** すべての変更を加えて変更を適用した後。

![Content Hubの設定 UI アップロードの詳細](assets/configuration-ui-upload-details.png)

設定ユーザーインターフェイスで有効にしたメタデータは、アセットのアップロードページに表示されます。

![Content Hubへのメタデータのアップロード](assets/configuration-ui-add-assets.png)

### フィルター {#configure-filters-content-hub}

Content Hubでは、管理者がアセットの検索時に表示するフィルターを設定できます。 新しいフィルターを追加するには、次の手順を実行します。

1. 日 [設定](#access-configuration-options-content-hub) ユーザ インタフェース、クリック **[!UICONTROL フィルター]**.

1. クリック **[!UICONTROL フィルターを追加]**.

1. フィルターのラベルを指定し、 **[!UICONTROL メタデータ]** 新しいフィルターの入力タイプを選択します。
1. クリック **[!UICONTROL 確認]**. 新しいフィルターが既存のフィルターのリストに表示されます。

1. クリック **[!UICONTROL 保存]** アセットのフィルタリング時に新しいフィルターが検索ページに表示されるように変更を適用します。

   >[!NOTE]
   >
   >新しいフィルターは、フィルター条件に一致するアセットがリポジトリー内に最後に 1 つ存在する場合にのみ、検索ページに表示されます。

同様に、 ![編集アイコン](assets/do-not-localize/edit_icon.svg)使用可能な各フィルターの横にあるを使用して、ラベルを編集するか、削除アイコンをクリックして既存のフィルターを削除できます。 クリック **[!UICONTROL 保存]** すべての変更を加えて変更を適用した後。

![Content Hubの設定 UI フィルター](assets/configuration-ui-filters.png)

設定ユーザーインターフェイスで有効になっているフィルターは、検索ページに表示されます。

![Content Hubで検索](assets/filters-for-search.png)


### アセットの詳細 {#configure-asset-details-content-hub}

また、ファイル名、タイトル、形式、サイズなど、各アセットに対して表示されるアセットプロパティを設定することもできます。 これを行うには、次の手順を実行します。

1. 日 [設定](#access-configuration-options-content-hub) ユーザ インタフェース、クリック **[!UICONTROL アセットの詳細]**.

1. クリック **[!UICONTROL メタデータを追加]**.

1. プロパティのラベルを指定し、 **[!UICONTROL メタデータ]** フィールドに入力し、新しいアセットメタデータの入力タイプを選択します。
1. クリック **[!UICONTROL 確認]**. 新しいメタデータが、既存のアセットプロパティのリストに表示されます。

1. クリック **[!UICONTROL 保存]** 新しいプロパティがアセットの詳細ページに表示されるように変更を適用します。

同様に、 ![編集アイコン](assets/do-not-localize/edit_icon.svg)使用可能な各プロパティの横にあるを使用してラベルを編集するか、削除アイコンをクリックして既存のアセットの詳細を削除します。 クリック **[!UICONTROL 保存]** すべての変更を加えて変更を適用した後。

![Content Hubの設定 UI アセットの詳細](assets/configuration-ui-asset-details.png)

設定ユーザーインターフェイスで有効にしたプロパティがアセットの詳細ページに表示されます。

![Content Hubのアセットプロパティ](assets/config-ui-asset-properties.png)

### 検索 {#configure-metadata-search-content-hub}

管理者は、ユーザーがContent Hubで検索条件を指定した際に検索されるメタデータフィールドを定義できます。 以下の手順を実行します。

1. 日 [設定](#access-configuration-options-content-hub) ユーザ インタフェース、クリック **[!UICONTROL メタデータを追加]**.

1. メタデータフィールドを指定し、 **[!UICONTROL 確認]**.

1. クリック **[!UICONTROL 保存]** 新しいメタデータプロパティがメタデータフィールドのリストに表示されるように、変更を適用します。

同様に、 ![編集アイコン](assets/do-not-localize/edit_icon.svg)使用可能な各メタデータプロパティの横にあるを使用して、プロパティを編集するか、削除アイコンをクリックして既存のプロパティを削除します。 クリック **[!UICONTROL 保存]** すべての変更を加えて変更を適用した後。

![Content Hubでの Configuration UI 検索](assets/configuration-ui-metadata-search.png)


### ブランディング {#configure-branding-content-hub}

また、管理者は、ブランディング要件に従って、Content Hub ポータルのバナーに表示されるタイトルと本文をパーソナライズすることもできます。 これを行うには、次の手順を実行します。

1. 日 [設定](#access-configuration-options-content-hub) ユーザ インタフェース、クリック **[!UICONTROL ブランド化]**.

1. テキストを指定 **[!UICONTROL バナーのタイトルテキスト]** および **[!UICONTROL バナーの本文]** フィールド。

1. 「**[!UICONTROL 保存]**」をクリックして、変更内容を適用します。

![Content Hubの設定 UI ブランディング](assets/configuration-ui-branding.png)

設定ユーザーインターフェイスで有効にしたブランディングのアップデートは、Content Hub ポータルバナーに表示されます。

![Content Hubの設定 UI ブランディング](assets/configuration-ui-branding-updates.png)

### カスタムリンク {#configure-custom-links-content-hub}

標準に加えて、カスタムタブを追加することもできます **[!UICONTROL すべてのAssets]**, **[!UICONTROL コレクション]**、および **[!UICONTROL インサイト]** バナーのすぐ下のContent Hub ポータル上のタブ これを行うには、次の手順を実行します。

1. 日 [設定](#access-configuration-options-content-hub) ユーザ インタフェース、クリック **[!UICONTROL カスタムリンク]**.

1. クリック **[!UICONTROL リンクを追加]**.

1. テキストを指定 **[!UICONTROL ラベル]** および **[!UICONTROL URL]** フィールド。 定義するラベルはタブとして表示され、ラベルをクリックすると、 **[!UICONTROL URL]** フィールド。

1. 「**[!UICONTROL 確認]**」をクリックします。

1. 「**[!UICONTROL 保存]**」をクリックして、変更内容を適用します。

同様に、 ![編集アイコン](assets/do-not-localize/edit_icon.svg)各 URL の横にあるを使用してリンクを編集するか、削除アイコンをクリックして既存の URL を削除できます。 クリック **[!UICONTROL 保存]** すべての変更を加えて変更を適用した後。

![Content Hubの設定 UI カスタムリンク](assets/configuration-ui-custom-links.png)

カスタムリンクは、Content Hub ホームページで「インサイト」タブの横に新しいタブとして表示されます。

![Content Hubの設定 UI カスタムリンク タブ](assets/configuration-ui-custom-link-tab.png)


