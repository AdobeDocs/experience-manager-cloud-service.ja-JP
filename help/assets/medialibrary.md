---
title: 基本的なデジタルアセット管理にメディアライブラリを使用する
description: '[!DNL Experience Manager Assets] およびアセット管理用のメディアライブラリ。'
contentOwner: AG
role: 建築家、リーダー
translation-type: tm+mt
source-git-commit: db74b206439e5e9d6c1526c7baa05e5a17997702
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 基本的なアセット管理にメディアライブラリを使用{#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] プラットフォームは、アセットを管理するための様々な機能を提供します。Media Libraryを使用すると、少数のアセットをリポジトリにアップロードし、Webページ内でアセットを検索して使用し、アセットに対する単純なアセット管理タスクを実行できます。

Media Libraryは、[!DNL Adobe Experience Manager Sites]ライセンスを補完する軽量のDigital Asset Management(DAM)ソリューションです。 [!DNL Sites] は、Webコンテンツ管理(WCM)の製品です。メディアライブラリは、Experience Managerのすべての機能と連携します。

[!DNL Adobe Experience Manager Assets] ライセンスは別途購入可能です。[!DNL Experience Manager Assets] 企業の使用例を介したアセットの堅牢な処理、メタデータ、スキーマ、検索、ユーザーインターフェイスのカスタマイズ、およびMedia Libraryの機能を超える多数の機能を利用できます。

## ライセンス要件{#avail-media-library-license}

[!DNL Sites]ライセンスを持つお客様は、Media Libraryを使用する権利が与えられます。 [!DNL Experience Manager]の全てのコンポーネントで機能します。

メディアライブラリがサイトの一部としてインストールされます。 サイトのライセンスおよびインストール以外に追加のライセンスまたはパッケージは必要ありません。

## [!DNL Assets] 対するメディアライブラリ  {#assets-and-media-library}

Experience Managerアセットは、エンタープライズグレードのDAM機能を提供します。 アセット機能は、[!DNL Experience Manager]と共に1つのパッケージとして提供されます。 ただし、アセットライセンスを購入していないユーザーは、高度なDAM機能を使用する権利を持ちません。 アセットライセンスがない場合は、[メディアライブラリ機能](#use-media-library)のみ使用できます。

ライセンスを取得していない[!DNL Assets]機能の意図しない使用を防ぐには、[!DNL Assets]固有のワークフロー、コンポーネント、分類、オプション、および[!DNL Assets]管理者をすべて[!DNL Experience Manager]から削除します。 これにより、ライセンスを取得していない[!DNL Assets]機能を誤ってユーザが使用するのを防ぐことができます。

## メディアライブラリを使用{#use-media-library}

Media Libraryは、次の使用例を大まかにカバーしています。

* [!DNL Adobe Experience Manager Sites]を使用して作成したWebページに、基本的なDAM機能を提供します。
* [!DNL Adobe Experience Manager Forms]を使用して作成されたアダプティブフォームと通信
* [!DNL Adobe Experience Manager Screens]を使用して作成されたデジタル画面の操作。
* [!DNL Assets] HTTP REST API（ヘッドレス操作用）

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

メディアライブラリ機能を使用するには、デフォルトの[!DNL Experience Manager]ユーザーインターフェイスを使用できます。 Media Libraryは[!DNL Experience Manager Sites]インストールの一部であり、別のインターフェイスやアドオンを必要としません。 既存のインターフェイスを使用して、Media Libraryのユーザーは次のタスクを実行する権利があります。

* フォルダーを作成してアセットを整理します。
* アセットのアップロード.
* アセットの公開.
* アセットの編集、移動およびコピーを行います。
* アセットの参照、フィルタリングおよび検索（類似性検索を含む）を行います。
* 「スマートタグ」フィールドを除き、メタデータフィールドの値に対する値および編集追加値。このフィールドは、アセットの[!UICONTROL プロパティ]ページの「[!UICONTROL 基本]」タブでデフォルトで使用できます。
* 静的レンディションの追加削除を行います。
* フォルダ、アセット、アセットレンディションをダウンロードします。
* アセットのバージョンを作成します。
* アセットに対してレビュータスクを作成し、実行します。
* アセットに注釈を付けます。
* コンテン追加ツファインダーを使用して[!DNL Sites]ページにアセットを追加。
* 使用方法 [!DNL Content Fragments].

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>高度なDAMの使用例の多くは[!DNL Experience Manager Assets]によって満たされます。 Media Libraryのライセンスでは、Media Libraryを使用して、一覧に示されている使用例のみを満たす権限を与えられます。 使用事例が一覧に表示されない場合は、Media Libraryライセンスで使用しないでください。 クエリがある場合は、Adobeカスタマーケアにお問い合わせください。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [DAM機能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=ja)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)

