---
title: Adobe InDesign用の配置専用レンディションを生成
description: アセットワークフローとImageMagickを使用して、新しいアセットと既存のExperience ManagerのFPOレンディションを生成します。
contentOwner: Vishabh Gupta
role: Admin
feature: レンディション
exl-id: null
source-git-commit: 69f1ac34dc24f92cae47e1bfcffb39f6f3b03b7b
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 8%

---

# Adobe InDesign用の配置専用レンディションを生成 {#fpo-renditions}

Experience Managerの大きなサイズのアセットをAdobe InDesignドキュメントに配置する場合、クリエイティブプロフェッショナルは、アセット[を配置してからかなりの時間待つ必要があります。](https://helpx.adobe.com/jp/indesign/using/placing-graphics.html) 一方、ユーザーは InDesign の使用をブロックされます。これにより、クリエイティブの流れが中断され、ユーザーエクスペリエンスに悪影響が出ます。Adobeでは、最初にInDesignドキュメントに小さいサイズのレンディションを一時的に配置できます。 印刷や公開ワークフローなど、最終的な出力が必要な場合は、元のフル解像度のアセットがバックグラウンドの一時レンディションを置き換えます。 このバックグラウンドでの非同期更新により、デザインプロセスが高速化され、生産性が向上し、クリエイティブプロセスが妨げられることはありません。

アセットには、配置専用(FPO)のレンディションが用意されています。 これらの FPO レンディションは、ファイルサイズは小さいですが、縦横比は同じです。FPOレンディションがアセットに使用できない場合、Adobe InDesignは元のアセットを代わりに使用します。 このフォールバックメカニズムにより、クリエイティブワークフローは中断することなく続行されます。

Experience Manageras aCloud Serviceは、FPOレンディションを生成するためのクラウドネイティブなアセット処理機能を提供します。 レンディションの生成にアセットマイクロサービスを使用する。 新しくアップロードされたアセットと、アセット内に存在するアセットのレンディションの生成をExperience Managerできます。

FPOレンディションを生成する手順は次のとおりです。
1. [処理プロファイルの作成](#create-processing-profile)を参照してください。
1. Experience Managerを設定し、このプロファイルを使用して[新しいアセット](#generate-renditions-of-new-assets)を処理します。
1. プロファイルを使用して、既存のアセットを[処理します。](#generate-renditions-of-existing-assets)

## 処理プロファイルの作成 {#create-processing-profile}

FPOレンディションを生成するには、**[!UICONTROL 処理プロファイル]**&#x200B;を作成します。 プロファイルは、処理にクラウドネイティブなアセットマイクロサービスを使用します。 手順については、[アセットマイクロサービスの処理プロファイルの作成](asset-microservices-configure-and-use.md)を参照してください。

「**[!UICONTROL FPOレンディションを作成]**」を選択してFPOレンディションを生成します。 必要に応じて、「**[!UICONTROL 新規追加]**」をクリックして、別のレンディション設定を同じプロファイルに追加します。

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## 新しいアセットのレンディションの生成 {#generate-renditions-of-new-assets}

新しいアセットのFPOレンディションを生成するには、フォルダープロパティのフォルダーに&#x200B;**[!UICONTROL 処理プロファイル]**&#x200B;を適用します。 フォルダーのプロパティページで、「**[!UICONTROL アセット処理]**」タブをクリックし、**[!UICONTROL FPOプロファイル]**&#x200B;を&#x200B;**[!UICONTROL 処理プロファイル]**&#x200B;として選択して、変更を保存します。 フォルダーにアップロードされた新しいアセットは、すべてこのプロファイルを使用して処理されます。

![add-fpo-rendition](assets/add-fpo-rendition.png)


## 既存のアセットのレンディションの生成 {#generate-renditions-of-existing-assets}

レンディションを生成するには、アセットを選択し、次の手順に従います。

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## FPOレンディションの表示 {#view-fpo-renditions}

ワークフローの完了後に、生成されたFPOレンディションを確認できます。 Experience ManagerAssetsユーザーインターフェイスで、アセットをクリックして大きなプレビューを開きます。 左側のレールを開き、「**[!UICONTROL レンディション]**」を選択します。 または、プレビューを開いたときにキーボードショートカット`Alt + 3`を使用します。

**[!UICONTROL FPOレンディション]**&#x200B;をクリックして、プレビューを読み込みます。 オプションで、レンディションを右クリックして、ファイルシステムに保存できます。 左側のパネルで、使用可能なレンディションを確認します。

![rendition_list](assets/list-renditions.png)
