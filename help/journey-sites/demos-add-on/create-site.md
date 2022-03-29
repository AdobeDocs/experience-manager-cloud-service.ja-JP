---
title: デモサイトを作成
description: 事前設定済みのテンプレートのライブラリに基づいて、AEM にデモサイトを作成します。
exl-id: e76fd283-12b2-4139-9e71-2e145b9620b1
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 79%

---

# デモサイトを作成 {#creating-a-site}

事前設定済みのテンプレートのライブラリに基づいて、AEM にデモサイトを作成します。

## これまでの説明内容 {#story-so-far}

In the previous document of the AEM Reference Demos Add-On journey, [Create Program,](create-program.md) you took the first configuration step to create a program for testing purposes and used a pipeline to deploy the add-on content. その結果、以下を達成できました。

* Cloud Manager を使用して新しいプログラムを作成する方法を理解します。
* 新しいプログラムの Reference Demos Add-On を有効にする方法を理解します。
* パイプラインを実行してアドオンコンテンツをデプロイできます。

この記事では、参照デモアドオンのテンプレートに基づいてAEMで新しいサイトまたはAEM Screensプロジェクトを作成し、プロセスの次の手順について説明します。

## 目的 {#objective}

このドキュメントは、Reference Demo Add-On のテンプレートに基づいて新しいサイトを作成する方法を理解するのに役立ちます。読み終えると、次のことができるようになります。

* AEM オーサリング環境へのアクセス方法を理解する。
* テンプレートに基づくサイトの作成方法を理解します。
* サイト構造内を移動し、ページを編集する際の基本事項を理解する。

## デモサイトの作成 または Screens プロジェクト {#create-site}

パイプラインが Reference Demo Add-On をデプロイしたら、AEM オーサリング環境にアクセスして、アドオンコンテンツに基づくデモサイトを作成できます。

1. Cloud Manager のプログラムの概要ページで、AEM オーサリング環境へのリンクをタップまたはクリックします。

   ![オーサリング環境へのアクセス](assets/access-author.png)

1. AEM のメインメニューで、 **サイト** をタップまたはクリックします。

   ![サイトへのアクセス](assets/access-sites.png)

1. サイトコンソールから、画面の右上にある **作成** をタップまたはクリックし、ドロップダウンで **テンプレートからのサイト** を選択します。

   ![テンプレートからサイトを作成](assets/create-site-from-template.png)

1. サイト作成ウィザードが開始されます。左側の列には、パイプラインがオーサリングインスタンスにデプロイしたデモテンプレートが表示されます。1 つをタップまたはクリックして選択すると、右側の列に詳細が表示されます。AEM Screensのテストやデモをおこなう場合は、必ず **We.Cafe サイトテンプレート**. 「**次へ**」をタップまたはクリックします。

   ![サイト作成ウィザード](assets/site-creation-wizard.png)

1. 次の画面で、サイトまたは Screens プロジェクトのタイトルを指定します。 サイト名を指定できます。省略した場合はタイトルからサイト名が生成されます。「**作成**」をタップまたはクリックします。

   * サイトのタイトルは、ブラウザーのタイトルバーに表示されます。
   * サイト名が URL の一部になります。
   * サイト名は、AEM のページ命名規則に従う必要があります。詳細については、 [その他のリソース](#additional-resources) の節を参照してください。

   ![サイトの詳細](assets/site-details.png)

1. ダイアログで、サイトの作成が確認されます。「**完了**」をタップまたはクリックします。

   ![サイトの作成の完了](assets/site-creation-complete.png)

独自のデモサイトを作成しました。

## デモサイトを使用 {#use-site}

デモサイトが作成されたので、AEM 内の他のサイトと同様に移動して使用できます。

1. サイトがサイトコンソールに表示されます。

   ![サイトコンソールの新しいデモサイト](assets/new-demo-site.png)

1. 画面の右上隅で、コンソールビューが **列表示** に設定されていることを確認します。

   ![列表示](assets/column-view.png)

1. サイトをタップまたはクリックして、その構造とコンテンツを参照します。デモサイトのコンテンツツリーを移動すると、列表示が継続的に展開します。

   ![サイト構造](assets/site-structure.png)

1. ページをタップまたはクリックして選択し、ツールバーの「**編集**」をタップまたはクリックします。

   ![ページを選択](assets/select-page.png)

1. コンポーネントやアセットの追加や編集など、他の AEM コンテンツページと同様にページを編集し、AEM の機能をテストできます。

   ![ページを編集](assets/edit-page.png)

おめでとうございます。これで、デモサイトのコンテンツをさらに詳しく調べ、Reference Demo Add-On のベストプラクティスコンテンツを通じて AEM が提供するすべてを見つけることができます。

他のテンプレートに基づいて追加のサイトを作成し、より多くの AEM 機能を調べます。

## 次の手順 {#what-is-next}

これで、AEM Reference Demo Add-On ジャーニーのこのステップが完了しました。ここで、次のことを行う必要があります。

* AEM オーサリング環境へのアクセス方法を理解する。
* テンプレートに基づくサイトの作成方法を理解します。
* サイト構造内を移動し、ページを編集する際の基本事項を理解する。

アドオンコンテンツを使用して AEM の機能をテストできるようになりました。ジャーニーを続行するには、次の 2 つのオプションがあります。

* AEM Screensのコンテンツの完全なデモとテストをおこなう場合は、 **We.Cafe サイトテンプレート** 前に説明したように、引き続き [デモサイトにAEM Screensを有効にします。](screens.md)
* を使用して Sites コンテンツのデモをおこなう場合は、次に進みます。 [デモサイトの管理、](manage.md) ここでは、デモサイトの管理と削除方法に役立つツールについて説明します。

## その他のリソース {#additional-resources}

* [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=ja) - Cloud Manager の機能について詳しくは、詳細な技術ドキュメントを直接参照してください。
* [サイトを作成](/help/sites-cloud/administering/site-creation/create-site.md) - AEM を使用して、サイトテンプレートを使用してサイトを作成し、サイトのスタイルと構造を定義する方法を説明します。
* [AEM のページ命名規則。](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices) - AEM ページを整理する際の規則を理解するには、このページを参照してください。
* [AEM の基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md) - ナビゲーションやコンソールの組織などの基本的な概念を理解するために AEM を初めて使用する場合は、このドキュメントを参照してください。
