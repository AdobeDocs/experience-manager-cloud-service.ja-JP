---
title: Cloud Serviceリリース2020.6.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.6.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 89%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.6.0 {#release-notes}

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.6.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.6.0のリリース日は2020年6月4日です。

## 新機能 {#whats-new-cloud-manager}

* Cloud Manager での役割が&#x200B;*ビジネス所有者*&#x200B;のユーザーは、サンドボックスプログラムをランディングページから（プログラムカードのクイックアクションボタンを使用して）またはプログラム内から削除できるようになりました。

   詳細は、[サンドボックスプログラムの削除](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.translate.html)を参照してください。

* Cloud Manager の&#x200B;*ビジネス所有者*&#x200B;または&#x200B;*デプロイメントマネージャー*&#x200B;の役割にあるサンドボックスプログラムユーザーが、Cloud Manager UI を使用して、実稼動環境とステージ環境のセットを削除できるようになりました。削除オプションが、**プログラムの概要ページの環境カード**&#x200B;と、**環境**&#x200B;ページの両方から利用できるようになりました。実稼動環境またはステージ環境で削除オプションを選択すると、セット内の他のものも削除されます。

   詳細は、[サンドボックスプログラムの削除](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.translate.html)を参照してください。

* ランディングページにコーチマークを付け、基本的なナビゲーションについてユーザーに通知し、指示します。

* **プログラムの概要**&#x200B;ページにコーチマークを付けて、Cloud Manager 内部の基本的なナビゲーションに関する情報を提供し、ユーザーが開始できるように指示します。

* Cloud Manager で&#x200B;**学習**&#x200B;ページが利用できるようになり、トップナビゲーションからアクセスできます。このページには、Cloud Manager で割り当てられた役割に関連して、最も頻繁に使用されるワークフローについてユーザーが知るのに役立つリソースが含まれています。

* サンドボックスプログラムは、**サンドボックス**&#x200B;バッジによって識別されるようになります。このバッジは、ランディングページのプログラムカードと、**プログラムの概要**&#x200B;ページで、プログラム名の横に表示されます。

* 「システム管理者」の役割を持つユーザーは、Admin Console 内の場所に 1 回のクリックでアクセスできるようになりました。この場所から、ユーザーの役割や Cloud Manager への権限を管理できます。「**アクセスを管理**」ボタンが、ランディングページの「**プログラムを追加**」ボタンの横に表示されて使用できるようになりました。

   詳細は、[システム管理者のタスク](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks)を参照してください。

* 「システム管理者」の役割を持つユーザーは、Cloud Manager から直接オーサーインスタンスに対して 1 回のクリックでアクセスできるようになりました。

   詳細は、[オーサーインスタンスへのアクセス管理](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/onboarding/getting-access/navigation.translate.html#manage-access-aem)を参照してください。

* ビルドログに、スキップされたコンテンツパッケージを含む、検出されたアーティファクトのリストが含まれるようになりました。

* ビルド手順で、生成されるすべてのコンテンツパッケージに、名前、グループ、バージョンのすべての必須プロパティが含まれていることを検証できるようになりました。

* ビルド手順で、ビルドで少なくとも 1 つのコンテンツパッケージが生成されたかどうかを検証できるようになりました。

### バグ修正 {#bug-fixes-cm}

* 特定の状況で、**プログラムを作成**&#x200B;ダイアログボックスのアイコンの表示がずれていました。

* AEM リリース ID が、**プログラムの概要**&#x200B;ページに一貫して表示されなかった問題を修正しました。

* 実稼動パイプラインを設定する際に、一部の顧客に対して、**スケジュール済みデプロイメント**&#x200B;オプションが表示されない問題を修正しました。

### 既知の問題 {#known-issues-cm}

* サンドボックスプログラム内の環境が、一定期間アクティビティが検出されない場合、休止状態になる。このステータスは、Cloud Manager では確認されません。このステータスが確認されるのは、開発者コンソールを経由した場合です。この問題は、今後のリリースで修正される予定です。

* Cloud Manager から開発者コンソールへの直接リンクが、サンドボックスプログラムの環境を非休止／休止にするオプションを表示しない。これを解決するには、開発者コンソールで、url の末尾にパターン `#release-cm-p1234-e5678` を追加します。ここで、*1234* はプログラム ID、*5678* は環境 ID です。この問題は、今後のリリースで修正される予定です。
