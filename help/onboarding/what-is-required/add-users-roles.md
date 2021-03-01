---
title: 追加ユーザーと役割 — 必要なもの
description: 追加ユーザーと役割 — 必要なもの
translation-type: tm+mt
source-git-commit: 2c21414edd6c3178d05c818d2bf57aa152b5956b
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 63%

---


# ユーザーとロールの追加 {#add-users-roles}


[!UICONTROL Cloud Manager] の多くの機能には、使用するための特定の権限が必要です。

[!UICONTROL Cloud Manager] では、現在、特定の機能を使用できるかどうかを制御する次の 4 つのユーザーロールを定義しています。

* ビジネスオーナー
* プログラムマネージャー
* デプロイメントマネージャー
* デベロッパー

>[!CAUTION]
>
>[!UICONTROL Cloud Manager]を使用するには、Cloud Service製品コンテキストとして、Adobe IDとAdobe Experience Managerが必要です。

## ロールの定義 {#role-definitions}

>[!NOTE]
>
>Admin Console の「開発者」ペルソナは、[!UICONTROL Cloud Manager] の「デベロッパー」ロールとは無関係です。

ロールの概要を次の表に示します。

| [!UICONTROL Cloud Manager] のロール | 説明 |
|--- |--- |
| ビジネスオーナー | KPI の定義、実稼動デプロイメントの承認、重大な 3 層エラーのオーバーライドを担当します。 |
| プログラムマネージャー | [!UICONTROL Cloud Manager] を使用して、チームの設定、ステータスのレビュー、KPI の確認をおこないます。重大な 3 層エラーを承認することができます。 |
| デプロイメントマネージャー | デプロイメント作業を管理します。[!UICONTROL Cloud Manager] を使用して、ステージング環境または実稼動環境へのデプロイメントを実行します。CI/CD パイプラインを編集できます。重大な 3 層エラーを承認することができます。Git リポジトリにアクセスできます。 |
| デベロッパー | カスタムアプリケーションコードを開発およびテストします。主に [!UICONTROL Cloud Manager] を使用してステータスを確認します。Git リポジトリにアクセスして、コードをコミットできます。 |
| コンテンツ作成者 | 通常は、[!UICONTROL Cloud Manager] を操作しません。（[!UICONTROL Experience Cloud] からナビゲートした）[!UICONTROL Cloud Manager] プログラムスイッチャーを使用して、AEM にアクセスできます。 |

## 統合製品プロファイル{#integration-product-profile}

上記に加えて、Cloud Managerでは「Integrations -Cloud Service」という製品プロファイルが自動的に作成されます。 この製品プロファイルは、Adobe Experience Manager製品と他のAdobe製品との統合に使用されます。 この製品プロファイル&#x200B;**は削除できません。** 誤ってこのプロファイルを削除した場合は、手動で再作成する必要があります。 このプロファイルの表示名&#x200B;**は**`CM_CS_DEFAULT`でなければなりません。
