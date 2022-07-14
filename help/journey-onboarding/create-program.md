---
title: プログラムの作成
description: Cloud Manager を使用して最初のプログラムを作成する方法を説明します。
role: Admin, User, Developer
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 25%

---


# プログラムの作成 {#create-program}

この部分では、 [オンボーディングジャーニー](overview.md) Cloud Manager を使用して最初のプログラムを作成する方法を学習します。

## 目的 {#objective}

このオンボーディングジャーニーの前のドキュメントを確認した後、 [Cloud Manager にアクセスする](cloud-manager.md) Cloud Manager への適切なアクセス権が確保されている。 これで、最初のプログラムを作成できます。

このドキュメントを読むと、次の操作を実行できます。

* プログラムとは何かを理解する。
* 実稼動プログラムとサンドボックスプログラムの違いを理解する。
* 独自のプログラムを作成できるようにする。

## プログラムとは {#programs}

プログラムは、Cloud Manager の組織の最上位レベルです。 Adobeのライセンスに応じて、プログラムを使用すると、ソリューションを整理し、特定のチームメンバーに対してそれらのプログラムへのアクセス権を付与できます。

Cloud Manager プログラムは、Cloud Manager 環境のセットを表します。 これらのプログラムは、通常、ライセンスを受けた SLA(Service Level Agreement) に対応する、ビジネスイニシアチブの論理的なセットをサポートします。 例えば、あるプログラムは組織のグローバルパブリック Web サイトをサポートするAEMリソースを表し、別のプログラムは内部の中央 DAM を表す場合があります。

旅行関連のメディアに重点を置いたテナントである、理論上の WKND Travel and Adventure Enterprises の例を思い出してみれば、次の 2 つのプログラムがある可能性があります。WKND マガジン部門の 1 つのサイトプログラムと WKND メディア部門の 1 つのアセットプログラムです。 その後、異なるチームメンバーは、それぞれの分割の労働要件のため、異なるプログラムにアクセスできます。

2 種類のプログラムがあります。

* **実稼動プログラム**&#x200B;は、サイトのライブトラフィックを有効にするために作成されます。これは、「実際の」環境です。
* **サンドボックスプログラム**&#x200B;は、通常、トレーニング、デモの実行、イネーブルメント、POC またはドキュメントの目的にかなうように作成されます。

用途が異なるので、環境が異なれば、選択肢も異なります。 ただし、作成のプロセスは似ています。 このオンボーディングジャーニーに対して、サンドボックス環境を作成します。

## サンドボックスプログラムの作成 {#create-sandbox}

サンドボックスプログラムを作成するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. Cloud Manager のランディングページで、画面の右上隅にある「**プログラムを追加**」をクリックします。

   ![Cloud Manager ランディングページ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. プログラム作成ウィザードで、「**サンドボックスを設定する**」を選択し、プログラム名を入力して、「**作成**」をクリックします。

   ![指定タイプのプログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

ランディングページに新しいサンドボックスプログラムカードが表示され、セットアッププロセスの進行に応じてステータスインジケーターも表示されます。

![概要ページからのサンドボックスの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

プログラムが完了すると、組織のメンバーが **開発者** 製品プロファイルは、 Cloud Manager にログインして Cloud Manager の Git リポジトリーを管理できます。

## 次の手順 {#whats-next}

最初のプログラムが作成されたので、そのプログラムの環境を作成できます。 次にドキュメントを確認して、オンボーディングジャーニーを続行する必要があります [環境を作成する。](create-environments.md)

## その他のリソース {#additional-resources}

その他に、次のリソースも参照してください。

* [プログラムとプログラムの種類](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) - Cloud Manager の階層、および様々なタイプのプログラムが構造に適合する方法、およびプログラムの違いについて説明します。
* [サンドボックスプログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) - Cloud Manager を使用して、トレーニング、デモ、POC、またはその他の非実稼動用に独自のサンドボックスプログラムを作成する方法を説明します。
* [実稼働プログラムの作成](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) - Cloud Manager を使用して、ライブトラフィックをホストする独自の実稼動プログラムを作成する方法を説明します。
* [AdobeCloud Manager の使用 — プログラム](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=ja) - Cloud Manager プログラムは、通常、購入したサービス契約 (SLA) に対応するビジネスイニシアチブの論理セットをサポートする、AEM環境のセットを表します。
