---
title: エクスペリエンスフラグメントのAdobe Targetへの書き出し
description: エクスペリエンスフラグメントのAdobe Targetへの書き出し
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 50%

---

# エクスペリエンスフラグメントのAdobe Targetへの書き出し{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* AEMエクスペリエンスフラグメントは、Adobe Targetのデフォルトのワークスペースに書き出されます。
>* AEMは、 [Adobe Targetとの統合](/help/sites-cloud/integrating/integrating-adobe-target.md).


書き出し可能 [エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)(Adobe Experience Manager as a Cloud Service(AEM) で作成、Adobe Target(Target) に対して ) 書き出したエクスペリエンスフラグメントは、Target アクティビティのオファーとして使用し、幅広くエクスペリエンスをテストおよびパーソナライズできます。

エクスペリエンスフラグメントをAdobe Target に書き出す際には、3 つのフォーマットオプションを利用できます。

* HTML（デフォルト）:Web およびハイブリッドコンテンツ配信のサポート
* JSON:ヘッドレスコンテンツ配信のサポート
* HTML と JSON

後 [Adobe Targetとの統合](/help/sites-cloud/integrating/integrating-adobe-target.md) AEMエクスペリエンスフラグメントは、Adobe Targetのデフォルトのワークスペースに書き出したり、Adobe Targetのユーザー定義のワークスペースに書き出したりできます。

>[!NOTE]
>
>Adobe Targetワークスペースは、Adobe Target自体には存在しません。 これらはAdobe IMS(Identity Management System) で定義および管理され、Adobe I/O統合を使用するソリューション間での使用に選択されます。

>[!NOTE]
>
>Adobe Targetのワークスペースを使用して、組織（グループ）のメンバーに対し、この組織のオファーとアクティビティの作成と管理のみを許可できます。他のユーザーへのアクセス権を付与することなく 例えば、グローバルに関係する国固有の組織などです。

>[!NOTE]
>
>詳しくは、以下を参照してください。
>
>* [Adobe Target開発](https://www.adobe.io/apis/experiencecloud/target.html)
>* [コアコンポーネント — エクスペリエンスフラグメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
>* [Adobe Target - Adobe Experience Manager(AEM) エクスペリエンスフラグメントを使用する方法を教えてください。](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)


## 前提条件 {#prerequisites}


様々なアクションが必要です。

1. 必要な操作 [AEMとAdobe Targetの統合](/help/sites-cloud/integrating/integrating-adobe-target.md).
2. エクスペリエンスフラグメントはAEMオーサーインスタンスから書き出されるので、次の操作を行う必要があります。 [AEM Link Externalizer を設定](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) オーサーインスタンスを使用して、エクスペリエンスフラグメント内の参照が Web 配信用に外部化されていることを確認します。

   >[!NOTE]
   >
   >デフォルトでカバーされていないリンクの書き換えでは、[Experience Fragment Link Rewriter Provider](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) が利用可能です。これにより、インスタンスに合わせてカスタマイズされたルールを開発できます。

## クラウド設定を追加 {#add-the-cloud-configuration}

フラグメントを書き出す前に、**Adobe Target** 用の&#x200B;**クラウド設定**&#x200B;をフラグメント、またはフォルダーに追加する必要があります。また、次のことも可能です。

* エクスポートに使用するフォーマットオプションを指定します
* 宛先としての Target ワークスペースの選択
* エクスペリエンスフラグメント内の参照を書き換える externalizer ドメインを選択します（オプション）

必要なオプションは、必要なフォルダーやフラグメントの&#x200B;**ページのプロパティ**&#x200B;で選択できます。仕様は必要に応じて継承されます。

1. **エクスペリエンスフラグメント**&#x200B;コンソールに移動します。

1. 適切なフォルダーまたはフラグメントの&#x200B;**ページのプロパティ**&#x200B;を開きます。

   >[!NOTE]
   >
   >クラウド設定をエクスペリエンスフラグメントの親フォルダーに追加すると、設定はすべての子に継承されます。
   >
   >
   >クラウド設定をエクスペリエンスフラグメント自体に追加すると、設定はすべての変更によって継承されます。

1. 「**クラウドサービス**」タブを選択します。

1. の下 **Cloud Service設定**&#x200B;を選択します。 **Adobe Target** 」を選択します。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントオファーの JSON 形式はカスタマイズできます。 これをおこなうには、顧客のエクスペリエンスフラグメントコンポーネントを定義し、そのプロパティを Sling Model コンポーネントに書き出す方法に注釈を付けます。
   >
   >次のコアコンポーネントを参照してください。
   >
   >[コアコンポーネント — エクスペリエンスフラグメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

   の下 **Adobe Target** 選択：

   * 適切な設定
   * 必須フォーマットオプション
   * Adobe Target
   * 必要に応じて、Externalizer ドメインを設定します。

   >[!CAUTION]
   >
   >Externalizer ドメインはオプションです。
   >
   > AEM Externalizer は、書き出されるコンテンツが特定の *公開* ドメイン。 詳しくは、 [AEM Link Externalizer の設定](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > また、Externalizer ドメインは、Target に送信されるエクスペリエンスフラグメントのコンテンツにのみ関連し、「オファーコンテンツを表示」などのメタデータには関連しません。

<!--
   For example, for a folder:

   ![Folder - Cloud Services](assets/xf-target-integration-01.png "Folder - Cloud Services")
-->

1. **保存して閉じます**。

## エクスペリエンスフラグメントのAdobe Targetへの書き出し {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>画像などのメディアアセットでは、参照のみが Target に書き出されます。アセット自体は AEM Assets に格納されたままで、AEM パブリッシュインスタンスから配信されます。
>
>このため、エクスペリエンスフラグメントは、すべての関連アセットと共に、Target に書き出す前に公開する必要があります。

AEM から Target にエクスペリエンスフラグメントを書き出すには（クラウド設定を指定した後）：

1. エクスペリエンスフラグメントコンソールに移動します。
1. Target に書き出すエクスペリエンスフラグメントを選択します。

   >[!NOTE]
   >
   >エクスペリエンスフラグメント Web のバリエーションである必要があります。

1. **Adobe Target に書き出し**&#x200B;をタップ／クリックします。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントがすでに書き出されている場合は、**Adobe Target でアップデート** を選択します。

1. 要求に応じて&#x200B;**公開せずに書き出し**&#x200B;または&#x200B;**公開**&#x200B;をタップ／クリックします。

   >[!NOTE]
   >
   >**公開**&#x200B;を選択すると、エクスペリエンスフラグメントはすぐに公開され、Target に送信されます。

1. タップまたはクリック **OK** をクリックします。

   エクスペリエンスフラグメントは Target に送信されているはずです。

   >[!NOTE]
   >
   >書き出しについての[様々な詳細](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment)は、コンソールの&#x200B;**リストビュー**&#x200B;と&#x200B;**プロパティ**&#x200B;で参照できます。

   >[!NOTE]
   >
   >Adobe Target でエクスペリエンスフラグメントを表示すると、表示される&#x200B;*最終変更日*&#x200B;は、フラグメントが最後に Adobe Target に書き出された日付ではなく、AEM でフラグメントが最後に変更された日付です。

>[!NOTE]
>
>あるいは、[ページ情報](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information)メニューの同等のコマンドを使用して、ページエディターから書き出しを実行することもできます。

## Adobe Targetでのエクスペリエンスフラグメントの使用 {#using-your-experience-fragments-in-adobe-target}

上記のタスクを実行すると、エクスペリエンスフラグメントが Target のオファーページに表示されます。 Target 側でできることを詳しく知るには、[Target に特化したドキュメント](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html)を参照してください。

>[!NOTE]
>
>Adobe Target でエクスペリエンスフラグメントを表示すると、表示される&#x200B;*最終変更日*&#x200B;は、フラグメントが最後に Adobe Target に書き出された日付ではなく、AEM でフラグメントが最後に変更された日付です。

## Adobe Targetに既に書き出されているエクスペリエンスフラグメントの削除 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Target に書き出し済みのエクスペリエンスフラグメントを削除すると、そのフラグメントがすでに Target のオファーで使用されている場合に問題が発生する可能性があります。フラグメントのコンテンツが AEM によって配信されているため、フラグメントを削除するとオファーが使用できなくなります。

そのような状況を避けるためには：

* エクスペリエンスフラグメントが現在アクティビティで使用されていない場合、AEM はユーザーに警告メッセージなしでフラグメントを削除することを許可します。
* エクスペリエンスフラグメントが現在ターゲットのアクティビティで使用されている場合、フラグメントを削除するとアクティビティに影響が及ぶ可能性があると、AEM ユーザーに警告メッセージが表示されます。

   AEM のエラーメッセージは、ユーザーがエクスペリエンスフラグメントを（強制的に）削除することを禁止するものではありません。エクスペリエンスフラグメントを削除した場合：

   * AEMエクスペリエンスフラグメントを含む Target オファーで、望ましくない動作が表示される場合があります

      * エクスペリエンスフラグメントHTMLが Target にプッシュされたので、オファーは引き続きレンダリングされる可能性が高くなります
      * 参照元のアセットがAEMでも削除された場合、エクスペリエンスフラグメント内の参照は正しく機能しない可能性があります。
   * もちろん、エクスペリエンスフラグメントがAEMに存在しなくなったので、エクスペリエンスフラグメントに対するそれ以上の変更は不可能です。
