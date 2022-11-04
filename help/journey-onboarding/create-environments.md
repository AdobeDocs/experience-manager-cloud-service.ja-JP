---
title: 環境の作成
description: Cloud Manager を使用して最初の環境を作成する方法を説明します。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 100%

---

# 環境の作成 {#create-environments}

[オンボーディングジャーニー](overview.md)のこのパートでは、Cloud Manager を使用して最初の環境を作成する方法を説明します。

## 目的 {#objective}

オンボーディングジャーニーの前のドキュメント「[プログラムの作成](create-program.md)」を読み、独自の Cloud Manager プログラムを作成できました。次に、Cloud Manager を使用して、そのプログラム用の最初の環境を作成する方法を説明します。

このドキュメントを読み終えると、次のことができるようになります。

* 環境とは何かを理解する。
* さまざまな環境の違いを把握する。
* 独自の環境を作成できるようになる。

## 環境とは {#environments}

環境は、Cloud Manager の階層内のプログラムの下に配置されます。プログラムを使用すると、ソリューションを整理し、そのプログラムへのアクセス権を特定のチームメンバーに付与できますが、環境は特定のプログラムに属し、プログラム内のアドビソリューションの個々のインスタンスです。環境は、コンテンツのオーサリングや新しい開発のテストなど、特定の目的で使用されます。Cloud Manager の CI/CD パイプラインを使用すると、Git リポジトリからこれらの環境へのコードのデプロイが容易になります。

旅行関連のメディアに焦点を当てたテナントである理論上の WKND Travel and Adventure Enterprises の例を思い出すと、WKND マガジン部門用の Sites プログラムと WKND メディア部門用の Assets プログラムの 2 つのプログラムがある可能性があります。各プログラムには、サイトの実際のトラフィックを処理する 1 つの実稼動環境と、新しいアプリケーションコードをテストするための 1 つの開発環境など、いくつかの環境が含まれる可能性があります。

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
      * 使用可能な環境または使用中の環境の数は、開発環境タイプの後ろの括弧内に表示されます。
   * 「**環境名**」を入力します。
   * 「**環境の説明**」を入力します。
   * 「**クラウドリージョン**」を選択します。

   ![環境を追加ダイアログ](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 「**保存**」をクリックして、指定された環境を追加します。

環境が使用可能になると、**開発者**&#x200B;製品プロファイルに割り当てられた組織のメンバーは、Cloud Manager にログインして、Cloud Manager Git リポジトリを管理できます。

## 次のステップ {#whats-next}

オンボーディングジャーニーのこのパートを読み終えたので、次のことをできるようになりました。

* 環境とは何かを理解する。
* さまざまな環境の違いを把握する。
* 独自の環境を作成できるようになる。

クラウドリソースが作成され、チームがアクセスする準備が整いました。システム管理者は、最初にチームメンバーを Adobe Admin Console から AEM as a Cloud Service 製品プロファイルに割り当てて、それらのリソースにアクセスできるようにする必要があります。

そのため、AEM as a Cloud Service 製品プロファイルへのチームメンバーの割り当てのドキュメント[を確認して、オンボーディングジャーニーを続ける必要があります。](assign-profiles-aem.md) このドキュメントでは、チームメンバーに新しい環境へのアクセスに必要な権限を付与する方法を説明します。

## その他のリソース {#additional-resources}

その他に、次のリソースも参照してください。

* [環境の管理](/help/implementing/cloud-manager/manage-environments.md) - 作成できる環境のタイプと、Cloud Manager プロジェクト用に環境を作成する方法について説明します。
* [Adobe Cloud Manager の使用 - 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=ja) - Cloud Manager 環境は、AEM オーサリング、パブリッシング、およびディスパッチャーの各サービスで構成されています。様々な環境がどのように役割をサポートし、様々な CI／CD パイプラインを使用して関与できるかについて説明します。
