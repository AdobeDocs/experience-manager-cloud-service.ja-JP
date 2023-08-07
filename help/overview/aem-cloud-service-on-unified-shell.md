---
title: 統合シェルでの AEM as a Cloud Service
description: 統合シェルでのAEMas a Cloud Serviceのメリットについて説明します。
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 76%

---

# 統合シェルでの AEM as a Cloud Service {#aem-as-a-cloud-service-on-unified-shell}

## 概要 {#overview}

AEM as a Cloud Service（オーサーサービス）は統合シェルと統合することにより、ユーザーエクスペリエンスが向上し、他のすべての Experience Cloud アプリケーションと統合できるようになりました。この統合の影響は、次に示すように、アプリケーションの上部のヘッダーで確認できます。

![画像](/help/overview/assets/unifiedshell_header.png)

この利点は次のとおりです。

* すべてのExperience Cloud・アプリケーションでのシングル・サインオン
* 組織間の切り替えや別のアプリケーションへの切り替えが簡単
* 製品ヘルプを改善
* 製品内の使いやすいフィードバックボタンを使用して、アドビへの問題の報告やアイデアの共有が可能
* AEM as a Cloud Service 固有の通知に加えて、製品のグローバルなお知らせや通知にもアクセス

## 統合シェルの無効化 {#disabling-unified-shell}

標準提供の AEM as a Cloud Service では、統合シェルが有効になっています。ただし、トップヘッダーがカスタマイズされている場合は、カスタマイズの問題を回避するため、統合シェルを無効にすることをお勧めします。統合シェルを無効にするには、次の手順に従います。

>[!NOTE]
>統合シェルは、管理権限を持つアカウントによってのみ無効にできます。

1. クリック **ツール/Cloud Services**.

   管理者ユーザーには、次に示すように、統合シェル構成カードが表示されます。

   ![画像](/help/overview/assets/unifiedshell2.png)

1. クリック **統合シェル構成**. 次に、以下に示すチェックボックスの選択を解除して、統合シェルを無効にします。

   ![画像](/help/overview/assets/unifiedshell3.png)

## ダークテーマへの変更 {#changing-to-dark-theme}

暗いテーマに変更するには、自分のプロファイルアイコンをクリックします。 このアクションは、次に示すように、ポップオーバーを表示します。 切替スイッチを使用して、統合シェルをダークテーマに切り替えることができます。

>[!INFO]
>
>ダークテーマは、統合シェル（上部のバー）にのみ適用されます。

![画像](/help/overview/assets/unifiedshell4.png)

## AEM as a Cloud Service 環境の識別 {#identify-aemaacs-environment}

AEM as a Cloud Service には、実稼動環境、ステージ環境、開発環境の 3 つの環境タイプがあります。詳しくは、 [環境タイプ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=ja) を参照してください。 この統合シェルとの統合により、以下に示すように、オーサーサービスにログインしているユーザーの環境タイプが、ラベルを介して上部ヘッダーに表示されます。

![画像](/help/overview/assets/unifiedshell_header_label.png)

## AEM インボックスへのアクセス {#accessing-the-aem-inbox}

AEMインボックスにアクセスするには、統合シェルでベルのアイコンをクリックします。

>[!INFO]
>
> ベルのアイコンに示されている数字には、その IMS 組織内のすべてのソリューションと AEM インボックスに一覧表示されるタスクにわたる未読の通知が含まれます。

![画像](/help/overview/assets/unifiedshell5.png)

ポップオーバーの「インボックス」ボタンをクリックして、AEMインボックスに移動できるようにします。

![画像](/help/overview/assets/unifiedshell6.png)
