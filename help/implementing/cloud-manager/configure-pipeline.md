---
title: CI/CD パイプラインの設定 - Cloud Services
description: CI/CD パイプラインの設定 - Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: 3c9c14745e784c47eecd04ac622cc48f65d7442a
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 45%

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

[!UICONTROL Cloud Manager] UI を使用してプログラムを設定し、少なくとも 1 つの環境を設定したら、実稼動パイプラインを追加する準備が整います。

次の手順に従って、実稼動パイプラインの動作と環境を設定します。

1. **プログラムの概要** ページから **パイプライン** カードに移動します。
**+Add** をクリックし、「**実稼動パイプラインを追加**」を選択します。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add1.png)

1. **実稼動パイプラインを** 追加ダイアログボックスが表示されます。パイプライン名を入力します。

   さらに、**デプロイメントトリガー** から、**デプロイメントオプション** と **重要な失敗動作** を設定することもできます。 「**続行**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   パイプラインを開始するデプロイトリガーを定義できます。

   * **手動** - UI を使用して、パイプラインを手動で開始します。
   * **Git の変更時** - 設定された Git ブランチにコミットが追加されるたびに CI/CD パイプラインを開始します。このオプションを選択しても、常にパイプラインを手動で開始できます。

      パイプラインのセットアップまたは編集中に、デプロイメントマネージャーは、品質ゲートのいずれかで重要なエラーが検出された場合のパイプラインの動作を定義できます。

      これは、より自動化されたプロセスを求めるお客様に役に立ちます。使用できるオプションは以下のとおりです。
   重要な失敗指標の動作を定義して、パイプラインを開始できます。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **即座に失敗**  — 重要なエラーが発生すると、常にパイプラインはキャンセルされます。このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **直ちに続行** - 重要なエラーが検出されても、常にパイプラインは自動的に続行されます。このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。


1. **実稼動パイプラインを追加** ダイアログボックスには、**ソースコード** というラベルの付いた 2 番目のタブが含まれています。 **完全なスタックコ** ードが選択されます。**リポジトリ** と **Git ブランチ** を選択できます。 「**保存**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

1. **実稼動パイプラインを追加** ダイアログボックスには、**エクスペリエンス監査** というラベルの付いた 3 番目のタブが含まれています。 このオプションは、エクスペリエンス監査に常に含める必要がある URL パスの表を提供します。

   >[!NOTE]
   >「**ページを追加**」をクリックして、独自のカスタムリンクを定義する必要があります。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add4.png)

   「**新規ページを追加**」をクリックして、エクスペリエンス監査に含める URL パスを指定します。

   例えば、`https://wknd.site/us/en/about-us.html` をエクスペリエンス監査に含める場合は、このフィールドにパス `us/en/about-us.html` を入力し、「**保存**」をクリックします。

   ![](assets/exp-audit4.png)

   表に表示される URL は次のとおりです。

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   最大 25 行まで含めることができます。このセクションにユーザーが送信したページがない場合、サイトのホームページはデフォルトでエクスペリエンス監査に含まれます。

   詳しくは、「[エクスペリエンス監査結果について](/help/implementing/cloud-manager/experience-audit-testing.md)」ｓを参照してください。

   >[!NOTE]
   > 設定されたページはサービスに送信され、パフォーマンス、アクセシビリティ、SEO（検索エンジン最適化）、ベストプラクティス、PWA（プログレッシブ Web アプリ）のテストに従って評価されます。

1. 「**保存**」をクリックします。 新しく作成した実稼動パイプラインが **パイプライン** カードに表示されます。

   パイプラインは、次に示すように、3 つのアクションと共にホーム画面のカードに表示されます。

   * **** を追加 — 新しいパイプラインを追加できます。
   * **リポジトリー情報へアクセス** - Cloud Manager Git リポジトリーへのアクセスに必要な情報をユーザーが取得できるようにします.
   * **詳細情報** - CI／CD パイプラインのドキュメントリソースの概要に移動します。

### 実稼動パイプラインの編集 {#editing-prod-pipeline}

パイプライン設定は、**プログラムの概要** ページで編集できます。

設定したパイプラインを編集するには、次の手順に従います。

1. **プログラムの概要** ページから **パイプライン** カードに移動します。

1. **をクリックします…** パイプライン **カードから** を開き、**編集** をクリックします（下図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. **実稼動パイプラインを編集** ダイアログボックスが表示されます。

   1. 「**設定**」タブを使用すると、**パイプライン名**、**デプロイメントトリガー**、**重要な指標の失敗動作** を更新できます。

      >[!NOTE]
      >Cloud Manager でリポジトリを追加および管理する方法については、[ リポジトリの追加と管理 ](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) を参照してください。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. 「**ソース**」タブには、「**実稼動環境** にデプロイする前に一時停止」および「**実稼動環境のデプロイメントオプション**」の「**スケジュール済み**」オプションをオンまたはオフにするオプションがあります。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. 「**エクスペリエンス監査**」オプションを使用すると、新しいページを更新または追加できます。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. パイプラインの編集が完了したら、「**更新**」をクリックします。

### その他の実稼動パイプラインのアクション {#additional-prod-actions}

#### 実稼動パイプラインの実行 {#run-prod}

パイプラインカードから実稼動パイプラインを実行できます。

1. **プログラムの概要** ページから **パイプライン** カードに移動します。

1. **をクリックします…** パイプライン **カードから** を開き、**「** を実行」をクリックします（下図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### 実稼動パイプラインの削除 {#delete-prod}

パイプラインカードから実稼動パイプラインを削除できます。

1. **プログラムの概要** ページから **パイプライン** カードに移動します。

1. **をクリックします…** パイプライン **カードから** を開き、**削除** をクリックします（下図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >デプロイメントマネージャーの役割を持つユーザーは、パイプラインカードの **削除** オプションを使用して、セルフサービス方式で実稼動パイプラインを削除できるようになりました。


## 非実稼動パイプラインとコード品質専用パイプライン {#non-production-pipelines}

ステージングおよび実稼動環境にデプロイするメインパイプラインに加えて、顧客は、**実稼動以外のパイプライン**&#x200B;と呼ばれる追加のパイプラインを設定できます。このパイプラインでは、常にビルドステップとコード品質ステップを実行します。オプションで、AEM as a Cloud Service環境にデプロイすることもできます。

### 新しい非実稼動パイプラインの追加 {#adding-non-production-pipeline}

ホーム画面には、このパイプラインが新しいカードに一覧表示されます。

1. Cloud Manager のホーム画面から **パイプライン** カードにアクセスします。 「**+追加**」をクリックし、「**非実稼動パイプラインを追加**」を選択します。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **非実稼動パイプラインを追加ダ**  イアログボックスが表示されます。作成するパイプラインのタイプを、**コード品質パイプライン** または **デプロイメントパイプライン** のいずれかから選択します。

   さらに、**デプロイメントトリガー** から、**デプロイメントオプション** と **重要な指標の失敗の動作** を設定することもできます。 「**続行**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **完全なスタックコ** ードが選択されます。**リポジトリ** と **Git ブランチ** を選択できます。 「**保存**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. 新しく作成した非実稼動パイプラインが **パイプライン** カードに表示されるようになりました。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   パイプラインは、次に示すように、3 つのアクションと共にホーム画面のカードに表示されます。

   * **** を追加 — 新しいパイプラインを追加できます。
   * **リポジトリー情報へアクセス** - Cloud Manager Git リポジトリーへのアクセスに必要な情報をユーザーが取得できるようにします.
   * **詳細情報** - CI／CD パイプラインのドキュメントリソースの概要に移動します。

### 実稼動以外のパイプラインの編集 {#editing-nonprod-pipeline}

**プログラムの概要** ページから、**パイプラインカード** からパイプライン設定を編集できます。

次の手順に従って、設定済みの非実稼動パイプラインを編集します。

1. **プログラムの概要** ページから **パイプライン** カードに移動します。

1. 非実稼動パイプラインを選択し、「**...」をクリックします。**. 下の図に示すように、「**編集**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. **実稼動パイプラインを編集** ダイアログボックスが表示されます。

   1. 「**設定**」タブでは、**パイプライン名**、**デプロイメントトリガー**、**重要な指標の失敗の動作** を更新できます。

      >[!NOTE]
      >Cloud Manager でリポジトリを追加および管理する方法については、[ リポジトリの追加と管理 ](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) を参照してください。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. 「**ソースコード**」タブでは、**リポジトリ** と **Git ブランチ** を更新できます。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. 非実稼動パイプラインの編集が完了したら、「**更新**」をクリックします。


## 次の手順 {#the-next-steps}

パイプラインを設定したら、コードをデプロイする必要があります。

詳しくは、[コードのデプロイ](deploy-code.md)を参照してください。
