---
title: コンテンツフラグメントのAdobe Targetへの書き出し
description: コンテンツフラグメントのAdobe Targetへの書き出し
source-git-commit: 78840c83d91d6e4f35ec7ca8d14f52024d3535ff
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 42%

---

# コンテンツフラグメントのAdobe Targetへの書き出し {#exporting-content-fragments-to-adobe-target}

>[!CAUTION]
>
>* AEMコンテンツフラグメントは、Adobe Targetのデフォルトのワークスペースに書き出されます。
>* [Adobe Target との統合](/help/sites-cloud/integrating/integrating-adobe-target.md)で説明されている手順に従って、AEM と Adobe Target を統合する必要があります。


書き出し可能 [コンテンツフラグメント](/help/sites-cloud/authoring/fundamentals/content-fragments.md)(Adobe Experience Manager as a Cloud Service(AEM) で作成、Adobe Target(Target) に対して ) 書き出したエクスペリエンスフラグメントは、Target アクティビティのオファーとして使用し、幅広くエクスペリエンスをテストおよびパーソナライズできます。

コンテンツフラグメントをAdobe Targetに書き出すには、次のオプションを使用できます。

* JSON：ヘッドレスコンテンツ配信のサポート

<!-- * GraphQL query ??? -->

AEMコンテンツフラグメントをAdobe Targetに書き出すインスタンスを準備するには、次の操作が必要です。

* [Adobe Target との統合](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [クラウド設定の追加](#add-the-cloud-configuration)
* [レガシー設定の追加](#add-the-legacy-configuration)

その後、以下が可能になります。

* [コンテンツフラグメントをAdobe Targetに書き出す](#exporting-a-content-fragment-to-adobe-target)
* [Adobe Targetでのコンテンツフラグメントの使用](#using-your-content-fragments-in-adobe-target)
* また、 [既にAdobe Targetに書き出されたコンテンツフラグメントを削除する](#deleting-a-content-fragment-already-exported-to-adobe-target)

コンテンツフラグメントは、Adobe Targetのデフォルトのワークスペースに書き出すことも、Adobe Targetのユーザー定義ワークスペースに書き出すこともできます。

>[!NOTE]
>
>Adobe Target ワークスペースは、Adobe Target 自体には存在しません。これらは Adobe IMS（Identity Management System）で定義および管理され、あらゆるソリューションで使用できるように Adobe 開発者コンソールで選択されます。

>[!NOTE]
>
>Adobe Target のワークスペースを使用すると、組織（グループ）のメンバーは、他のユーザーにアクセス権を付与することなく、その組織専用のオファーとアクティビティを作成および管理することができます。例えば、国際的な企業の国別の組織などです。

## 前提条件 {#prerequisites}

次のアクションが必要です。

1. [AEM と Adobe Target を統合する](/help/sites-cloud/integrating/integrating-adobe-target.md)必要があります。

<!-- link rewriter - targets in content-fragments-customizing don't exist yet

1. Content Fragments are exported from the AEM author instance, so you need to [Configure the AEM Link Externalizer](/help/implementing/developing/extending/content-fragments-customizing.md#configuring-the-aem-link-externalizer) on the author instance to ensure that any references within the Content Fragment are externalized for web delivery.

   >[!NOTE]
   >
   >For link rewriting not covered by the default, the [Content Fragment Link Rewriter Provider](/help/implementing/developing/extending/content-fragments-customizing.md#the-content-fragment-link-rewriter-provider-html) is available. With this, customized rules can be developed for your instance.
-->

## クラウド設定の追加 {#add-the-cloud-configuration}

フラグメントを書き出す前に、**Adobe Target** 用の&#x200B;**クラウド設定**&#x200B;をフラグメントまたはフォルダーに追加する必要があります。この結果、次のことも可能になります。

* 書き出しに使用する形式オプションを指定する
* Target ワークスペースを宛先として選択する
* コンテンツフラグメント内の参照を書き換える externalizer ドメインを選択します（オプション）

必要なオプションは、必要なフォルダーやフラグメントの&#x200B;**ページのプロパティ**&#x200B;で選択できます。仕様は必要に応じて継承されます。

1. 次に移動： **Assets** コンソール。

1. 適切なフォルダーまたはフラグメントの&#x200B;**ページのプロパティ**&#x200B;を開きます。

   >[!NOTE]
   >
   >クラウド設定をコンテンツフラグメントの親フォルダーに追加した場合、設定はすべての子に継承されます。
   >
   >クラウド設定をコンテンツフラグメント自体に追加した場合、設定はすべてのバリエーションに継承されます。

1. 「**クラウドサービス**」タブを選択します。

1. **クラウドサービス設定**&#x200B;で、ドロップダウンリストから「**Adobe Target**」を選択します。

   <!-- is this note appropriate? -->

   >[!NOTE]
   >
   >コンテンツフラグメントオファーの JSON 形式はカスタマイズできます。 これをおこなうには、顧客のコンテンツフラグメントコンポーネントを定義し、そのプロパティを Sling Model コンポーネントに書き出す方法に注釈を付けます。
   >
   >次のコアコンポーネントを参照してください。 [コアコンポーネント — コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html)

1. **Adobe Target** で以下を選択します。

   * 適切な設定
   * 必要な形式オプション
   * Adobe Target ワークスペース
   * Externalizer ドメイン（必要な場合）

   >[!CAUTION]
   >
   >Externalizer ドメインはオプションです。
   >
   > AEM Externalizer を設定するのは、コンテンツの書き出し先を特定の&#x200B;*パブリッシュ*&#x200B;ドメインに指定する場合です。詳しくは、[AEM Link Externalizer の設定](/help/implementing/developing/extending/content-fragments-customizing.md#configuring-the-aem-link-externalizer)を参照してください。
   >
   > また、Externalizer ドメインは、Target に送信されるコンテンツフラグメントのコンテンツにのみ関連し、「オファーコンテンツを表示」などのメタデータには関連しません。

   例えば、フォルダーの場合は下図のようになります。

   <!-- need a new screenshot -->

   ![フォルダー - Cloud Services](assets/cf-target-integration-01.png "フォルダー - Cloud Services")

1. **保存して閉じます**。

## レガシー設定の追加 {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>新しいレガシー設定の追加は、コンテンツフラグメントの書き出しでのみサポートされる特殊なシナリオです。

Adobe Experience Platform Launch を使用するための[クラウド設定を追加](#add-the-cloud-configuration)した後で、最初 AEM を Adobe Target と統合するには、レガシー設定を使用して Adobe Target と手動で統合する必要もあります。

### Target クラウド設定の作成 {#creating-a-target-cloud-configuration}

AEMがAdobe Targetとやり取りできるようにするには、Target クラウド設定を作成します。 設定を作成するには、Adobe Targetのクライアントコードとユーザーの資格情報を指定します。

Target クラウド設定を作成するのは、1 回のみです。これは、設定を複数のAEMキャンペーンに関連付けることができるからです。 複数のAdobe Targetクライアントコードがある場合、各クライアントコードに対して 1 つの設定を作成します。

クラウド設定を設定して、Adobe Targetからセグメントを同期することができます。 同期を有効にした場合、クラウド設定が保存されるとすぐに、セグメントがバックグラウンドで Target から読み込まれます。

AEMで Target クラウド設定を作成するには、以下の手順を実行します。

1. **AEM ロゴ**／**ツール**／**クラウドサービス**／**従来のクラウドサービス**&#x200B;を使用して、**従来のクラウドサービス**&#x200B;に移動します。（例：[http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)）

   **Adobe Experience Cloud** の概要ページが開きます。

1. 「**Adobe Target**」セクションで、「**今すぐ設定**」をクリックします。
1. **設定を作成**&#x200B;ダイアログで、次の操作を実行します。

   1. 設定の「**タイトル**」を入力します。
   1. 「**Adobe Target 設定**」テンプレートを選択します。
   1. 「**作成**」をクリックします。

これで、新しい設定を選択して編集できます。

1. 編集ダイアログが開きます。

   ![config-target-settings-dialog](assets/config-target-settings-dialog.png)

   <!-- Can this still occur?

   >[!NOTE]
   >
   >When configuring A4T with AEM, you may see a Configuration reference missing entry. To be able to select the analytics framework, do the following:
   >
   >1. Navigate to **Tools** &gt; **General** &gt; **CRXDE Lite**.
   >1. Navigate to **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   >1. Set the property **disable** to **false**.
   >1. Tap or click **Save All**.

   -->

1. **Adobe Target 設定**&#x200B;ダイアログで、次のプロパティの値を入力します。

   * **認証**：デフォルトは IMS です（ユーザー資格情報は非推奨／廃止予定です）

   * **クライアントコード**：Target アカウントのクライアントコード

   * **テナント ID**：テナント ID です

   * **IMS 設定**：ドロップダウンリストから必要な設定を選択します

   * **API タイプ**：デフォルトは REST です（XML は非推奨／廃止予定です）

   * **A4T Analytics Cloud 設定**：ターゲットアクティビティの目標と指標に使用する Analytics Cloud 設定を選択します。これは、コンテンツをターゲティングするときに、Adobe Analytics をレポートソースとして使用している場合に必要です。

      <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **正確なターゲット設定を使用**：デフォルトでは、このチェックボックスはオンになっています。選択した場合、クラウドサービス設定は、コンテキストの読み込みを待ってから、コンテンツを読み込みます。 次の注意を参照してください。

   * **Adobe Target からセグメントを同期**：Target で定義されているセグメントをダウンロードして AEM で使用するには、このオプションをオンにします。API Type プロパティが REST の場合は、このオプションを選択する必要があります。インラインセグメントはサポートされず、常に Target のセグメントを使用する必要があるからです。 (「セグメント」のAEM用語は、Target の「オーディエンス」と同じです )。

   * **クライアントライブラリ**：デフォルトは AT.js です（mbox.js は非推奨／廃止予定です）。

      >[!NOTE]
      >
      >Target ライブラリファイル [AT.JS](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html?lang=ja) は、Adobe Target 用の新しい実装ライブラリであり、通常の web 実装と単一ページアプリケーションの両方に使用できるように設計されています。
      >
      >mbox.js は非推奨（廃止予定）となり、後日で削除される予定です。
      >
      >Adobeでは、mbox.js ではなく AT.js をクライアントライブラリとして使用することをお勧めします。
      >
      >AT.js は、mbox.js ライブラリに対していくつかの強化点を提供します。
      >
      >* Web 実装のページ読み込み時間の改善
      >* セキュリティの向上
      >* シングルページアプリケーション向けの実装オプションの改善
      >* AT.js は、target.js に含まれるコンポーネントを含むので、target.js を呼び出す必要がなくなりました

      >
      >**クライアントライブラリ**&#x200B;ドロップダウンメニューでは、AT.js または mbox.js を選択できます。

   * **タグ管理システムを使用してクライアントライブラリを提供**：このオプションを選択すると、Adobe Launch または別のタグ管理システム（DTM は非推奨／廃止予定）からクライアントライブラリを使用できます。

   * **カスタムの AT.js**：参照してカスタム AT.js をアップロードします。デフォルトのライブラリを使用する場合は、空白のままにします。

      >[!NOTE]
      >
      >デフォルトでは、Adobe Target 設定ウィザードをオプトインすると、正確なターゲット設定が有効になります。
      >
      >正確なターゲティングとは、クラウドサービスの設定が、コンテキストの読み込みを待ってからコンテンツを読み込むことを意味します。 その結果、パフォーマンスに関しては、正確なターゲティングによって、コンテンツを読み込む前に数ミリ秒の遅延が生じる場合があります。
      >
      >正確なターゲット設定は、オーサーインスタンスで常に有効になっています。 ただし、パブリッシュインスタンスでは、クラウドサービス設定の「正確なターゲティング」の横にあるチェックマークをオフにすることで、正確なターゲティングをグローバルにオフにすることができます (**http://localhost:4502/etc/cloudservices.html**) をクリックします。 また、クラウドサービス設定での設定に関係なく、個々のコンポーネントに対して正確なターゲティングのオン/オフを切り替えることもできます。
      >
      >この設定を変更しても、作成済みの対象コンポーネントには影響しません&#x200B;***。***&#x200B;これらのコンポーネントに対して直接変更を加える必要があります。

1. 「**Adobe Target に接続**」をクリックして、Target の接続を開始します。接続に成功すると、「**接続に成功しました**」というメッセージが表示されます。メッセージの「**OK**」をクリックして、ダイアログの「**OK**」をクリックします。

### Target フレームワークの追加 {#adding-a-target-framework}

<!-- Is this section needed? -->

Target クラウド設定を設定したら、Target フレームワークを追加します。このフレームワークは、使用可能な [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) コンポーネントから Adobe Target に送信されるデフォルトのパラメーターを識別します。Target は、パラメーターを使用して、現在のコンテキストに適用されるセグメントを決定します。

1 つの Target 設定に対して複数のフレームワークを作成できます。 Web サイトのセクションごとに異なるパラメーターセットを Target に送信する必要がある場合は、複数のフレームワークが便利です。 送信する必要のあるパラメーターの各セットに対してフレームワークを作成します。 Web サイトの各セクションを適切なフレームワークに関連付けます。 1 つの web ページは一度に 1 つのフレームワークしか使用できません。

1. Target 設定ページで、「利用可能な設定」の横の「**+**」（プラス符号）をクリックします。

1. フレームワークを作成ダイアログで、「**タイトル**」を指定し、「**Adobe Target フレームワーク**」を選択して、「**作成**」をクリックします。

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   フレームワークページが表示されます。マッピングできる [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) の情報を表すコンポーネントがサイドキックに表示されます。

   <!-- ![chlimage_1-162](assets/chlimage_1-162.png) -->

1. マッピングに使用するデータを表す ClientContext コンポーネントをドロップターゲットにドラッグします。または、**ContextHub ストア**&#x200B;コンポーネントをフレームワークにドラッグします。

   >[!NOTE]
   >
   >マッピング時に、パラメーターは単純な文字列を使用して mbox に渡されます。 ContextHub から配列をマッピングすることはできません。

   例えば、サイト訪問者に関する&#x200B;**プロファイルデータ**&#x200B;を使用して Target キャンペーンを管理するには、「**プロファイルデータ**」コンポーネントをページにドラッグします。Target パラメーターへのマッピングに使用できるプロファイルデータ変数が表示されます。

   <!-- ![chlimage_1-163](assets/chlimage_1-163.png) -->

1. 該当する列の「**共有**」チェックボックスをオンにして、Target システムで表示する変数を選択します。

   <!-- ![chlimage_1-164](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >パラメーターの同期は、AEMからAdobe Targetへの 1 つの方法のみです。

フレームワークが作成されました。 フレームワークをパブリッシュインスタンスにレプリケートするには、 **フレームワークを有効化** オプションを選択します。

<!--
### Associating Activities With the Target Cloud Configuration  {#associating-activities-with-the-target-cloud-configuration}

Associate your [AEM activities](/help/sites-cloud/authoring/personalization/activities.md) with your Target cloud configuration so that you can mirror the activities in [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
>What types of activities are available is determined by the following:
>
>* If the **xt_only** option is enabled on the Adobe Target tenant (clientcode) used on the AEM side to connect to Adobe Target, then you can create **only** XT activities in AEM.
>
>* If the **xt_only** options is **not** enabled on the Adobe Target tenant (clientcode), then you can create **both** XT and A/B activities in AEM.
>
>**Additional note:** **xt_only** options is a setting applied on a certain Target tenant (clientcode) and can only be modified directly in Adobe Target. You cannot enable or disable this option in AEM.
-->

<!--
### Associating the Target Framework With Your Site {#associating-the-target-framework-with-your-site}

After you create a Target framework in AEM, associate your web pages with the framework. The targeted components on the pages send the framework-defined data to Adobe Target for tracking. (See [Content Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).)

When you associate a page with the framework, the child pages inherit the association.

1. In the **Sites** console, navigate to the site that you want to configure.
1. Using either [quick actions](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) or [selection mode](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources), select **View Properties.**
1. Select the **Cloud Services** tab.
1. Tap/click **Edit**.
1. Tap/click **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![chlimage_1-165](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Tap/click **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which allows you to publish it as well.
-->

## コンテンツフラグメントのAdobe Targetへの書き出し {#exporting-a-content-fragment-to-adobe-target}

>[!CAUTION]
>
>画像などのメディアアセットの場合、参照のみが Target に書き出されます。 アセット自体はAEM Assetsに保存されたままで、AEMパブリッシュインスタンスから配信されます。
>
>このため、Target に書き出す前に、関連するすべてのアセットを含むコンテンツフラグメントを公開する必要があります。

（クラウド設定を指定した後に）コンテンツフラグメントをAEMから Target に書き出すには、次の手順を実行します。

1. 内のコンテンツフラグメントに移動します。 **Assets** コンソール。
1. ターゲットに書き出すコンテンツフラグメントを選択します。

1. タップまたはクリック **Adobe Targetに書き出し**.

   ![Adobe Target に書き出し](assets/cfm-export-target-01.png)

   <!-- this note doesn't seem to be accurate for CFs -->

   <!--
   
   >[!NOTE]
   >
   >If the Content Fragment has already been exported, select **Update in Adobe Target**.
   
   -->

1. タップまたはクリック **公開せずに書き出し** または **公開** 必要に応じて。

   >[!NOTE]
   >
   >選択 **公開** コンテンツフラグメントをすぐに公開し、Target に送信します。

1. 確認ダイアログで「**OK**」をタップ／クリックします。

   これで、コンテンツフラグメントが Target に表示されます。

   >[!NOTE]
   >
   >書き出しについての[様々な詳細](/help/sites-cloud/authoring/fundamentals/content-fragments.md#details-of-your-content-fragment)は、コンソールの&#x200B;**リスト表示**&#x200B;と&#x200B;**プロパティ**&#x200B;で参照できます。

   >[!NOTE]
   >
   >Adobe Targetでコンテンツフラグメントを表示すると、 *最終変更日* 表示される日付は、フラグメントがAdobe Targetに最後に書き出された日付ではなく、AEMでフラグメントが最後に変更された日付です。

>[!NOTE]
>
>または、ページエディターで、 [ページ情報](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) メニュー

## Adobe Targetでのコンテンツフラグメントの使用 {#using-your-content-fragments-in-adobe-target}

上記のタスクを実行すると、コンテンツフラグメントが Target のオファーページに表示されます。 ご覧ください [特定の Target ドキュメント](https://experienceleague.adobe.com/docs/target/using/integrate/aem/fragments/content-fragments-aem.html) そこで何を達成できるかを学ぶために

>[!NOTE]
>
>Adobe Targetでコンテンツフラグメントを表示すると、 *最終変更日* 表示される日付は、フラグメントがAdobe Targetに最後に書き出された日付ではなく、AEMでフラグメントが最後に変更された日付です。

## Adobe Targetに既に書き出されているコンテンツフラグメントの削除 {#deleting-a-content-fragment-already-exported-to-adobe-target}

書き出しと同様に、Adobe Targetからコンテンツフラグメントを削除する場合は、 **Assets** フラグメントを選択した場合のコンソール：

![Adobe Target で削除](assets/cfm-export-target-02.png)

Target に既に書き出されているコンテンツフラグメントを削除すると、そのフラグメントが既に Target のオファーで使用されている場合に問題が発生する可能性があります。 フラグメントコンテンツがAEMによって配信されるので、フラグメントを削除すると、オファーが使用できなくなります。

<!-- if the information about deleting-if-used correct, or is it not allowed at all? -->

このような状況を回避するには、次の手順に従います。

* コンテンツフラグメントが現在アクティビティで使用されていない場合、AEMを使用すると、警告メッセージを表示せずにフラグメントを削除できます。
* コンテンツフラグメントが Target のアクティビティで現在使用中の場合は、フラグメントを削除するとアクティビティに発生する可能性がある結果について、AEMユーザーに警告するエラーメッセージが表示されます。

   AEMのエラーメッセージは、ユーザーによるコンテンツフラグメントの削除（強制）を禁止していません。 コンテンツフラグメントを削除した場合：

   * AEMコンテンツフラグメントを含む Target オファーで、望ましくない動作が表示される場合があります

      * コンテンツフラグメントが Target にプッシュされたので、オファーは引き続きレンダリングされる可能性が高くなります
      * 参照元のアセットがAEMでも削除された場合、コンテンツフラグメント内の参照は正しく機能しない可能性があります。
   * もちろん、コンテンツフラグメントはAEMには存在しなくなったので、コンテンツフラグメントに対するそれ以上の変更はできません。


## その他のリソース {#further-resources}

詳しくは、以下も参照してください。

<!--
* [Creating a Target Cloud Configuration](/help/sites-cloud/integrating/integrating-adobe-target.md#create-configuration)
-->

* [コアコンポーネント — コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html)

* [Adobe Target Developers](https://developers.adobetarget.com/)

* [Adobe Target - Target アクティビティでAEMコンテンツフラグメントを使用して、最適化やパーソナライゼーションを支援する](https://experienceleague.adobe.com/docs/target/using/integrate/aem/fragments/content-fragments-aem.html)

* [Adobe Target - AEMエクスペリエンスフラグメントとコンテンツフラグメントの概要](https://experienceleague.adobe.com/docs/target/using/integrate/aem/fragments/aem-experience-and-content-fragments.html)
