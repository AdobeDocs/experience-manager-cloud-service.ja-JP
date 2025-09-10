---
title: 以前にデプロイされたソースコードを復元
description: パイプラインの実行を必要とせずに、環境を最後の正常なビルドに復元する方法を説明します。
feature: Operations
role: Admin
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: 8f804f55-a66d-47ad-a48d-61b861cef4f7
source-git-commit: 650ef846b469337c96e728277af02ca890e85117
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 92%

---

# AEM as a Cloud Service で以前にデプロイされたソースコードを復元する {#restore-previous-code-deployed}

>[!NOTE]
>
>この記事で説明する機能は、Beta プログラムを通じてのみ使用できです。Beta に新規登録するには、[パイプラインデプロイメントのワンクリックロールバック](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback)を参照してください。

**デプロイした以前のコードを復元**&#x200B;を使用すると、パイプラインの実行を必要とせずに、環境を最後に成功したビルドに即座にロールバックできます。

選択した環境の ![詳細アイコンまたは省略記号メニューアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) メニューを開き、**復元**／**デプロイした以前のコード**&#x200B;を選択するだけで、秒単位で最後にデプロイしたソースコードをロールバックできます。

>[!TIP]
>
>使用中のアクティブなソースコードのバージョンは、環境の詳細ビューの「**一般**」タブで確認できます。[環境の詳細の表示](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)を参照してください。
>
>![使用中のソースコードバージョン](/help/operations/assets/environments-view-details-sourcecodeversion.png)

**デプロイした以前のコードを復元**&#x200B;機能は、以下の&#x200B;**すべて**&#x200B;の条件が true の場合にのみ使用可能です。

* 正常なパイプライン実行ごとに許可される復元は 1 つだけです。再び復元するには、別の正常なパイプライン実行を完了します。
* **環境の復元の作成**&#x200B;権限を保持している。権限の管理について詳しくは、[カスタム権限](/help/implementing/cloud-manager/custom-permissions.md)を参照してください。
* 組織が Beta プログラムに登録され、機能フラグがオンになっている。
* プログラムが AEM as a Cloud Service で実行されている。
* 以前のソースコードの復元は、`Development` 環境、`Stage` 環境または `Specialized Testng Environment` で実行できます。
* この環境の最後のパイプラインが正常に完了し、実行から **30 日未満**&#x200B;である。
* 環境のステータスが&#x200B;*実行中*&#x200B;で、進行中のパイプラインがない。

復元：選択した環境は、`Development` ージ、ステージまたは専用のテスト環境です。
いずれかの確認に失敗した場合、Cloud Manager では、次のダイアログボックスが開き、満たされていない条件が 1 つ以上リストされ、**確認**&#x200B;が無効になり、復元が防止されます。

![デプロイした以前のコードを復元エラーダイアログボックス](/help/operations/assets/restore-previous-code-deployment-not-allowed.png)。

紛失したデータ、破損したデータ、誤って削除されたデータを元の状態に復元する場合は、[AEM as a Cloud Service でのコンテンツ復元](/help/operations/restore.md)を使用できます。この復元プロセスが影響するのはコンテンツのみで、AEM のソースコードとバージョンは変更されません。

**デプロイした以前のコードを復元するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 復元を開始するプログラムをクリックします。

1. 次のいずれかの操作を行って、プログラムのすべての環境をリストします。

   * 左側のサイドメニューの&#x200B;**サービス**&#x200B;で、![データアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)「**環境**」をクリックします。

     ![「環境」タブ](assets/environments-1.png)

   * 左側のサイドメニューの&#x200B;**プログラム**&#x200B;で「**概要**」をクリックし、**環境**&#x200B;カードから ![ワークフローアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)「**すべて表示**」をクリックします。

     ![「すべて表示」オプション](assets/environments-2.png)

     >[!NOTE]
     >
     >**環境**&#x200B;カードには、3 つの環境のみがリストされます。 カードの「**すべて表示**」をクリックすると、プログラムの&#x200B;*すべて*&#x200B;の環境が表示されます。

1. 環境テーブルで、ソースコードを復元する環境の右側にある ![詳細アイコンまたは省略記号メニューアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、次に&#x200B;**復元**／**デプロイした以前のコード**&#x200B;をクリックします。

   ![省略記号メニューからの「デプロイした以前のコードを復元」オプション](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. **デプロイした以前のコードを復元ダイアログボックス**&#x200B;で、現在デプロイされているバージョンと復元するバージョンを確認し、「**確認**」をクリックします。

   ![デプロイした以前のコードを復元ダイアログボックス](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. Cloud Manager は、環境を以前のビルドにロールバックし、コンテンツと設定をそのままの状態に保ち、デプロイメントが完了するまで環境ページで環境に&#x200B;**復元中**&#x200B;とマークを付けます。

   ![アクティベーションの復元](/help/operations/assets/restore-previous-code-deployed-restoring.png)
