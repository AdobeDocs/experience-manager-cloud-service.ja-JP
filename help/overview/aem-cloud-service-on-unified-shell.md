---
title: 統合シェルでas a Cloud ServiceのAEMを使用
description: 統合シェルでas a Cloud ServiceのAEMを使用
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: 51ecb21bf479cfaacb01a9c99c88d7f112f6ff95
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 6%

---

# 統合シェルでas a Cloud ServiceのAEMを使用 {#aem-as-a-cloud-service-on-unified-shell}

>[!NOTE]
>この機能は 2022 年 7 月のプレリリースチャネルにあります。
>
>これは、2022 年 8 月のリリースで一般に利用可能になる新機能の紹介です。
>
>お使いの環境でこの機能を有効にする方法については、[プレリリースチャネルのドキュメント](/help/release-notes/prerelease.md#enable-prerelease)を参照してください。

## 概要 {#overview}

AEM as a Cloud Serviceは、Unified Shell と統合され、ユーザーエクスペリエンスを向上し、他のすべてのExperience Cloudアプリケーションと統合します。 この統合の影響は、次に示すように、アプリケーションの上部のヘッダーで確認できます。

![画像](/help/overview/assets/unifiedshell1.png)

この利点は次のとおりです。

* すべてのExperience Cloud・アプリケーションでのシングル・サインオン
* 組織間の切り替えや、別のアプリケーションへの切り替えが容易
* 製品ヘルプの改善
* 製品内でのフィードバックボタンを使用して、問題を報告したり、Adobeとアイデアを共有したりできます。
* AEMas a Cloud Serviceに特有の通知に加えて、グローバルな製品のお知らせや通知にアクセス

## 統合シェルの無効化 {#disabling-unified-shell}

標準では、AEM as a Cloud Serviceは統合シェルを有効にしています。 ただし、トップヘッダーがカスタマイズされている場合は、カスタマイズの問題を回避するために、統合シェルを無効にすることをお勧めします。 統合シェルを無効にするには、次の手順に従います。

>[!NOTE]
>統合シェルは、管理者権限を持つアカウントでのみ無効にできます。

1. に移動します。 **ツール/Cloud Services**.

   管理者ユーザーには、次に示すように、統合シェル構成カードが表示されます。

   ![画像](/help/overview/assets/unifiedshell2.png)

1. クリック **統合シェル構成**. 次に、次に示すチェックボックスの選択を解除して、統合シェルを無効にします。

   ![画像](/help/overview/assets/unifiedshell3.png)

## ダークテーマに変更 {#changing-to-dark-theme}

ダークテーマに変更するには、自分のプロファイルアイコンをクリックします。 これにより、次に示すようにポップオーバーが表示されます。 切り替えを使用して、統合シェルのダークテーマに切り替えることができます。

>[!INFO]
>
>ダークテーマは、統合シェル（上部のバー）にのみ適用されます。

![画像](/help/overview/assets/unifiedshell4.png)

## AEMインボックスへのアクセス {#accessing-the-aem-inbox}

AEMインボックスにアクセスするには、統合シェルのベルのアイコンをクリックします。

>[!INFO]
>
> ベルのアイコンに表示される数字には、その IMS 組織内のすべてのソリューションおよびAEMインボックスに一覧表示されるタスクにわたって未読の通知が含まれます。

![画像](/help/overview/assets/unifiedshell5.png)

ポップアップの「インボックス」ボタンをクリックして、AEMインボックスに移動します。

![画像](/help/overview/assets/unifiedshell6.png)
