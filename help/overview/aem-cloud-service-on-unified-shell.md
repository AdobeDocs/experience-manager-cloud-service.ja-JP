---
title: 統合シェルでの AEM as a Cloud Service
description: 統合シェルでの AEM as a Cloud Service
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: 53e22737e62835872e47ac07530078c3d1dfcf31
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 65%

---

# 統合シェルでの AEM as a Cloud Service {#aem-as-a-cloud-service-on-unified-shell}

>[!NOTE]
>この機能は 2022 年 7 月のプレリリースチャネルにあります。
>
>これは、2022 年 8 月のリリースで一般に利用可能になる新機能の紹介です。
>
>お使いの環境でこの機能を有効にする方法については、[プレリリースチャネルのドキュメント](/help/release-notes/prerelease.md#enable-prerelease)を参照してください。

## 概要 {#overview}

AEMas a Cloud Service（オーサーサービス）は、統合シェルと統合され、ユーザーエクスペリエンスを向上し、他のすべてのExperience Cloudアプリケーションと統合します。 この統合の影響は、次に示すように、アプリケーションの上部のヘッダーで確認できます。

![画像](/help/overview/assets/unifiedshell_header.png)

この利点は次のとおりです。

* すべての Experience Cloud アプリケーションでシングルサインオン
* 組織間の切り替えや別のアプリケーションへの切り替えが簡単
* 製品ヘルプを改善
* 製品内の使いやすいフィードバックボタンを使用して、アドビへの問題の報告やアイデアの共有が可能
* AEMas a Cloud Serviceに特有の通知に加えて、グローバルな製品のお知らせや通知にアクセス

## 統合シェルの無効化 {#disabling-unified-shell}

標準提供の AEM as a Cloud Service では、統合シェルが有効になっています。ただし、トップヘッダーがカスタマイズされている場合は、カスタマイズの問題を回避するため、統合シェルを無効にすることをお勧めします。統合シェルを無効にするには、次の手順に従います。

>[!NOTE]
>統合シェルは、管理者権限を持つアカウントでのみ無効にできます。

1. **ツール／クラウドサービス**&#x200B;に移動します。

   管理者ユーザーには、次に示すように、統合シェル設定カードが表示されます。

   ![画像](/help/overview/assets/unifiedshell2.png)

1. 「**統合シェル設定**」をクリックします。次に、以下に示すチェックボックスの選択を解除して、統合シェルを無効にします。

   ![画像](/help/overview/assets/unifiedshell3.png)

## ダークテーマへの変更 {#changing-to-dark-theme}

ダークテーマに変更するには、自分のプロファイルアイコンをクリックします。これにより、次に示すようにポップオーバーが表示されます。切替スイッチを使用して、統合シェルをダークテーマに切り替えることができます。

>[!INFO]
>
>ダークテーマは、統合シェル（上部のバー）にのみ適用されます。

![画像](/help/overview/assets/unifiedshell4.png)

## AEMas a Cloud Service環境の識別 {#identify-aemaacs-environment}

AEMas a Cloud Serviceは、次の 3 種類の環境を提供します。実稼動、ステージング、開発。 参照： [環境タイプ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en) を参照してください。 この統合シェルとの統合により、以下に示すように、オーサーサービスにログインしているユーザーの環境のタイプが、上部のヘッダーにラベルを付けて表示されます。

![画像](/help/overview/assets/unifiedshell_header_label.png)


## AEM インボックスへのアクセス {#accessing-the-aem-inbox}

AEM インボックスにアクセスするには、統合シェルのベルのアイコンをクリックします。

>[!INFO]
>
> ベルのアイコンに示されている数字には、その IMS 組織内のすべてのソリューションと AEM インボックスに一覧表示されるタスクにわたる未読の通知が含まれます。

![画像](/help/overview/assets/unifiedshell5.png)

ポップオーバーの「インボックス」ボタンをクリックして、AEM インボックスに移動します。

![画像](/help/overview/assets/unifiedshell6.png)
