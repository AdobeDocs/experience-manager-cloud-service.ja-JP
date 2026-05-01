---
title: 承認されたビデオにビデオスマート切り抜きを適用する
description: OpenAPI機能を備えたDynamic Mediaを使用すると、Adobe Experience Manager（AEM）で承認済みビデオアセット用のビデオスマート切り抜き出力を自動生成できます。
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: video-smartcrop-dmwoapi
source-git-commit: 8ddd2ade491069e4592becf3b77c04e6bbb2c06a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 7%

---


# 承認されたビデオにビデオスマート切り抜きを適用する {#apply-video-smart-crops-dmwoapi}

[!DNL Dynamic Media with OpenAPI capabilities]を使用すると、[!DNL Adobe Experience Manager (AEM)]でビデオアセットのビデオスマート切り抜き出力を自動的に生成できます。 ビデオスマート切り抜きビデオコンテンツを分析し、フレームを動的に調整して、様々な縦横比やデバイスをまたいで主要な被写体に焦点を当てることができます。

機能が有効になり、ビデオアセットが承認されると、ビデオスマート切り抜きが自動的に生成されます

## 始める前に {#prerequisites-for-video-smart-crops}

次の点を確認します。

* [!DNL AEM Assets as a Cloud Service] にアクセスします。
* メタデータスキーマを編集する権限。
* お使いの環境でOpenAPI機能が有効になっているDynamic Media。
* **[!UICONTROL Approved]**&#x200B;としてマークできるビデオアセット。

## ビデオのスマート切り抜きを有効にする {#enable-video-smart-crops}

ビデオスマート切り抜きを有効にするには、ビデオアセットに使用するメタデータスキーマを設定します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
2. 該当するメタデータスキーマを開きます（例：**default**）。
3. **ビデオ** フォームを選択し、**[!UICONTROL 編集]**&#x200B;をクリックします。
4. 新しい&#x200B;**[!UICONTROL ドロップダウンフィールド]**&#x200B;を追加し、次の設定を行います。

   * **フィールドラベル**：ビデオのスマート切り抜きを作成
   * **プロパティにマッピング**：`./jcr:content/dam:applyVideoSmartCrop`

5. 次の値を手動で追加します。

   * はい→true
   * No → false

6. スキーマを保存します。

**ビデオ スマート切り抜きを作成** オプションが、ビデオアセットのメタデータフォームで使用できるようになりました。

![&#x200B; ビデオ スマート切り抜きフィールドを作成](/help/assets/assets/video-smartcrop-metadata-field.png)

## 承認されたビデオにビデオスマート切り抜きを適用する {#apply-video-smart-crops}

メタデータフィールドを有効にしてアセットを承認すると、ビデオスマート切り抜きをビデオアセットに適用できます。

次の手順を実行します。

1. [!DNL Assets View] で「**[!UICONTROL Assets]**」を選択し、フォルダーに移動します。
2. ビデオアセットの選択。
3. 「**[!UICONTROL 詳細]**」をクリックします。
4. メタデータパネルで、**[!UICONTROL ビデオのスマートクロップを作成]**&#x200B;を見つけます。
5. 値を&#x200B;**Yes**&#x200B;に設定し、**[!UICONTROL 保存]**&#x200B;をクリックします。
6. アセットステータスを&#x200B;**[!UICONTROL Approved]**&#x200B;に設定します。

アセットが承認されると、ビデオスマート切り抜き出力が自動的に生成されます。

## ビデオのスマート切り抜き出力の表示 {#view-video-smart-crops}

ビデオスマート切り抜きが生成されたら：

* 出力は、ビデオ再生中に利用できます。
* Dynamic Media ビューアは、デバイスと縦横比に基づいて最適な切り抜きを自動的に選択します。
* ビデオの再生は、主要な被写体の焦点を合わせるように動的に調整されます。

## ビデオスマート切り抜きビデオの使用 {#use-video-smart-crops}

ビデオスマート切り抜き出力は、ビデオアセットが配信される場所で次のように使用できます。

* web ページ
* Applications
* 埋め込み型ビデオプレーヤー

ビューアは、再生中に適切なスマート切り抜きを自動的に適用します。

>[!NOTE]
>
>* ビデオスマート切り抜きは、**承認済み**&#x200B;個のビデオアセットに対してのみ生成されます。
>* アセットを承認する前に、**ビデオのスマートクロップを作成** フィールドが&#x200B;**はい**&#x200B;に設定されていることを確認してください。
>* ビデオスマート切り抜きは、元のアセットを変更しません。 トリミングは、再生中に動的に適用されます。