---
title: アプリのコンテンツ構造の作成
description: AEMコンテンツフラグメントモデルを使用して、すべてのヘッドレスコンテンツの基盤となる構造を作成する方法を説明します。
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# アプリのコンテンツ構造の作成 {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="アプリのコンテンツ構造を作成する"
>abstract="この一連のインタラクティブガイドに従うことで、ヘッドレスコンテンツの基盤となる構造（コンテンツフラグメントモデルと呼ばれます）を作成する方法を学習できます。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="モデルコンソールを起動します。"
>abstract="Adobe Experience Manager as a Cloud Serviceのコンテンツに対して、コンテンツフラグメントモデルと呼ばれる再利用可能なスキーマを作成する方法を見てみましょう。 これが重要な手順である理由については、ビデオをご覧ください。 <br><br>下のボタンをクリックし、このガイドに従って、新しいタブでこのモジュールを起動します。"
>additional-url="https://video.tv.adobe.com/v/3413261" text="コンテンツ構造の概要ビデオ"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="おめでとうございます。ヘッドレスデータの構造を表すコンテンツフラグメントモデルを作成する方法を学び、オムニチャネルコンテンツを拡大/縮小/標準的な方法で配信する最初の手順を踏みました。"
>abstract=""

## モデルの作成 {#create-model}

クリック **モデルコンソールを起動します。** 上のボタンをクリックすると、新しいタブにコンテンツフラグメントモデルコンソールが開きます。

![コンテンツフラグメントモデルコンソール](assets/content-structure/content-fragment-model-console.png)

コンテンツフラグメントモデルコンソールは、新しいモデルの作成や既存のモデルの管理を行うモデルのライブラリと考えることができます。 コンソールが空になるので、新しいモデルを作成しましょう。

1. コンテンツフラグメントモデルコンソールで、 **作成** ボタンをクリックして、コンテンツフラグメントモデルの作成を開始します。

1. モデルの作成ウィザードが起動し、ガイドが表示されます。

   ![コンテンツフラグメントモデルウィザード](assets/content-structure/model-wizard.png)

   必須の情報を入力します。

   * **モデルタイトル**  — これはモデルの簡単な説明で、通常はモデルの目的を示します。
   * **モデルを有効にする**  — このオプションはデフォルトでオンになっています。このモデルに基づいてコンテンツフラグメントを作成するには、このオプションをオンにする必要があります。

1. 必須フィールドを入力したら、 **作成** をクリックして、モデルを作成します。

1. この **成功** モデルが作成されたことを確認するダイアログが表示されます。

   ![新しいコンテンツフラグメントモデルを作成するための成功ダイアログ](assets/content-structure/success.png)

## モデルにフィールドを追加 {#configure-model}

モデルを使用する前に、そのデータの構造を定義する必要があります。

1. クリック **開く** 内 **成功** 前の手順のダイアログで、コンテンツフラグメントモデルエディターで新しいモデルを開き、そのフィールドを定義できます。

1. フィールドを **データタイプ** エディターの右側のパネルを開き、コンテンツフラグメントモデルにドロップします。

   ![データタイプの追加](assets/content-structure/drop-fields.png)

1. データ型を配置すると、 **データタイプ** 列が自動的に **プロパティ** 」タブに移動し、配置したデータタイプの詳細を定義できます。

   ![データフィールドの「プロパティ」タブ](assets/content-structure/data-type-properties.png)

1. コンテンツフラグメントモデルに必要なすべてのフィールドを追加したら、 **保存** をクリックします。

モデルが保存され、コンテンツフラグメントモデルコンソールに戻り、必要に応じて他のモデルを追加できます。

![モジュール完了](assets/content-structure/content-fragment-model-console-populated.png)
