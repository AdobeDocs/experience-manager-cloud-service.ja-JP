---
title: リファクタリングツールの概要
description: AEM as a Cloud Serviceのリファクタリングツールの使用を開始する方法について説明します
source-git-commit: 20bb756c4a2eb37341da4582f19cf41e4d60304a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---

# リファクタリングツールの概要 {#getting-started-refactoring-tools}

## 入手方法 {#availability}

<!-- Alexandru: duplicate contextualhelp id, drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_rs_upload"
>title="Download"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html" text="Release Notes"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution Portal"

-->

## リファクタリングツールの実行 {#running-refactoring-tools}

リファクタリングツールを使用して、AEM as a Cloud Serviceとの互換性を保つためにコードを移行します。

1. CAM プロジェクトをまだ作成していない場合は、[CAM でのプロジェクトの作成と管理 ](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project) を参照してください。
1. **コードリファクタリング** カードをクリックして、ソースコードをアップロードします。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. 初めて **Sourceのコードビュー** にアクセスすると、ソースコードをアップロードするよう促す空のステートが表示されます。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam2.png)

&#x200B;---

## Source コードのアップロード {#uploading}

ユーザーが初めて **リファクタリングツール** にアクセスすると、**Source コードビュー** に空のステートが表示されます。 以下の手順に従ってプロジェクトをアップロードし、検査プロセスを開始します。

1. **プロジェクトのアップロードページへのアクセス**\
   空の状態の **プロジェクトのアップロード** ボタンをクリックして、アップロードプロセスを開始します。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **Source コードのアップロード**
   - アップロード ダイアログで、ソースコードの ZIP ファイルを選択します。
   - 「**アップロード**」をクリックして開始します。
   - アップロードの進行状況がダイアログに表示されます。 期間は、プロジェクトのサイズによって異なります。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **検査の経過**
   - アップロード後、バックグラウンドで **検査プロセス** が自動的に開始されます。
   - **Source コードビュー** に、アップロードされたプロジェクトとそのインスペクションステータスが表示されます。

1. **検査ステータス** 検査プロセスは、手動設定のオーバーヘッドを削減することで、リファクタリングツールの実行を簡素化するように設計されています。

   検査では、次のいずれかのステータスが表示されます。
   - **実行中** – 検査中です。
   - **準備完了** – 検査が完了しました。リファクタリングツールを実行できるようになりました。
   - **失敗** - エラーが発生しました。 プロジェクトをクリックして検査レポートを確認し、問題があれば解決します。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>新しいプロジェクトをアップロードすると、既存のプロジェクトが削除されます。 続行する前に、必要なデータが保存されていることを確認します。

>[!NOTE]
>リファクタリングジョブは、ソースコードのアップロードが成功した場合にのみ実行できます。

&#x200B;---

## リファクタリングジョブ {#refactoring-jobs}

「**リファクタリングジョブ**」タブをクリックすると、既存のジョブのリストが表示されます。 ジョブがまだ作成されていない場合は、ジョブ作成を促す空の状態が表示されます。

![画像](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### 1.新しいリファクタリングジョブの作成

- 「**新規ジョブを作成** ボタンをクリックします。
- 目的のリファクタリングツールを選択します。
- 「**開始**」をクリックして、リファクタリングプロセスを開始します。

![画像](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>個々のリファクタリングジョブをトリガーするか、「すべてのツールを統合 **オプションを使用して使用可能なすべてのツールを一度に実行** きます。

&#x200B;---

### 2.ジョブのステータス

- **実行中** - ジョブは現在処理中です。 ステータスは、完了または失敗すると自動的に更新されます。
- **完了** - ジョブは正常に完了しました。 結果を確認したり、リファクタリングされたコードをダウンロードしたりできるようになりました。
- **失敗** - ジョブでエラーが発生しました。 ジョブをクリックすると、詳細なログが表示され、問題のトラブルシューティングを行うことができます。

![画像](/help/journey-migration/refactoring-tools/assets/rscam8.png)

ジョブが正常に完了すると、「**ダウンロード**」ボタンが使用可能になり、次の情報を取得できます。

- **リファクタリングされたプロジェクト**：これは、変換が適用された後に更新されたコードです。 顧客は、プロジェクトの最新のコードをダウンロードできます。
- **アクティビティログ**：ジョブの実行中、ツールで実行されたすべての手順と加えられた変更が、この中に記録されます。
- **結果レポート**：このレポートには、ツールによって完全には実行されなかったものの、対処が必要な項目が含まれています。 これらの変更はすべてここに記録されます。

![画像](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>各ジョブの完了には最大 1 時間かかる場合があります。 ステータスが更新されない場合は、Adobe サポートにお問い合わせください。

