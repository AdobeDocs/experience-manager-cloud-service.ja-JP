---
title: プロジェクト作成ウィザード
description: 実稼動プログラムを作成した後、プロジェクトをすばやく設定するのに役立つプロジェクト作成ウィザードについて説明します。
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 100%

---

# プロジェクト作成ウィザード {#project-creation-wizard}

実稼動プログラムを作成した後、Cloud Manager には、すばやく開始できるように、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)に基づいて最小限の AEM プロジェクトを作成するためのウィザードが用意されています。

Cloud Manager でウィザードを使用して AEM アプリケーションプロジェクトを作成するには、次の手順に従います。

1. [実稼動プログラムの作成](creating-production-programs.md)ドキュメントの手順に従って、実稼動プログラムを作成します。

1. プログラムの設定が完了したら、プログラムの&#x200B;**概要**&#x200B;画面にアクセスし、最上部にある&#x200B;**分岐とプロジェクトを作成**&#x200B;コールトゥアクションカードを確認します。

   ![ウィザードのコールトゥアクションケア](assets/create-wizard1.png)

1. 「**作成**」をクリックしてウィザードを起動し、**分岐とプロジェクトを作成**&#x200B;ウィンドウでプロジェクトの「**タイトル**」および「**新しい分岐名**」を確認します。

   ![分岐とプロジェクトを作成](assets/create-wizard2.png)

1. オプションで、分割部分をクリックしてプロジェクトのその他のパラメーターを表示します。デフォルト値は AEM プロジェクトアーキタイプによって指定され、通常は変更する必要はありません。

   ![追加のプロジェクトパラメーター](assets/create-wizard5.png)

1. 「**作成**」をクリックして、プロジェクト作成プロセスを開始します。


 **プログラムの概要**&#x200B;画面の上部にある&#x200B;**分岐とプロジェクトを作成**&#x200B;コールトゥアクションカードが、**プロジェクトを作成中**&#x200B;カードに置き換えられます。

![プロジェクト作成中](assets/create-wizard3.png)

プログラムの作成が完了すると、**プログラムの概要**&#x200B;画面の上部にある&#x200B;**プロジェクトを作成中**&#x200B;カードが、**環境を追加**&#x200B;カードに置き換えられます。

![環境を追加](assets/create-wizard4.png)

これで、AEM アーキタイプに基づく AEM プロジェクトが Git リポジトリに追加され、自身のプロジェクトの開発基盤として活用できます。次に、プロジェクトコードをデプロイできる環境を作成できます。

環境を追加または管理する方法については、「[環境の管理](/help/implementing/cloud-manager/manage-environments.md)」を参照してください。

>[!NOTE]
>
>このウィザードは、実稼動プログラムでのみ使用できます。[サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation)にはプロジェクトの自動作成が含まれているため、このウィザードは不要です。