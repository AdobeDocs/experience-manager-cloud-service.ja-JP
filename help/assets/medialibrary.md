---
title: 基本的なデジタルアセット管理にMedia Libraryを使用
description: '[!DNL Experience Manager Assets] とMedia Library（アセット管理用）'
contentOwner: AG
feature: アセット管理，公開
role: Business Practitioner,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 6%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 基本的なアセット管理にMedia Libraryを使用{#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] platformには、アセットを管理するための様々な機能が用意されています。Media Libraryを使用すると、少数のアセットをリポジトリにアップロードし、Webページで検索して使用し、アセットに対して簡単なアセット管理タスクを実行できます。

Media Libraryは、[!DNL Adobe Experience Manager Sites]ライセンスを補完する軽量のデジタルアセット管理(DAM)ソリューションです。 [!DNL Sites] は、Webコンテンツ管理(WCM)機能です。Media Libraryは、Experience Managerのすべての機能と連携します。

[!DNL Adobe Experience Manager Assets] ライセンスは別途購入可能です。[!DNL Experience Manager Assets] では、エンタープライズのユースケースを介したアセットの堅牢な処理、メタデータ、スキーマ、検索、ユーザーインターフェイスのカスタマイズ、Media Libraryの機能以外の様々な機能を利用できます。

## ライセンス要件{#avail-media-library-license}

[!DNL Sites]ライセンスを持つお客様は、Media Libraryを使用する権利があります。 [!DNL Experience Manager]のすべてのコンポーネントで機能します。

Media LibraryがSitesの一部としてインストールされます。 Sitesのライセンスとインストール以外に、追加のライセンスやパッケージは必要ありません。

## [!DNL Assets] と  Media Library {#assets-and-media-library}

Experience Managerアセットは、エンタープライズグレードのDAM機能を提供します。 アセット機能は、1つのパッケージに[!DNL Experience Manager]と共に提供されます。 ただし、Assetsライセンスを購入していないユーザーは、高度なDAM機能を使用する権利はありません。 Assetsライセンスがない場合、[Media Library機能](#use-media-library)のみ使用できます。

ライセンスを所有していない[!DNL Assets]機能を意図しない使用を防ぐには、[!DNL Assets]固有のワークフロー、コンポーネント、分類、オプションおよび[!DNL Assets]管理を[!DNL Experience Manager]からすべて削除します。 これによって、ユーザーがライセンスを所持していない [!DNL Assets] の機能を誤って使用することを防ぐことができます。

## Media Library {#use-media-library}を使用

Media Libraryでは、次の使用例を大まかに扱います。

* [!DNL Adobe Experience Manager Sites]を使用して作成されたWebページに対して、基本的なDAM機能を提供します。
* [!DNL Adobe Experience Manager Forms]を使用して作成されたアダプティブフォームと通信
* [!DNL Adobe Experience Manager Screens]を使用して作成されたデジタルスクリーンエクスペリエンス。
* [!DNL Assets] ヘッドレス操作用のHTTP REST API。

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

Media Library機能を使用するには、デフォルトの[!DNL Experience Manager]ユーザーインターフェイスを使用できます。 Media Libraryは[!DNL Experience Manager Sites]インストールに含まれており、別のインターフェイスやアドオンは必要ありません。 既存のインターフェイスを使用すると、Media Libraryユーザーは次のタスクを実行できます。

* フォルダーを作成してアセットを整理する。
* アセットのアップロード.
* アセットの公開.
* アセットの編集、移動およびコピー。
* アセットの参照、フィルタリングおよび検索（類似性検索を含む）。
* デフォルトでは、アセットの[!UICONTROL プロパティ]ページの「[!UICONTROL 基本]」タブで使用できる「スマートタグ」フィールドを除き、メタデータフィールドの値を追加および編集します。
* 静的レンディションを追加および削除します。
* フォルダー、アセット、アセットレンディションのダウンロード。
* アセットのバージョンを作成する。
* アセットに対してレビュータスクを作成および実行します。
* アセットに注釈を付ける。
* コンテンツファインダーを使用して[!DNL Sites]ページにアセットを追加します。
* 使用方法 [!DNL Content Fragments].

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>高度なDAMの使用例の多くは、[!DNL Experience Manager Assets]で処理されます。 Media Libraryライセンスでは、Media Libraryを使用して、記載されている使用例のみを満たすことができます。 使用例が一覧に表示されない場合は、Media Libraryライセンスで使用しないでください。 質問がある場合は、Adobeカスタマーケアにお問い合わせください。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [のDAM機能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=ja)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-cloud-service.html)

