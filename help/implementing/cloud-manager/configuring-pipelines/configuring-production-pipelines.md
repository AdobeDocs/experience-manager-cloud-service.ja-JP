---
title: 実稼動パイプラインの設定
description: 実稼動パイプラインの設定
index: true
source-git-commit: 8bdc246d1f47e1bdc9a217588f0be69a09982be5
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 45%

---


# 実稼動パイプラインの設定 {#configure-production-pipeline}

実稼動パイプラインの設定はデプロイメントマネージャーが担当します。

>[!NOTE]
>プログラムの作成が完了し、Git リポジトリーに少なくとも 1 つのブランチがあり、実稼働とステージングの環境セットが作成されるまで、実稼動パイプラインを設定できません。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を指定する必要があります。

>[!NOTE]
>初期設定後にパイプライン設定を変更できます。

## 新しい実稼動パイプラインの追加 {#adding-production-pipeline}

プログラムを設定し、次を使用して 1 つ以上の環境を設定したら、 [!UICONTROL Cloud Manager] UI で実稼動パイプラインを追加する準備が整いました。

実稼動パイプラインの動作と環境を設定するには、次の手順に従います。

1. 次に移動： **パイプライン** カード **プログラムの概要** ページ。
クリック **+追加** を選択し、 **実稼動パイプラインを追加**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **実稼動パイプラインを追加** ダイアログボックスが表示されます。 パイプライン名を入力します。

   また、 **デプロイメントトリガー** および **重要な指標の失敗の動作** から **デプロイメントオプション**. クリック **続行**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   パイプラインを開始するデプロイメントトリガーを定義できます。

   * **手動** - UI を使用して、パイプラインを手動で開始します。
   * **Git の変更時** - 設定された Git ブランチにコミットが追加されるたびに CI/CD パイプラインを開始します。このオプションを選択しても、常にパイプラインを手動で開始できます。

      パイプラインのセットアップまたは編集中に、デプロイメントマネージャーは、品質ゲートのいずれかで重要なエラーが検出された場合のパイプラインの動作を定義できます。

      これは、より自動化されたプロセスを求めるお客様に役に立ちます。使用できるオプションは以下のとおりです。
   重要な失敗指標の動作を定義して、パイプラインを開始できます。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **すぐに失敗**  — 重要なエラーが発生すると、常にパイプラインはキャンセルされます。 このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **すぐに続行**  — 重要なエラーが発生した場合は常に、パイプラインは自動的に続行されます。 このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。


1. この **実稼動パイプラインを追加** ダイアログボックスには、次のラベルが付いた 2 番目のタブが含まれます **ソースコード**. 次のいずれかを選択できます。 **[フロントエンドコード](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)** または **[フルスタックコード](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   選択した場合 **フロントエンドコード**&#x200B;を選択する場合は、 **リポジトリ**, **Git ブランチ** および **コードの場所**（下の図を参照）。
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack1.png)

   選択した場合 **フルスタックコード**&#x200B;を選択する場合は、 **リポジトリ**, **Git ブランチ** および **実稼動デプロイメントオプション** （詳細は以下の図を参照）。
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prodpipeline-fullstack2.png)

   **実稼動デプロイメントオプション:**

   * **実稼動環境にデプロイする前に一時停止します**:このオプションを使用すると、実稼動前にデプロイメントを一時停止できます。
   * **予定**:このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

   >[!IMPORTANT]
   >選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/full-stack-disabled.png)

   >[!NOTE]
   >フロントエンドパイプラインの設定を開始する前に、 [AEMクイックサイト作成ジャーニー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) 使いやすいAEM Quick Site Creation ツールを使用してエンドツーエンドのワークフローを実現する このドキュメントサイトは、AEMサイトのフロントエンド開発を合理化し、AEMのバックエンドに関する知識を持たずに、すばやくサイトをカスタマイズするのに役立ちます。

1. クリック **続行** 次のオプションを選択したら、 **ソースコード** タブをクリックします。

1. この **実稼動パイプラインを追加** ダイアログボックスには、次のラベルの付いた 3 番目のタブが含まれます。 **エクスペリエンス監査**. このオプションは、エクスペリエンス監査に常に含める必要がある URL パスの表を提供します。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >次をクリックする必要があります： **ページを追加** をクリックして独自のカスタムリンクを定義します。 ページのパスはで始める必要があります `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   「**新規ページを追加**」をクリックして、エクスペリエンス監査に含める URL パスを指定します。

   例えば、`https://wknd.site/us/en/about-us.html` をエクスペリエンス監査に含める場合は、このフィールドにパス `/us/en/about-us.html` を入力し、「**保存**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   表に表示される URL は次のとおりです。

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   最大 25 行まで含めることができます。このセクションにユーザーが送信したページがない場合、サイトのホームページはデフォルトでエクスペリエンス監査に含まれます。

   詳しくは、「[エクスペリエンス監査結果について](/help/implementing/cloud-manager/experience-audit-testing.md)」ｓを参照してください。

   >[!NOTE]
   > 設定されたページはサービスに送信され、パフォーマンス、アクセシビリティ、SEO（検索エンジン最適化）、ベストプラクティス、PWA（プログレッシブ Web アプリ）のテストに従って評価されます。

1. 「**保存**」をクリックします。新しく作成した実稼動パイプラインが、 **パイプライン** カード。

   パイプラインは、次に示すように、4 つのアクションと共にホーム画面のカードに表示されます。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-created.png)

   * **追加**  — 新しいパイプラインを追加できます。
   * **すべて表示** ：ユーザーがすべてのパイプラインを表示できます。
   * **リポジトリー情報へアクセス** - Cloud Manager Git リポジトリーへのアクセスに必要な情報をユーザーが取得できるようにします.
   * **詳細情報** - CI／CD パイプラインのドキュメントリソースの概要に移動します。


