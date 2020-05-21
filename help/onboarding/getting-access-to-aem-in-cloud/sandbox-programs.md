---
title: サンドボックスプログラム — クラウドサービス
description: サンドボックスプログラム — クラウドサービス
translation-type: tm+mt
source-git-commit: e7cad0cd67f04eac5627e72339ccb1c4f54cc8c8
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---


# Sandboxプログラム {#sandbox-programs}

## 概要 {#introduction}

Sandboxプログラムは、AEMクラウドサービスで使用できる2種類のプログラムの1つで、もう1つは通常のプログラムです。

通常、サンドボックスは、トレーニング、実行デモ、有効化、またはコンセプトの配達確認(POC)の目的を満たすために作成されます。 彼らは生きたトラフィックを運ぶつもりはない。

SandboxプログラムにはSitesとAssetsが含まれ、サンプルコード、開発環境、非実稼働パイプラインを含むGitブランチが自動入力されます。

プログラムタイプの詳細については、「プログラムとプログラムタイプについて [](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)」を参照してください。

### サンドボックスプログラムの属性 {#attributes-sandbox}

Sandboxプログラムには次の属性があります。

1. **プログラムの作成：** サンドボックスプログラムの作成には、次の自動機能が含まれます。
   * サンプルコードとコンテンツを使用したプロジェクトのセットアップ
   * 開発環境の創出
   * 開発環境への非実稼働パイプラインの作成(開発環境へのマスターブランチのデプロイ)

1. **ソリューション：** Sandboxのプログラムには、AEMサイトとアセットが含まれます。

1. **AEMのアップデート：** AEMのアップデートはSandboxプログラム内の環境に手動で適用でき、自動的にプッシュされることはありません。

1. **休止状態：** Sandboxプログラム内の環境は、特定の期間、アクティビティが検出されなかった場合、自動的に休止状態になります。 冬眠状態の環境は、手動で非冬眠状態にすることができます。

### Sandboxプログラムの作成 {#creating-sandbox-program}

プログラム作成ウィザードを使用すると、Sandboxプログラムを作成できます。

Sandboxプログラムの作成方法については、「Sandboxプログラムの [作成](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)」を参照してください。

### Sandbox環境の作成 {#creating-sandbox-environments}

Sandboxプログラムは、プログラムの作成時に開発環境を自動作成方式で配信します。 開発環境には、デフォルトで、作成者と発行層が含まれます。

実稼働段階の環境セットは、実稼動パイプラインをセットアップする準備ができたら、Sandboxプログラムに手動で追加できます。

環境を手動で作成する方法について詳しくは、「環境の [追加](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) 」を参照してください。

### Sandbox環境の削除  {#deleting-sandbox-environments}

必要な権限を持つユーザーは、開発環境、実稼働/ステージ環境またはセットを削除できます。

環境を削除する方法について詳しくは、環境の [削除](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) を参照してください。


## サンドボックス環境の冬眠と非冬眠 {#hibernating-introduction}

Sandboxプログラム環境は、特定の期間、アクティビティが検出されなかった場合、 *休止モードに入ります* 。

>[!NOTE]
>休止状態は、サンドボックスプログラム環境に固有です。 正規プログラム環境は休止状態になりません。

### 休止状態 {#hibernation-introduction}

休止状態は、自動または手動で発生できます。 サンドボックスプログラム環境が *休止モードに入るまで、数分かかる場合があります*。 データは休止中に保持されます。

休止状態は次のように分類されます。

* **Sandboxの自動プログラム環境は** 、8時間操作が実行されなかった場合に自動的に休止状態になります。つまり、作成者も発行サービスも要求を受け取りません。

* **手動**: ユーザはSandboxプログラム環境を手動で休止できますが、休止状態が一定時間（8時間）続くと自動的に休止状態になるので、必要ありません。

#### 手動ハイバーネーションの使用 {#using-manual-hibernation}

SandboxプログラムをDeveloper Consoleから手動で休止状態にするには、次の2つの方法があります。

* 環境の詳細画面
* 環境一覧画面

Sandboxプログラム環境を手動で休止状態にするには、次の手順に従います。

1. Navigate to the **Developer Console**.
[環境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) カードから **Developer Console** （開発者コンソール）にアクセスする方法については、Accessing Developer Console **** （開発者コンソールへのアクセス）を参照してください。
1. 次の図に示すように、「休止状態」をクリックします。
1. 「 **Hibernate** 」をクリックして手順を確認します
1. ハイバーネーションが正常に終了すると、次の画面が表示されます。

#### 冬眠環境へのアクセス {#accessing-hibernated-environment}

冬眠した環境の作成者層または発行層に対してブラウザーリクエストを行うと、次の図に示すように、環境ーの冬眠状態を説明するランディングページが発生します。

Cloud Managerの開発者ロールを持つユーザーは、 **** Developer Consoleボタンをクリックして開発者コンソールにアクセスし、環境の休止を解除できます。 ロールの設定に関する情報は、Cloud Managerのドキュメントで確認できます。

組織のユーザーがDeveloper Consoleに表示するDeveloper Consoleボタンをクリックできない場合は、「Cloud Manager - Developer Role」を割り当てる必要があります。


### 冬眠解除 {#de-hibernation-introduction}

1. Navigate to the **Developer Console**.
[環境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) カードから **Developer Console** （開発者コンソール）にアクセスする方法については、Accessing Developer Console **** （開発者コンソールへのアクセス）を参照してください。

   >[!IMPORTANT]
   >Developer Consoleへのアクセスは、 **管理コンソールの** Cloud Manager - Developer Role **（開発者ロール）で定義します**。 開発者ロールの権限を持つユーザーは、Sandboxプログラム環境の休止状態を解除できます。

1. Click on **De-hibernate**, as shown in the figure below:

   ![](assets/de-hibernation-img1.png)

1. 「 **休止状態を** 解除」をクリックして手順を確認します。

   ![](assets/de-hibernation-img2.png)

1. 休止プロセスが開始され、進行状況が更新されるという通知が届きます。

   ![](assets/de-hibernation-img3.png)

1. 処理が完了すると、Sandboxプログラム環境が再度アクティブになります。

   ![](assets/de-hibernation-img4.png)


## Sandbox環境に対するAEMの更新 {#aem-updates-sandbox}


詳しくは、 [AEMバージョンの更新](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) （英語）を参照してください。

ユーザーは、Sandboxプログラム内の環境にAEMの更新を手動で適用できます（下図を参照）。 これは、表示されるステータスが **UPDATE AVAILABLEの場合に実行できます**。

「更新」オプションは、 **環境** ・カードのドロップダウン・メニューから利用できます。 このオプションは、 **環境カードで「** 詳細 **」をクリックした場合に** 、「 **管理** 」ボタンからも使用できます。

>[!NOTE]
>手動更新パイプラインを開始するには、 *対象の開発環境に展開する* 非実稼動パイプラインを設定する必要があります。

>[!NOTE]
>手動更新パイプラインからProduction+Stage環境セットへの *Production Pipeline* （実稼動パイプライン）を開始するには、Production Pipeline（実稼動パイプライン）を設定する必要があります。

>[!NOTE]
>「 *Production* 」または「 *Stage* 」環境に手動で更新すると、もう一方が自動的に更新されます。 Production+Stage環境セットは、同じAEMリリースに存在する必要があります。





