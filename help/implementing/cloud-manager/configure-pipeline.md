---
title: CI/CD パイプラインの設定 - Cloud Services
description: CI/CD パイプラインの設定 - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: f3743451f7aeadae26e8a6814cfbed9667c4a242
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 38%

---

# CI/CD パイプラインの設定 {#configure-ci-cd-pipeline}

Cloud Manager には、次の 2 種類のパイプラインがあります。

* **実稼動パイプライン**：

   実稼働パイプラインは、実稼働とステージング環境のセットを作成した場合にのみ追加できます。

   詳しくは、[実稼働パイプラインの設定](configure-pipeline.md#setting-up-the-pipeline)を参照してください。

* **実稼動以外のパイプライン**：

   実稼動以外のパイプラインは、Cloud Manager のユーザーインターフェイスの&#x200B;**概要**&#x200B;ページから追加できます。

   詳細は、[非実稼動パイプラインとコード品質専用パイプライン](configure-pipeline.md#non-production-pipelines)を参照してください。

   >[!NOTE]
   >パイプラインを設定するには、次の操作を行う必要があります。
   > * パイプラインを開始するトリガーの定義
   > * 実稼動デプロイメントを制御するパラメーターの定義
   > * パフォーマンステストパラメーターの設定


## 実稼働パイプラインの設定 {#setting-up-production-pipeline}

実稼働パイプラインの設定はデプロイメントマネージャーが担当します。

>[!NOTE]
>プログラムの作成が完了し、Git リポジトリーに少なくとも 1 つのブランチがあり、実稼働とステージングの環境セットが作成されるまで、実稼動パイプラインを設定できません。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を指定する必要があります。

>[!NOTE]
>
>初期設定後にパイプライン設定を変更できます。

### 新しい実稼動パイプラインの追加 {#adding-production-pipeline}

プログラムを設定し、 [!UICONTROL Cloud Manager] UI で、実稼動パイプラインを追加する準備が整いました。

次の手順に従って、実稼動パイプラインの動作と環境を設定します。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページを開きます。
をクリックします。 **+追加** を選択します。 **実稼動パイプラインの追加**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **実稼動パイプラインの追加** ダイアログボックスが表示されます。 パイプライン名を入力します。

   また、 **導入トリガー** および **重要な指標エラーの動作** から **デプロイメントオプション**. をクリックします。 **続行**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   パイプラインを開始するデプロイトリガーを定義できます。

   * **手動** - UI を使用して、パイプラインを手動で開始します。
   * **Git の変更時** - 設定された Git ブランチにコミットが追加されるたびに CI/CD パイプラインを開始します。このオプションを選択しても、常にパイプラインを手動で開始できます。

      パイプラインのセットアップまたは編集中に、デプロイメントマネージャーは、品質ゲートのいずれかで重要なエラーが検出された場合のパイプラインの動作を定義できます。

      これは、より自動化されたプロセスを求めるお客様に役に立ちます。使用できるオプションは以下のとおりです。
   重要な失敗指標の動作を定義して、パイプラインを開始できます。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **即時失敗**  — 重要なエラーが発生すると、常にパイプラインはキャンセルされます。 このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **すぐに続行**  — 重要なエラーが発生すると、常にパイプラインは自動的に続行されます。 このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。


1. 10. **実稼動パイプラインの追加** ダイアログボックスには、 **ソースコード**. **フルスタックコード** が選択されている場合、 選択できる **リポジトリ** そして **Git ブランチ**. 以下に説明するように、「実稼動デプロイメントオプション」を選択します。 をクリックします。 **続行**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   実稼動デプロイメントオプション:

   * **実稼動環境にデプロイする前に一時停止します**:このオプションを使用すると、実稼動前にデプロイメントを一時停止できます。
   * **スケジュール済み**:このオプションを使用すると、ユーザーはスケジュールされた実稼動デプロイメントを有効にできます。

1. 10. **実稼動パイプラインの追加** ダイアログボックスには、 **エクスペリエンス監査**. このオプションは、エクスペリエンス監査に常に含める必要がある URL パスの表を提供します。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >「 」をクリックする必要があります。 **ページを追加** をクリックして、独自のカスタムリンクを定義します。 ページのパスはで始める必要があります `/`.
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

1. をクリックします。 **保存**. 新しく作成した実稼動パイプラインが **パイプライン** カード。

   パイプラインは、次に示すように、3 つのアクションと共にホーム画面のカードに表示されます。

   * **追加** ：新しいパイプラインの追加を許可します。
   * **リポジトリー情報へアクセス** - Cloud Manager Git リポジトリーへのアクセスに必要な情報をユーザーが取得できるようにします.
   * **詳細情報** - CI／CD パイプラインのドキュメントリソースの概要に移動します。

### 実稼動パイプラインの編集 {#editing-prod-pipeline}

パイプライン設定は、 **プログラムの概要** ページを開きます。

設定したパイプラインを編集するには、次の手順に従います。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページを開きます。

1. をクリックします。 **...** から **パイプライン** カードを開き、 **編集**&#x200B;を参照してください。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. 10. **実稼動パイプラインの編集** ダイアログボックスが表示されます。

   1. 10. **設定** 「 」タブでは、 **パイプライン名**, **導入トリガー**&#x200B;および **重要な指標の失敗の動作**.

      >[!NOTE]
      >詳しくは、 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. 10. **ソース** 「 」タブに、チェックまたはチェック解除のオプションが表示されます。 **実稼動環境にデプロイする前に一時停止します** および **スケジュール済み** オプション **実稼動デプロイメントオプション**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. 10. **エクスペリエンス監査** 「 」オプションを使用すると、新しいページを更新または追加できます。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. をクリックします。 **更新** パイプラインの編集が完了したら、

### その他の実稼動パイプラインのアクション {#additional-prod-actions}

#### 実稼動パイプラインの実行 {#run-prod}

パイプラインカードから実稼動パイプラインを実行できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページを開きます。

1. をクリックします。 **...** から **パイプライン** カードを開き、 **実行**&#x200B;を参照してください。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### 実稼動パイプラインの削除 {#delete-prod}

パイプラインカードから実稼動パイプラインを削除できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページを開きます。

1. をクリックします。 **...** から **パイプライン** カードを開き、 **削除**&#x200B;を参照してください。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >デプロイメントマネージャーの役割を持つユーザーが、 **削除** オプションを選択します。


## 非実稼動パイプラインとコード品質専用パイプライン {#non-production-pipelines}

ステージングおよび実稼動環境にデプロイするメインパイプラインに加えて、顧客は、実稼動以外のパイプラインと呼ばれる追加のパイプラインを設定できます。非実稼動パイプラインには 2 つのタイプがあります。

1. コード品質：Git ブランチのコードでコード品質スキャンを実行します。 このパイプラインは、ビルドとコードの品質ステップを実行します。
1. 導入：このパイプラインは、ビルドおよびコード品質手順の実行に加えて、選択した非実稼動環境にAEMas a Cloud Service環境にコードをデプロイします。

### 新しい非実稼動パイプラインの追加 {#adding-non-production-pipeline}

ホーム画面には、このパイプラインが新しいカードに一覧表示されます。

1. 次の **パイプライン** カードを Cloud Manager のホーム画面から削除します。 をクリックします。 **+追加** を選択します。 **非実稼動パイプラインの追加**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **非実稼動パイプラインの追加**  ダイアログボックスが表示されます。 作成するパイプラインのタイプを次のいずれかから選択します。 **コード品質パイプライン** または **デプロイメントパイプライン**.

   >[!NOTE]
   >デプロイメントパイプラインの場合は、デプロイメント環境を選択する必要があります。

   また、 **導入トリガー** および **重要な指標エラーの動作** から **デプロイメントオプション**. をクリックします。 **続行**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **フルスタックコード** が選択されている場合、 選択できる **リポジトリ** そして **Git ブランチ**. をクリックします。 **保存**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. 新しく作成した非実稼動パイプラインが **パイプライン** カード。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   パイプラインは、次に示すように、3 つのアクションと共にホーム画面のカードに表示されます。

   * **追加** ：新しいパイプラインの追加を許可します。
   * **リポジトリー情報へアクセス** - Cloud Manager Git リポジトリーへのアクセスに必要な情報をユーザーが取得できるようにします.
   * **詳細情報** - CI／CD パイプラインのドキュメントリソースの概要に移動します。

### 実稼動以外のパイプラインの編集 {#editing-nonprod-pipeline}

パイプライン設定は、 **パイプラインカード** から **プログラムの概要** ページを開きます。

次の手順に従って、設定済みの非実稼動パイプラインを編集します。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページを開きます。

1. 実稼動以外のパイプラインを選択し、「 」をクリックします。 **...**. をクリックします。 **編集**&#x200B;を参照してください。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. 10. **実稼動パイプラインの編集** ダイアログボックスが表示されます。

   1. 10. **設定** 「 」タブでは、 **パイプライン名**, **導入トリガー**&#x200B;および **重要な指標エラーの動作**.

      >[!NOTE]
      >詳しくは、 [リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) Cloud Manager でリポジトリーを追加および管理する方法について説明します。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. 10. **ソースコード** 「 」タブに、 **リポジトリ** そして **Git ブランチ**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. をクリックします。 **更新** 実稼動以外のパイプラインの編集が完了したら、

### その他の非実稼動パイプラインアクション {#additional-nonprod-actions}

#### 実稼動以外のパイプラインの実行 {#run-nonprod}

パイプラインカードから実稼動パイプラインを実行できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページを開きます。

1. をクリックします。 **...** から **パイプライン** カードを開き、 **実行**&#x200B;を参照してください。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### 実稼動以外のパイプラインの削除 {#delete-nonprod}

パイプラインカードから実稼動パイプラインを削除できます。

1. に移動します。 **パイプライン** カード **プログラムの概要** ページを開きます。

1. をクリックします。 **...** から **パイプライン** カードを開き、 **削除**&#x200B;を参照してください。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## 次の手順 {#the-next-steps}

パイプラインを設定したら、コードをデプロイする必要があります。

詳しくは、[コードのデプロイ](deploy-code.md)を参照してください。
