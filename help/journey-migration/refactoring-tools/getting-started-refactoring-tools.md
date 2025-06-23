---
title: リファクタリングツール入門
description: AEM as a Cloud Service でリファクタリングツールの使用を開始する方法について学ぶ
exl-id: 84394bdd-2b92-4f5d-b08a-7dc2c681baa4
source-git-commit: c89acee0c5090f32136306b41a669d7241002a37
workflow-type: ht
source-wordcount: '542'
ht-degree: 100%

---

# リファクタリングツール入門 {#getting-started-refactoring-tools}

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

1. CAM プロジェクトをまだ作成していない場合は、[CAM でのプロジェクトの作成と管理](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project)を参照してください。
1. **コードリファクタリング**&#x200B;カードをクリックして、ソースコードをアップロードします。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. 初めて&#x200B;**ソースコードビュー**&#x200B;にアクセスすると、ソースコードをアップロードするよう促す空のステートが表示されます。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam2.png)

---

## ソースコードのアップロード {#uploading}

ユーザーが初めて&#x200B;**リファクタリングツール**&#x200B;にアクセスすると、**ソースコードビュー**&#x200B;に空のステートが表示されます。以下の手順に従ってプロジェクトをアップロードし、検査プロセスを開始します。

1. **プロジェクトアップロードページへアクセスする**\
   空のステートの「**プロジェクトアップロード**」ボタンをクリックして、アップロードプロセスを開始します。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **ソースコードをアップロードする**
   - アップロードダイアログで、ソースコードの ZIP ファイルを選択します。
   - 「**アップロード**」をクリックして開始します。
   - アップロードの進行状況がダイアログに表示されます。アップロードにかかる時間は、プロジェクトのサイズによって異なります。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **検査プロセス**
   - アップロード後、バックグラウンドで&#x200B;**検査プロセス**&#x200B;が自動的に開始されます。
   - **ソースコードビュー**&#x200B;に、アップロードされたプロジェクトとその検査ステータスが表示されます。

1. **検査ステータス** 検査プロセスは、手動による設定のオーバーヘッドを軽減することで、リファクタリングツールの実行を簡素化するように設計されています。

   検査では、次のいずれかのステータスが表示されます。
   - **Running** – 検査中です。
   - **Ready** – 検査が完了しました。リファクタリングツールを実行できるようになりました。
   - **Failed** – エラーが発生しました。プロジェクトをクリックして検査レポートを確認し、問題があれば解決します。

   ![画像](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>新しいプロジェクトをアップロードすると、既存のプロジェクトが削除されます。続行する前に、必要なデータが保存されていることを確認します。

>[!NOTE]
>リファクタリングジョブは、ソースコードのアップロードが成功した場合にのみ実行できます。

---

## リファクタリングジョブ {#refactoring-jobs}

「**リファクタリングジョブ**」タブをクリックすると、既存のジョブのリストが表示されます。ジョブがまだ作成されていない場合は、ジョブ作成を促す空のステートが表示されます。

![画像](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### &#x200B;1. 新しいリファクタリングジョブを作成する

- 「**新規ジョブの作成**」ボタンをクリックします。
- 目的のリファクタリングツールを選択します。
- 「**Start**」をクリックしてリファクタリングプロセスを開始します。

![画像](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>「**すべてのツールを同時に実行**」オプションを使用すると、個別のリファクタリングジョブを実行することも、利用可能なすべてのツールを一度に実行することもできます。

---

### &#x200B;2. ジョブステータス

- **Running** – ジョブは現在進行中です。ステータスは、ジョブの完了または失敗時に自動的に更新されます。
- **Completed** – ジョブは正常に完了しました。結果を確認したり、リファクタリングされたコードをダウンロードしたりできるようになりました。
- **Failed** – ジョブでエラーが発生しました。ジョブをクリックすると、詳細なログが表示され、問題のトラブルシューティングを行うことができます。

![画像](/help/journey-migration/refactoring-tools/assets/rscam8.png)

ジョブが正常に完了すると、「**ダウンロード**」ボタンが使用可能になり、次の情報を取得できます。

- **リファクタリングされたプロジェクト**：これは、変換が適用された後に更新されたコードです。お客様は、プロジェクトの最新のコードをダウンロードできます。
- **アクティビティログ**：ジョブの実行中に、ツールによって実行されたすべての手順と加えられた変更は、ログとして記録されます。
- **結果レポート**：このレポートには、ツールによって完全には実行されなかったものの、対応が必要な項目が含まれています。これらの変更はすべてここに記録されます。

![画像](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>各ジョブの完了には最大 1 時間かかる場合があります。ステータスが更新されない場合は、アドビサポートにお問い合わせください。
