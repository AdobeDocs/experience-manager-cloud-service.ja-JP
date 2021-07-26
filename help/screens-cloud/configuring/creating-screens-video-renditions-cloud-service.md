---
title: ScreensでのScreensビデオレンディションの作成(Cloud Service)
description: ここでは、ScreensでScreensビデオレンディションをCloud Serviceとして作成する方法について説明します。
source-git-commit: b8691bb77079eeb7efd141ce89c44c5a312262b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---


# ScreensでのScreensビデオレンディションの作成(Cloud Service) {#creating-screens-video-renditions}

## はじめに {#introduction}

このガイドでは、Screens Playerで使用するビデオレンディションの作成方法について説明します。

>[!IMPORTANT]
>Screensチャネルでビデオを使用する場合は、この節で取り上げる手順を設定する必要があります。

## ScreensでのScreensビデオレンディションの作成手順(Cloud Service) {#steps-creating-screens-video-renditions}

1. Screens Cloud UIのチャネルに移動します。
1. 左上隅のAdobe Experience Managerをクリックして、Screensコンテンツプロバイダー(AEM as aCloud Service)に移動します。
1. メインナビゲーションの「ツール」セクションをクリックし、「アセット」をクリックし、「処理プロファイル」をクリックします。

1. 「作成」をクリックして、新しい処理プロファイルを作成します。
1. 「ScreensProcessingProfile」などの名前を指定します。
1. 「ビデオ」タブに移動してビデオエンコーディングを追加し、「新規追加」をクリックします。


   >[!IMPORTANT]
   >「screens — 」で始まるエンコーディング名を使用するようにしてください。これらのビデオレンディションのみが、ScreensでビデオエクスペリエンスをCloud Serviceとして再生すると見なされます。 ビデオに適したビットレートを入力します（720pxビデオの場合は2,500 kbps、1,080pxの場合は5,000 kbps）。

   >[!NOTE]
   >必要に応じて様々な幅/高さ/ビットレートで複数のビデオレンディションを追加できますが、デバイスがビデオレンディションのみを再生しても、すべての画面レンディションがScreensデバイスにダウンロードされることに注意してください。

1. 「保存」をクリックします。

1. 処理プロファイルを選択し、「プロファイルをフォルダーに適用」をクリックします。

1. Screensビデオを保存するフォルダーを選択し、「適用」をクリックします。

1. 複数の処理プロファイルを作成し、対応するフォルダーに適用して、それらのフォルダー内のビデオが特定のビデオレンディションを取得できるようにします

1. 処理プロファイルが適用されているフォルダーにビデオをアップロードすると、ビデオが処理され、設定済みのレンディションが作成されます。このレンディションは、Screensデバイスでビデオを再生するために使用されます。

