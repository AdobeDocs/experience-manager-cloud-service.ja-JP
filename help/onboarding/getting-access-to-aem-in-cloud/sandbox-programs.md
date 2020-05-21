---
title: サンドボックスプログラム — クラウドサービス
description: サンドボックスプログラム — クラウドサービス
translation-type: tm+mt
source-git-commit: eb874176c71d7f3d03d953f7bae4cb3db2ffb3b9
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Sandboxプログラム {#sandbox-programs}

## 概要 {#introduction}

Sandboxプログラムは、AEMクラウドサービスで使用できる2種類のプログラムの1つで、もう1つは通常のプログラムです。

サンドボックスは、通常、トレーニング、実行デモ、有効化、またはPOCの目的で作成されます。 彼らは生きたトラフィックを運ぶつもりはない。

SandboxプログラムにはSitesとAssetsが含まれ、サンプルコード、開発環境、非実稼働パイプラインを含むGitブランチが自動入力されて配信されます。

プログラムタイプの詳細については、「プログラムとプログラムタイプについて [](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)」を参照してください。

### サンドボックスプログラムの属性 {#attributes-sandbox}

Sandboxプログラムには次の属性があります。

1. **プログラムの作成：** サンドボックスプログラムの作成には、次の自動機能が含まれます。
   * サンプルコードとコンテンツを使用したプロジェクトのセットアップ
   * 開発環境の創出
   * 開発環境への非実稼働パイプラインの作成(開発環境へのマスターブランチのデプロイ)

1. **含まれるソリューション：** Sandboxプログラムには、サイトとアセットが含まれます。

1. **AEMのアップデート：** AEMのアップデートはSandboxプログラム内の環境に手動で適用でき、自動的にプッシュされることはありません。

1. **休止状態：** Sandboxプログラム内の環境は、特定の期間、アクティビティが検出されない場合、自動的に休止状態になります。 冬眠状態の環境は、手動で非冬眠状態にすることができます。

### Sandboxプログラムの作成 {#creating-sandbox-program}

プログラム作成ウィザードが表示され、詳細を送信するように求められます。

サンドボックスプログラムの作成方法について詳しくは、「サンドボックスプログラムの [作成](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)」を参照してください。

### Sandbox環境の作成 {#creating-sandbox-environments}

Sandboxプログラムは、プログラムの作成時に、自動作成された方法で開発環境を提供します。 開発環境には、デフォルトで作成者と発行層が付属しています。

実稼働段階の環境セットは、実稼動パイプラインをセットアップする準備ができたら、Sandboxプログラムに手動で追加できます。

環境を手動で作成する方法について詳しくは、環境の [追加を参照してください](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)。

### Sandbox環境の削除  {#deleting-sandbox-environments}

必要な権限を持つユーザーは、開発環境または実稼働/ステージ環境セットを削除できます。

環境の削除方法については、環境の [削除を参照してください](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment)。


## サンドボックス環境の冬眠と非冬眠 {#hibernating-introduction}

Sandboxプログラム環境は、無操作状態が続くと *休止モードに入ります* 。

>[!NOTE]
>休止状態は、サンドボックスプログラム環境に固有です。 通常のプログラム環境は冬眠しません。

### 休止状態 {#hibernation-introduction}

休止状態は、自動または手動で発生できます。 環境が冬眠状態になるまで数分かかる場合があります。 データは休止中に保持されます。

休止状態は次のように分類されます。

* **Sandboxの自動プログラム環境は** 、8時間操作が実行されなかった場合に自動的に休止状態になります。つまり、作成者も発行サービスも要求を受け取りません。

* **手動**: Sandboxプログラム環境を手動で休止することはできますが、休止状態が一定時間続くと自動的に休止状態が発生するので、これを行う必要はありません。

#### 手動ハイバーネーションの使用 {#using-manual-hibernation}


手動の休止状態は、デベロッパーコンソールの2つの画面のいずれかからでも実行できます。

次の手順に従って、プログラム環境を手動で休止状態にします。

1. 開発者コンソールに移動します。
1. 「休止状態」をクリックします
1. 「Hibernate」をクリックして確認します。
1. ハイバーネーションが正常に終了すると、次の画面が表示されます。
1. 下の図に示す環境リスト画面(環境の詳細画面から「環境」リンクをクリックするとアクセスできる)で、目的の環境の行に「Hibernate」ボタンをクリックできます。 確認画面が表示されます。

### 冬眠解除 {#de-hibernation-introduction}

>[!IMPORTANT]
>Developer Consoleへのアクセスは、管理コンソールの「Cloud Manager - Developer Role」で定義します。 この権限を持つユーザーは、環境を休止解除できます。

### 冬眠環境へのアクセス {#accessing-hibernated-environment}

冬眠した環境の作成者層または発行層に対してブラウザーリクエストを行うと、次の図に示すように、環境ーの冬眠状態を説明するランディングページが発生します。

「Cloud Manager - Developer Role」を持つユーザーは、Developer ConsoleボタンをクリックしてDeveloper Consoleにアクセスし、環境の休止を解除できます。 ロールの設定に関する情報は、Cloud Managerのドキュメントで確認できます。

組織のユーザーがDeveloper Consoleに表示するDeveloper Consoleボタンをクリックできない場合は、「Cloud Manager - Developer Role」を割り当てる必要があります。




## Sandbox環境へのAEMの更新 {#aem-updates-sandbox}


詳しくは、 [AEMバージョンの更新を参照してください](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates)。

ユーザーは、Sandboxプログラム内の環境にAEMの更新を手動で適用できます（下図を参照）。 これは、表示されるステータスが「UPDATE AVAILABLE」の場合に実行できます。 [更新]オプションは、[環境カード]のドロップダウンメニューから利用できます。 環境画面の[管理]メニューから選択することもできます。

>[!NOTE]
>手動更新パイプラインを開始するには、対象の開発環境に展開する非実稼動パイプラインを設定する必要があります。

>[!NOTE]
>手動更新パイプラインをProduction+Stage環境セットに開始するには、実稼動パイプラインを設定する必要があります。

>[!NOTE]
>「Production」または「Stage」環境に手動で更新すると、もう一方が自動的に更新されます。 Production+Stage環境セットは、同じAEMリリースに存在する必要があります。





