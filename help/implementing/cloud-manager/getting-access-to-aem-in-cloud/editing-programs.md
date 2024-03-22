---
title: プログラムの管理と編集
description: 実稼動およびサンドボックスプログラムを編集し、作成後にオプションを調整する方法について説明します。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 2dfae31e32d375c82c4f690624e48f7f09feb4df
workflow-type: ht
source-wordcount: '773'
ht-degree: 100%

---


# プログラムの管理と編集 {#editing-programs}

**マイプログラム**&#x200B;ページには、アクセス権を持つすべてのプログラムの概要が表示されます。個々のプログラムを選択すると、**プログラムの概要**&#x200B;ページで、プログラムの詳細が一目でわかります。

必要な権限を持つユーザーは、**プログラムの概要**&#x200B;から、組織内で作成された[実稼動プログラム](creating-production-programs.md)および組織内で作成された[サンドボックスプログラムを編集できます。](creating-sandbox-programs.md)プログラムの編集で、次のことが可能です。

* Assets を使用している既存のプログラムに Sites ソリューションを追加する（その逆も同様）。
* Sites と Assets の両方を使用している既存のプログラムから Sites または Assets を削除する。
* 使用されていない 2 つ目のソリューション使用権を既存のプログラムに追加するか、新規のプログラムとして追加する。
* サンドボックスプログラムを削除する。

## 権限 {#permissions}

プログラムの編集やサンドボックスプログラムの削除、およびライセンスダッシュボードへのアクセスを行うには、**ビジネスオーナー**&#x200B;ロールのメンバーである必要があります。

## マイプログラム {#my-programs}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **マイプログラム**&#x200B;ページには、アクセスできるすべてのプログラムのリストがタイルとして表示されます。

![マイプログラムページ](/help/implementing/cloud-manager/assets/my-programs.png)

### アクションの呼び出し {#cta}

ページの上部には、組織のステータスに関連するアクションの呼び出しが表示されます。例えば、プログラムを正常に設定した場合、過去 90 日間のアクティビティの統計には、次の内容が表示されることがあります。

* [デプロイ](/help/implementing/cloud-manager/deploy-code.md)数
* 特定された[コード品質の問題](/help/implementing/cloud-manager/code-quality-testing.md)の数
* ビルド数

組織の設定を開始したばかりの場合は、次の手順やドキュメントのリソースに関するヒントが表示される場合があります。

### 「プログラム」タブ {#programs-tab}

「**プログラム**」タブには、アクセス権のある各プログラムを表すカードが一覧表示されます。カードをタップまたはクリックすると、**プログラムの概要**&#x200B;ページにアクセスしてプログラムの詳細を確認できます。

並べ替えオプションを使用すると、必要なプログラムを見つけやすくなります。

![並べ替えオプション](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 並べ替え
   * 作成日（デフォルト）
   * プログラム名
   * ステータス
* 昇順（デフォルト）／降順
* グリッド表示（デフォルト）
* リスト表示

### 「ライセンス」タブ {#license-tab}

「**ライセンス**」タブから[ライセンスダッシュボード](/help/implementing/cloud-manager/license-dashboard.md)にすばやくアクセスできます。

## プログラムの概要 {#program-overview}

**[マイプログラム](#my-programs)**&#x200B;ページからプログラムを選択すると、Cloud Manager は選択したプログラムの&#x200B;**プログラム概要**&#x200B;ページを開きます。

![プログラムの概要ページ](/help/implementing/cloud-manager/assets/program-overview.png)

ページの左上隅にあるプログラム名をタップまたはクリックすると、別のプログラムにすばやく切り替えたり、**[マイプログラム](#my-programs)**&#x200B;ページに戻ったりします。また、[選択したプログラムを編集](#editing)したり、[プログラムを追加](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)したりすることもできます。

![プログラムスイッチャー](/help/implementing/cloud-manager/assets/program-switcher.png)

上部のアクションの呼び出しでは、プログラムのステータスに応じて役立つ情報を提供します。新しいプログラムの場合は、次の手順が提供されるほか、[プログラム作成時に設定された公開日のリマインダーが表示される場合があります。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![新規プログラムのアクションの呼び出し](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

ライブプログラムの場合、最後のデプロイメントのステータスと、詳細および新しいデプロイメントを開始するためのリンクが表示されます。

![コールトゥアクション](/help/implementing/cloud-manager/assets/info-banner.png)

**環境**&#x200B;と&#x200B;**パイプライン**&#x200B;カードを使用すると、選択したプログラム内の両方の概要を容易に確認できます。

![カード](/help/implementing/cloud-manager/assets/environments-pipelines.png)

**パフォーマンス**&#x200B;カードを使用すると、**[CDN ダッシュボード](/help/implementing/cloud-manager/cdn-performance.md)**&#x200B;の概要を確認できます。

![パフォーマンスカード](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

## プログラムの編集 {#editing}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](#my-programs)**&#x200B;ページで、編集するプログラムをクリックして詳細を表示します。

1. ページの左上にあるプログラムの名前をクリックし、「**プログラムを編集**」を選択します。

   ![プログラムオプションの編集](assets/edit-program-overview.png)

1. **プログラムを編集**&#x200B;ページで「**一般**」タブを開きます。

   ![「一般」タブ](assets/edit-program-prod1.png)

1. プログラムの編集に使用できるオプションは、プログラムの作成時のオプションと同じです。
   * 個々のオプションについて詳しくは、[実稼働プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)と[サンドボックスプログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)のドキュメントを参照してください。
   * [その他のオプション](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options)は組織の使用権限に応じて、実稼動プログラムで使用できる場合があります。

1. 「**更新**」をクリックして、プログラムに対する変更を保存します。

プログラムに対する変更が保存されます。

>[!NOTE]
>
>ソリューションやアドオンの追加または削除など、編集されたプログラムの変更内容は次回のデプロイメント後に有効になります。

## サンドボックスプログラムの削除 {#delete-sandbox-program}

サンドボックスプログラムを削除すると、それに関連付けられたすべての環境とパイプラインも削除されます。

>[!TIP]
>
>**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーは、サンドボックスプログラム全体ではなく、実稼動環境とステージ環境を削除することもできます。

サンドボックスプログラムを削除するには、次の操作を行います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](#my-programs)**&#x200B;ページで、編集するプログラムをクリックして詳細を表示します。

1. ページの左上にあるプログラムの名前をクリックし、「**プログラムを削除**」を選択します。

   ![プログラムオプションを削除する](assets/delete-sandbox1.png)

または、Cloud Manager の概要ページでプログラムのカードの省略記号ボタンをクリックし、「**プログラムを削除する**」を選択することもできます。

![プログラムカードからサンドボックスを削除](assets/delete-sandbox2.png)

>[!NOTE]
>
>サンドボックスプログラムのみを削除できます。実稼動プログラムは削除できません。
