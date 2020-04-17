---
title: Adobe Experience Manager 6.x から AEM Cloud Service への移行
description: Adobe Experience Manager 6.x から AEM Cloud Service への移行
contentOwner: AG
translation-type: ht
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Adobe Experience Manager Assets as a Cloud Service への移行 {#move-to-assets-cloud-service}

<!-- About the need to move from previous AEM deployment to a cloud service deployment. And how does Adobe help do it OOTB?
-->

## 移行ツールについて {#migration-tool}

<!-- 
Link back to information about the tool in the Experience Manager as a Cloud Service docs if the tool works the same for Sites and Assets. Document the Assets-specific information here.

* What is the migration tool called? Is there a branding term for it?
* How much do we want to elaborate about the Pattern Detector rules? Is there a branding term for it?
* Before migrating using the tool, is any prepping required?
* See CQ-4271901

-->

移行ツールを使用すると、次のことを実現できます。

* 既存のワークフローモデルを、アセットコンピューティングサービスで動作する処理プロファイルに変換する。
* サポートされていないステップをワークフローモデルから削除する。
* ワークフローランチャーを無効にする。
* ユーザーの確認／検証後に、既存のソースコード内の設定を結合する。

移行ツールは、Maven モジュールで処理プロファイルを作成し、次の 2 とおりの方法でユーザーが使用できるようにします。

* 既存のプロジェクトの 1 つにマージする。
* モジュールを新しいサブモジュールとして追加する。

移行ツールは、おこなった変更とそれらの変更に関する情報をレポートとして提供します。

<!--  

What is the output of the tool, besides migrated content.

Give details about reports and logs of the tool. 

* How to access the report, including required permissions.
* How to read/interpret the report.
* Location of logs. How to read the logs.
* What common errors to look for. Troubleshooting for these errors.

-->

## 新しいデプロイメントへのコンテンツの移行 {#content-migration-across-deployments}
