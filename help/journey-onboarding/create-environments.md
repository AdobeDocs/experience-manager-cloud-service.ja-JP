---
title: 環境の作成
description: Cloud Manager を使用して最初の環境を作成する方法を説明します。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 26%

---

# 環境の作成 {#create-environments}

この部分では、 [オンボーディングジャーニー](overview.md) Cloud Manager を使用して最初の環境を作成する方法について説明します。

## 目的 {#objective}

このオンボーディングジャーニーの前のドキュメントを読んだ後、 [プログラムの作成，](create-program.md) これで、独自の Cloud Manager プログラムが作成されました。 次に、Cloud Manager を使用して、そのプログラム用の最初の環境を作成する方法を説明します。

このドキュメントを読むと、次のことが可能になります。

* 環境とは何かを理解します。
* 異なる環境の違いを把握します。
* 独自の環境を作成できる。

## 環境とは {#environments}

環境は、Cloud Manager の階層内のプログラムの下に配置されます。 プログラムを使用すると、ソリューションを整理し、特定のAdobeメンバーに対してそれらのプログラムへのアクセスを許可できますが、環境は特定のプログラムに属し、それらのプログラム内のチームソリューションの個々のインスタンスです。 環境は、コンテンツのオーサリングや新しい開発のテストなど、特定の目的で使用されます。 Cloud Manager の CI/CD パイプラインを使用すると、Git リポジトリーからこれらの環境にコードをデプロイできます。

旅行関連のメディアに重点を置いたテナントである、理論上の WKND Travel and Adventure Enterprises の例を思い出してみれば、次の 2 つのプログラムがある可能性があります。WKND マガジン部門の 1 つのサイトプログラムと WKND メディア部門の 1 つのアセットプログラムです。 各プログラムには、サイトの実際のトラフィックを処理する 1 つの実稼動環境や、新しいアプリケーションコードをテストする 1 つの開発環境など、いくつかの環境がある可能性があります。

環境には、次の 3 つのタイプがあります。

* **実稼動環境とステージング環境** - 実稼動環境とステージング環境はペアとして使用でき、それぞれ実稼動およびテストのために使用されます。
* **開発環境**：開発環境は、開発およびテストのために構築でき、実稼動以外のパイプラインにのみ関連付けることができます。

このオンボーディングジャーニーを目的として、開発環境を作成します。

## 環境の作成 {#creating-environments}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 環境を追加するプログラムをクリックします。

1. **プログラムの概要**&#x200B;ページで、**環境**&#x200B;カードの「**環境を追加**」をクリックして環境を追加します。

   ![環境カード](/help/implementing/cloud-manager/assets/no-environments.png)

   * 「**環境を追加**」オプションは「**環境**」タブでも使用できます。

      ![「環境」タブ](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 「**環境を追加**」オプションは、権限がない場合やライセンスされているリソースによっては、無効になっている場合があります。

1. 表示される&#x200B;**環境を追加**&#x200B;ダイアログで以下を行います。

   * 「**環境タイプ**」を選択します。
      * 使用可能/使用済み環境の数は、「開発環境」タイプの後ろの括弧内に表示されます。
   * 「**環境名**」を入力します。
   * 「**環境の説明**」を入力します。
   * 「**クラウドリージョン**」を選択します。

   ![環境を追加ダイアログ](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 「**保存**」をクリックして、指定された環境を追加します。

環境が利用可能になると、組織のメンバーが **開発者** 製品プロファイルは、 Cloud Manager にログインし、 Cloud Manager Git リポジトリーを管理できます。

## 次の手順 {#whats-next}

オンボーディングジャーニーのこの部分を読んだので、次の操作を実行する必要があります。

* 環境とは何かを理解します。
* 異なる環境の違いを把握します。
* 独自の環境を作成できる。

クラウドリソースが作成され、チームからアクセスする準備が整いました。 システム管理者は、チームメンバーがAdobe Admin Consoleのas a Cloud Serviceの製品プロファイルにアクセスできるように、最初にチームメンバーを割り当てる必要があります。

したがって、次にドキュメントを確認して、オンボーディングジャーニーを続行する必要があります [チームメンバーのAEMas a Cloud Service製品プロファイルへの割り当て](assign-profiles-aem.md)  このドキュメントでは、チームメンバーに新しい環境へのアクセスに必要な権限を付与する方法を学びます。

## その他のリソース {#additional-resources}

その他に、次のリソースも参照してください。

* [環境の管理](/help/implementing/cloud-manager/manage-environments.md)  — 作成できる環境のタイプと、Cloud Manager プロジェクト用に環境を作成する方法について説明します
* [AdobeCloud Manager の使用 — 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja) - Cloud Manager 環境は、AEMオーサリング、パブリッシュ、および Dispatcher の各サービスで構成されます。 様々な環境が役割をサポートし、様々な CI/CD パイプラインを使用して関与する方法について説明します。
