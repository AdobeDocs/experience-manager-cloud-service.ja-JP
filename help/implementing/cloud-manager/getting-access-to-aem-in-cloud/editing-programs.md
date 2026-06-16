---
title: プログラムの編集
description: 実稼動およびサンドボックスプログラムを編集し、作成後にオプションを調整する方法について説明します。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: fd729f12b4d6ff94ba4f3c86b8b8c1a0d3627c16
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 20%

---


# プログラムの編集 {#editing-programs}

プログラムを管理および編集するには、[**マイプログラム**&#x200B;コンソール](/help/implementing/cloud-manager/navigation.md)から開始します。 **マイプログラム**&#x200B;ページには、アクセス権を持つすべてのプログラムの概要が表示されます。 個々のプログラムを選択すると、**プログラムの概要** ページにプログラムの詳細の概要が表示されます。

必要な権限を持つユーザーは、**プログラムの概要**&#x200B;から、[組織内で作成された実稼動プログラム](creating-production-programs.md)および[組織内で作成されたサンドボックスプログラム](creating-sandbox-programs.md)を編集できます。 プログラムを編集すると、次の操作を実行できます。


* 「**セキュリティ**」タブの&#x200B;**WAF-DDOS Protection**&#x200B;を有効または無効にします。
* Adobe Experience Manager SitesをAssetsの既存のプログラムに追加し、Adobe Experience Manager Sitesの既存のプログラムにAssetsを追加します。
* SitesとAssetsの両方を持つ既存のプログラムから、SitesまたはAssetsを削除します。
* 使用されていないソリューションの使用権限を既存のプログラムに追加するか、新しいプログラムを作成する。
* 実稼動プログラムに削除用のマークを付けます。
* サンドボックスプログラムを削除する。

## 権限 {#permissions}

プログラムの編集、サンドボックスプログラムの削除、実稼動プログラムの削除用のマーク、ライセンスダッシュボードへのアクセスには、**ビジネスオーナー**&#x200B;の役割が必要です。

## プログラムの編集 {#editing}

ソリューションやアドオンの追加または削除など、編集されたプログラムの変更内容は次回のデプロイメント後に有効になります。

**プログラムを編集するには：**

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
1. 適切な組織を選択します。
1. **マイプログラム** ページで、編集するプログラムをクリックします。
1. ページの左上隅付近で、プログラムの名前をクリックし、「**プログラムを編集**」を選択します。

   ![&#x200B; プログラムのドロップダウンメニューの「プログラムを編集」オプション &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program.png)

1. **プログラムを編集** ダイアログボックスで、タブを使用して必要な様々なオプションを設定します。

   ![「一般」タブ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program-dialog-box.png)

   プログラムの編集に使用できるオプションは、プログラムの作成のオプションと同じです。

   * パブリッシュ層を新しい環境（Beta）用にプロビジョニングするかどうかを設定できます。 [柔軟なパブリッシュ層（Beta） &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)を参照してください。
   * 個々のオプションについて詳しくは、[実稼動プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)と[サンドボックスプログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)を参照してください。
   * Web Application Firewall （WAF）を有効または無効にするには、「**セキュリティ**」タブを選択し、「**WAF-DDOS Protection**」チェックボックスをオンまたはオフにします。 このチェックボックスをオンにすると、機能が有効になりますが、一部の自動Common Vulnerabilities and Exposures （CVE）保護に加えて、Cloud Managerを通じてWAF ルールをデプロイする必要があります。 WAF ルールがライセンスされていても、このチェックボックスがオンになっていない場合、この機能はアクティブになっていません。 詳しくは、[WAF ルールを含むトラフィックフィルタールール &#x200B;](/help/security/traffic-filter-rules-including-waf.md)を参照してください。

     >[!NOTE]
     >この機能がアクティブであることを確認するには、トラフィックがサイトに流れたら、[CDN ログ &#x200B;](//help/security/traffic-filter-rules-including-waf.md#cdn-logs)を調べます。 `waf`属性を含む`rules` プロパティを含むログエントリを探します。 例：
     >
     >`"rules": "*waf=*"`
     >
     >この属性は、WAF ルールがデプロイされる前であっても、WAFがアクティブになると表示されます。

     ![&#x200B; プログラムを編集ダイアログボックスに「セキュリティ」タブのオプションが表示されている](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/cmk-edit-programs.png)

   * 同じ&#x200B;**セキュリティ** タブで、既存のプログラムに対して&#x200B;**顧客管理キー**&#x200B;を有効にできます。

     アクティブ化後にCMKを無効にすることはできません。 CMKを有効にした後、Experience Hubで暗号化キーを設定します。 Experience Hub[&#128279;](#configure-cmk-experience-hub)でのCMKの設定については、を参照してください。

   * [組織の使用権限に応じて、実稼動プログラムに追加のオプション &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options)を使用できます。

1. 「**更新**」をクリックして変更を保存します。

## Experience HubでのCMKの設定 {#configure-cmk-experience-hub}

プログラムに対してCMKを有効にすると、Cloud ManagerはExperience HubのCMK設定ページへの直接リンクを提供するので、次のように設定できます
プログラムから離れることなく暗号化キーを使用できます。

CMKが環境に対して正常に設定されると、環境の詳細ページに&#x200B;**CMK設定** ステータスバッジが表示されます。 CMKがプログラムに対して有効になっているが、特定の環境に対してまだ設定されていない場合、その環境の詳細ページにバッジは表示されません。

**Experience HubでCMKを設定するには：**

1. **マイプログラム** ページで、CMKが有効になっているプログラムカードを探します。
2. ![省略記号 – 詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**CMK**&#x200B;の設定をクリックします。

   ![有効を示すCMK アイコンを示すプログラムカード、次に省略記号メニューの「CMKを設定」オプション &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/cmk-configure-edit-program-dlg.png)

   Experience Hubでは、Azure Key Vaultの詳細と暗号化キー情報を入力できるCMK設定ページが開きます。

   設定手順について詳しくは、[AEM as a Cloud Service用のお客様が管理するキーの設定](/help/security/customer-managed-keys.md)を参照してください。

## 実稼動プログラムを削除用にマーク {#delete-production-program}

実稼動プログラムの削除は2段階のプロセスです。 ビジネスオーナーは、削除のためのプログラムをマークし、検証とテイクダウン期間をトリガーします。 その後、削除された期間が経過すると、プログラムは完全に削除されます。

実稼動プログラムに削除用のマークが付けられると、次の処理が行われます。

* 生産プログラムに関連付けられているクレジットは、顧客に返されます。
* 実稼動プログラムに属するすべての環境が削除されます。

削除のマークを開始する前に、実稼動プログラムが削除の対象であるかどうかを検証します。 マーキングが失敗した場合、実稼動プログラムは代わりに`Failed to mark for deletion`状態に移動します。

>[!NOTE]
>
>サンドボックスプログラムは、このプロセスの影響を受けません。 サンドボックスプログラムを削除するには、[&#x200B; サンドボックスプログラムの削除](#delete-sandbox-program)を参照してください。

**削除する実稼動プログラムをマークするには：**

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
1. 適切な組織を選択します。
1. **マイプログラム** ページで、削除対象としてマークする実稼動プログラムの場合、![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**プログラムを削除**&#x200B;をクリックします。

   ![実稼動プログラムのドロップダウンリストから「プログラムを削除」を選択する&#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete1.png)*上記の実稼動プログラムの例は、イラスト用です。*

1. **削除のための実稼動プログラムのマーク** ダイアログボックスで、実稼動環境、ステージ環境、開発環境など、プログラムに接続されているリソースを一覧表示する警告を確認します。

   ![実稼動プログラムの削除ダイアログボックス &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2.png)


   >[!NOTE]
   >
   >実稼動プログラムに、現在更新中の環境などのブロックリソースがある場合、「**削除用にマーク**」ボタンは無効になります。 すべてのプログラムリソースがロック解除されるまで待ってから、プログラムに削除用のマークを付けることができます。
   >
   >![削除用の実稼動プログラムをマークするダイアログボックスに、ブロックリソースがあるためプログラムを削除できないことを示す](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2b.png)


1. 確認するには、ダイアログボックスに表示されているプログラム名を入力し、**削除のマーク**&#x200B;をクリックします。

   確認後、実稼動プログラムは、プロセスの実行中に&#x200B;**削除用のマーキング** ステータスを表示します。

   ![削除状態のマーク &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete3.png)

   完了すると、実稼動プログラムカードが更新され、**削除用にマーク**&#x200B;され、関連するアラートバッジが付きます。

   ![関連するアラートバッジで削除状態にマークされました](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete4.png)

1. 実稼動プログラムカードのアラートバッジをクリックして、スケジュールされた永久削除日を表示します。

   ![実稼動プログラムの予定永久削除日の表示](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete5.png)

   テイクダウン期間が経過すると、プログラムは完全に削除され、復元できません。

### 実稼動プログラムを削除からマーク解除する {#unmark-from-deletion}

完全な削除がまだ行われていない限り、*削除用に* マークされた実稼動プログラムを復元できます。

>[!IMPORTANT]
>
>削除用にマークされた実稼動プログラムを復元するには、お客様が利用可能なクレジットを持っている必要があります。

**削除から実稼動プログラムのマークを解除するには：**

1. **マイプログラム** ページで、**削除用にマーク済みであることを示す実稼動プログラムカードを探します**。

1. 実稼動プログラムカードで、![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**削除するマークを解除**&#x200B;をクリックします。

   ![実稼動プログラムの予定永久削除日のマークを解除する](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-unmarkfordelete6.png)

   実稼動プログラムは削除対象としてマークされていません。

## サンドボックスプログラムの削除 {#delete-sandbox-program}

サンドボックスプログラムを削除すると、それに関連付けられたすべての環境とパイプラインも削除されます。

>[!TIP]
>
>**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、サンドボックスプログラム全体ではなく、実稼動環境とステージ環境を削除することもできます。

**サンドボックスプログラムを削除するには：**

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
1. 適切な組織を選択します。

1. **[マイプログラム](#my-programs)** ページで、編集するサンドボックスプログラムをクリックして、その詳細を表示します。

1. ページの左上にあるサンドボックスプログラムの名前をクリックし、**プログラムを削除**&#x200B;を選択します。

   ![プログラムオプションを削除する](assets/delete-sandbox1.png)

または、Cloud Managerの概要ページからサンドボックスプログラムのカードの![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**プログラムの削除**&#x200B;を選択することもできます。

![プログラムカードからサンドボックスを削除](assets/delete-sandbox2.png)
