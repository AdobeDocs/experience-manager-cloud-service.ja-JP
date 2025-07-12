---
title: デプロイされた以前のSource コードを復元します
description: パイプラインの実行を必要とせずに、環境を最後に成功したビルド&ndash；に復元する方法を説明します。
feature: Operations
role: Admin
badge: label="アルファ" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: 8f804f55-a66d-47ad-a48d-61b861cef4f7
source-git-commit: 19e23785f2c4fbfa5a244864fe16500c1e7e128b
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 7%

---

# AEM as a Cloud Serviceにデプロイされた以前のソースコードを復元します {#restore-previous-code-deployed}

>[!NOTE]
>
>この記事で説明する機能は、早期導入アルファプログラムでのみ使用できます。 アルファ版にサインアップするには、[ パイプラインデプロイメントのワンクリックロールバック ](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback) を参照してください。

**デプロイされた以前のコードを復元** を使用して、環境を最後に成功したビルドに即座にロールバックできます。パイプラインを実行する必要はありません。

選択した環境の ![ 詳細アイコンまたは省略記号メニューアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) メニューを開き、**復元**/**以前にデプロイされたコード** を選択するだけで、最新にデプロイされたソースコードを秒単位でロールバックできます。

>[!TIP]
>
>環境の詳細ビューの「**一般**」タブで、使用中のアクティブなソースコードバージョンを確認できます。 [ 環境の詳細を表示 ](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) を参照してください。
>
>![ 使用中のSource コード バージョン ](/help/operations/assets/environments-view-details-sourcecodeversion.png)

**以前にデプロイしたコードを復元** 機能は、以下の **すべて** 条件が true の場合にのみ使用できます。

* **環境の復元の作成** 権限を保持します。 権限の管理について詳しくは、[ カスタム権限 ](/help/implementing/cloud-manager/custom-permissions.md) を参照してください。
* 組織が早期導入プログラムに登録され、機能フラグがオンになっています。
* プログラムはAEM as a Cloud Serviceで実行されます。
* 選択した環境は `Development` 環境です（Alphaの一時的な制限）。
* その環境の最後のパイプラインは正常に終了し、**10 日未満** 前に実行されました。
* 環境のステータスは *実行中* で、進行中のパイプラインはありません。
* 復元するターゲットソースコードバージョンが **30 日以内に** デプロイされました。

いずれかのチェックが失敗した場合、Cloud Managerでは次のダイアログボックスが開き、1 つ以上の未適合の条件が一覧表示されます。このダイアログボックスは無効になり **確認**、復元できません。

![ 以前にデプロイしたコードを復元できませんでしたダイアログボックス ](/help/operations/assets/restore-previous-code-deployment-not-allowed.png)。

失われた、破損した、または誤って削除されたデータを元の状態に復元するだけの場合は、[AEM as a Cloud Serviceのコンテンツを復元 ](/help/operations/restore.md) を使用できます。 この復元プロセスが影響するのはコンテンツのみで、ソースコードとAEMのバージョンは変更されません。

**デプロイされた以前のコードを復元するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 復元を開始するプログラムをクリックします。

1. 次のいずれかの操作を行って、プログラムのすべての環境をリストします。

   * 左側のメニューの **サービス** で、![ データアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)**環境** をクリックします。

     ![「環境」タブ](assets/environments-1.png)

   * 左側のメニューの **プログラム** で **概要** をクリックし、**環境** カードで ![ ワークフローアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)**すべて表示** をクリックします。

     ![「すべて表示」オプション](assets/environments-2.png)

     >[!NOTE]
     >
     >**環境** カードには 3 つの環境のみ表示されます。 カードの **すべて表示** をクリックすると、プログラムの *すべて* の環境が表示されます。

1. 環境テーブルで、ソースコードを復元する環境の右側にある ![ 詳細アイコンまたは省略記号メニューアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、**復元**/**以前にデプロイされたコード** をクリックします。

   ![ 省略記号メニューから「以前にデプロイしたコードを復元」オプションを選択 ](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. **以前にデプロイしたコードを復元** ダイアログボックスで、現在デプロイされているバージョンと復元するバージョンを確認し、「**確認**」をクリックします。

   ![ 以前にデプロイしたコードを復元ダイアログボックス ](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. Cloud Managerは、環境を以前のビルドにロールバックし、コンテンツと設定を元の状態に保ち、デプロイメントが完了するまで環境ページに環境をマーク **復元** します。

   ![ アクティベーションの復元 ](/help/operations/assets/restore-previous-code-deployed-restoring.png)
