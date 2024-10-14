---
title: サンドボックス環境の休止と休止解除
description: サンドボックスプログラムの環境が自動的に休止モードに入る仕組みと、休止状態が解除される仕組みについて説明します。
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 88b4864da30fbf201dbd5bde1ac17d3be977648f
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 47%

---


# サンドボックス環境の休止と休止解除 {#hibernating-introduction}

サンドボックスプログラムの環境は、8 時間操作が検出されなかった場合、休止モードに入ります。 休止状態は、サンドボックスプログラム環境に固有のものです。 実稼動プログラム環境は休止状態にできません。

## 休止状態 {#hibernation-introduction}

休止状態には、自動または手動で移行します。

* **自動** - サンドボックスプログラム環境は、8 時間、無操作状態になると、自動的に休止状態になります。無操作状態とは、オーサー、プレビュー、パブリッシュの各サービスに対するリクエストがないことと定義されます。
* **手動** - ユーザーはサンドボックスプログラム環境を手動で休止状態にできます。前述のとおり休止状態は自動的に発生するので、そのための要件はありません。

サンドボックスプログラム環境が休止モードに入るまで、数分かかる場合があります。休止中、データは保持されます。

### サンドボックスプログラム環境を手動で休止状態にする {#using-manual-hibernation}

開発者コンソールからサンドボックスプログラムを手動で休止状態にすることができます。サンドボックスプログラム用のDeveloper Consoleへのアクセスは、Cloud Managerの任意のユーザーが利用できます。

**サンドボックスプログラム環境を手動で休止状態にするには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、休止状態にする *サンドボックスプログラム* をクリックして詳細を表示します。

1. **環境** カードで、「詳細」アイコン ![ クリックし ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)、「**Developer Console**」をクリックします。

   * 詳しくは、[Developer Console へのアクセス](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)を参照してください。

   ![開発者コンソールのメニューオプション](/help/implementing/cloud-manager/assets/developer-console-menu-option.png)

1. **Developer Console** ページで、「休止 **をクリック** ます。

<!-- UPDATE THESE SCREENSHOTS WHEN NEW AEM DEVELOPER CONSOLE UI IS RELEASED. AS OF OCTOBER 14, 2024, NEW UI IS STILL IN BETA -->

![「休止」ボタン](assets/hibernate-1.png)

1. 「**休止**」をクリックして手順を確定します。

   ![休止の確定](assets/hibernate-2.png)

休止処理が正常に完了すると、環境の休止処理完了通知が **Developer Console** 画面に表示されます。

![休止状態の確認](assets/hibernate-4.png)

Developer Consoleで、「**ポッド**」ドロップダウンリストの上にあるパンくずリスト内の **環境** リンクをクリックして、休止状態に使用できる環境を表示します。

![休止状態にする環境のリスト](assets/hibernate-1b.png)

## サンドボックスプログラムの休止状態をDeveloper Consoleから手動で解除する {#de-hibernation-introduction}

Developer Consoleからサンドボックスプログラムを手動で休止状態にすることができます。

>[!IMPORTANT]
>
>**開発者**&#x200B;の役割を持つユーザーは、サンドボックスプログラム環境の休止状態を解除できます。

**Developer Consoleからサンドボックスプログラムの休止状態を手動で解除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、休止状態を解除するプログラムをクリックして詳細を表示します。

1. **環境** カードで、https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svgをクリックし、**Developer Console** をクリックします。

   * 詳しくは、[Developer Console へのアクセス](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)を参照してください。

1. 「**休止状態を解除**」をクリックします。

   ![「休止解除」ボタン](assets/de-hibernation-img1.png)

1. 「**休止解除**」をクリックして、手順を確定します。

   ![休止解除の確定](assets/de-hibernation-img2.png)

1. 休止解除プロセスが開始されたことを示す通知が届き、進行状況に合わせて情報が更新されます。

   ![休止解除の進行状況の通知](assets/de-hibernation-img3.png)

1. 処理が完了すると、サンドボックスプログラム環境が再度アクティブになります。

   ![休止解除の完了](assets/de-hibernation-img4.png)

Developer Consoleで、「**ポッド**」ドロップダウンリストの上にあるパンくずリスト内の **環境** リンクをクリックして、休止解除で使用できる環境にアクセスします。

![休止状態のポッドのリスト](assets/de-hibernate-1b.png)

### 休止状態を解除する権限 {#permissions-de-hibernate}

製品プロファイルで AEM as a Cloud Service へのアクセスが許可されている場合は、**開発者コンソール**&#x200B;にアクセスして環境の休止状態を解除できます。

## 休止状態の環境へのアクセス {#accessing-hibernated-environment}

休止状態の環境のオーサー、プレビューまたはパブリッシュサービスに対してユーザーがブラウザーリクエストを行うと、ランディングページが表示されます。 ここでは、環境の休止状態に関するステータスと、休止状態を解除するためのDeveloper Consoleへのリンクを示します。

![休止状態にあるサービスのランディングページ](assets/de-hibernation-img5.png)

## デプロイメントとAEMのアップデート {#deployments-updates}

休止状態の環境でも、デプロイメントと AEM の手動アップグレードが可能です。

* ユーザーは、パイプラインを使用して、休止状態の環境にカスタムコードを導入できます。環境は休止状態のままとなり、休止状態を解除すると、新しいコードが環境に表示されます。

* AEM のアップグレードは、休止状態の環境にも適用でき、Cloud Manager から手動でトリガーできます。環境は休止状態のままとなり、新しいリリースは、休止状態を解除すると環境に表示されます。

## 休止と削除 {#hibernation-deletion}

* サンドボックスプログラム内の環境は、8 時間、無操作状態になると、自動的に休止状態になります。
   * 無操作状態とは、オーサー、プレビュー、パブリッシュの各サービスに対するリクエストがないことと定義されます。
   * 休止状態になったら、[手動で休止状態を解除](#de-hibernation-introduction)できます。
* サンドボックスプログラムは、連続休止モードになってから 6 か月が経過すると削除され、その後再作成できます。

>[!NOTE]
>
>休止状態が 6 か月続いた後で自動的に削除されるのは、サンドボックス環境のみです。リポジトリとコードを含むサンドボックスプログラムは保持されます。
