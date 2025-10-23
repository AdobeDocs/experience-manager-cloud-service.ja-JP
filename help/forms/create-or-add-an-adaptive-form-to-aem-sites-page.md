---
title: アダプティブフォームを AEM Sites ページに追加する方法？
description: アダプティブフォームを容易に作成または AEM Sites ページに追加する方法を学びます。また、利点や、フォームを Web サイトに統合する様々な方法についても説明します。
feature: Adaptive Forms, Foundation Components
Keywords: AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
exl-id: a1846c5d-7b0f-4f48-9d15-96b2a8836a9d
role: User, Developer
source-git-commit: 958c166585ac7eeb667d73744403558b2dc5ce94
workflow-type: tm+mt
source-wordcount: '3339'
ht-degree: 95%

---

# AEM Sites ページまたはエクスペリエンスフラグメントにアダプティブフォームの追加 {#create-or-add-an-adaptive-form-to-aem-sites-page}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

## 概要 {#overview}

AEM Forms を使用すれば、アダプティブフォームを AEM Sites ページにシームレスに追加できます。これにより、訪問者は、ページを離れることなく、フォームに簡単に入力して送信できます。これにより、web サイト上の他の要素とのやり取りを容易に行いながら、フォームを積極的に操作できます。

AEM ページエディターを使用すると、複数のフォームをすばやく作成して AEM Sites ページに追加できます。AEM ページエディターを使用すると、コンテンツ作成者は、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームのコンポーネントを活用して、Sites ページ内にシームレスなデータキャプチャのエクスペリエンスを作成できます。また、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sites ページの様々な機能を使用できます。

AEM Forms にはアダプティブフォームコンテナおよびアダプティブフォーム（埋め込みコンポーネント）が用意されています。アダプティブフォームコンテナを使用して、エクスペリエンスフラグメントまたは AEM Sites ページでフォームを作成できます。アダプティブフォーム – 埋め込みコンポーネントでは、既存のアダプティブフォームを追加したり、アダプティブフォームエディターを使用してフォームを作成できます。

![AEM Sites ページでのアダプティブフォームの例](/help/forms/assets/adaptive-form-in-sites-page.png)

## アダプティブFormsコアコンポーネントを使用して、AEM Sitesページまたはエクスペリエンスフラグメント内にアダプティブフォームを作成するのはなぜですか？

過去に Sites 用にアダプティブForms基盤コンポーネントまたはプレーンHTMLベースのフォームを作成している場合、Adobeでは、アダプティブFormsコアコンポーネントを使用してAEM Sitesページまたはエクスペリエンスフラグメントでアダプティブフォームを作成することをお勧めします。 また、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sites ページの様々な機能を使用して、フォームの全体的な作成と管理のエクスペリエンスを強化できます。次の機能の一部を見てみましょう。

* **バージョン管理：** AEM Sites ページは、[堅牢なバージョン管理機能](/help/sites-cloud/authoring/sites-console/page-versions.md)を提供し、フォームの様々なバージョンを追跡および管理できます。これにより、必要に応じて以前のバージョンにロールバックする機能を維持しながら、フォームに変更や機能強化を加えることができます。バージョン管理により、フォームの開発と進化に対する制御可能で体系的なアプローチが実現します。
* **ターゲティング（Adobe Target との統合）：** AEM Sites ページのターゲティング機能を使用して、[様々なオーディエンス向けにフォームエクスペリエンスをパーソナライズします](/help/sites-cloud/integrating/integrating-adobe-target.md)。ユーザーセグメントおよびターゲティング条件を使用することで、特定のユーザーグループに合わせてフォームのコンテンツ、デザインまたは動作を調整できます。これにより、パーソナライズされた関連性の高いフォームエクスペリエンスを提供し、エンゲージメント率とコンバージョン率を高めることができます。
* **翻訳：** AEM Sites [翻訳サービスとのシームレスな統合](/help/sites-cloud/administering/translation/overview.md)を使用すると、フォームを複数の言語に簡単に翻訳できます。この機能により、ローカライゼーションプロセスが簡素化され、グローバルなオーディエンスがフォームに確実にアクセスできるようになります。AEM 翻訳プロジェクト内で翻訳を効率的に管理できるので、多言語フォームのサポートに必要な時間と労力を削減できます。翻訳について詳しくは、考慮事項の節を参照してください。
* **マルチサイト管理とライブコピー：** AEM Sites [マルチサイト管理およびライブコピー機能](/help/sites-cloud/administering/msm/overview.md)を使用すると、1 つの環境内で複数の web サイトを作成および管理できます。この機能を使用すると、異なるサイト間でフォームを再利用できるようになり、一貫性を確保し、重複作業を減らすことができます。一元化された制御と管理により、複数の web サイトにわたってフォームの管理と更新を効率的に行うことができます。
* **テーマ：** AEM Sites ページには、複数の web ページをまたいで一貫したビジュアルスタイルをデザインし、維持するためのフレームワークが用意されています。これらは、web サイトの全体的なルックアンドフィールに貢献するカラー、フォント、スタイルシートおよびその他のビジュアル要素を定義します。[アダプティブフォームで AEM Sites ページ用に設計されたテーマを使用することで、時間と労力を節約できます](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes)。
* **タグ付け：** AEM Sites ページでは、[ページ、アセットまたは他のコンテンツへのタグやラベルの割り当て](/help/implementing/developing/introduction/tagging-framework.md)の操作を実行できます。タグは、特定の条件に基づいてコンテンツを分類および整理する方法を提供するキーワードまたはメタデータラベルです。AEM 内のページやアセットまたはその他のコンテンツ項目にタグを 1 つ以上割り当てて、検索を改善し、アセットを分類できるようにします。
* **コンテンツのロックとロック解除：** AEM Sites でユーザーは[ページへのアクセスと変更の制御](/help/sites-cloud/authoring/page-editor/edit-content.md)を AEM Sites 環境内で実行できます。ページがロックされている場合、他のユーザーによる不正な変更や編集から保護されています。コンテンツをロックしたユーザーまたは指定された管理者のみが、ロックを解除して変更を許可できます。

また、AEM ページエディターのアダプティブフォームは、[アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja#features)を使用します。これらのコアコンポーネントは、[AEM Sites WCM コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)と同じで、コンポーネントを標準的でより簡単にスタイルおよびカスタマイズする方法を提供します。


## AEM Sites ページまたは AEM エクスペリエンスフラグメントでアダプティブフォームを作成または追加する方法？ {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

次のオプションを使用すると、この機能を最大限に活用できます。

* **[カスタムアダプティブフォームを作成し、AEM Sites ページに追加](#create-an-adaptive-form-in-sites-editor-or-experience-fragment)：**&#x200B;アダプティブフォームコンテナコンポーネントを使用すると、要件やデザインの好みに合わせてカスタマイズし、新規フォームをゼロから作成します。

* **[カスタムアダプティブフォームを作成し、エクスペリエンスフラグメントに追加](#create-an-adaptive-form-in-sites-editor)：** AEM エクスペリエンスフラグメントにフォームを追加して、フォームのリーチを拡張し、複数のページやサイトでシームレスに再利用できます。

* **[アダプティブフォームをエクスペリエンスフラグメントに変換](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)：** AEM Sites ページに追加されたアダプティブフォームをエクスペリエンスフラグメントに変換して、複数の AEM Sites ページでフォームを再利用します。

* **[承認済みのテンプレートに基づいてフォームを作成し、AEM Sites ページに追加：](/help/forms/embed-adaptive-form-aem-sites.md#embed-form-using-adaptive-form-wizzard-aem-sites)**&#x200B;事前に承認されたテンプレートを活用して、組織のブランディングガイドラインやデザイン標準に合ったアダプティブフォームをすばやく作成できます。このオプションは、アダプティブフォームエディターまたはアダプティブフォーム - 埋め込みコンポーネントでのみで使用できます。

* **[既存のフォームを AEM Sites ページに追加：](/help/forms/embed-adaptive-form-aem-sites.md#embed-an-adaptive-form-in-sites-editor)**&#x200B;作成済みのフォームを web サイトに簡単に統合し、訪問者が直接操作できるようにします。このオプションは、アダプティブフォームエディターまたはアダプティブフォーム - 埋め込みコンポーネントでのみで使用できます。


* **複数のフォームを AEM Sites ページまたはエクスペリエンスフラグメントに追加：**&#x200B;複数のアダプティブフォームを作成し、AEM Sites ページに追加して、ユーザーの環境設定や要件に基づいて複数の選択肢をユーザーに提供します。新規フォームと既存フォームを組み合わせることができます。以下を使用すると、 **[!UICONTROL アダプティブフォームコンテナ]** コンポーネントを複数回追加して、AEM SitesページにアダプティブFormsを追加します。 以下を使用すると、 **[!UICONTROL アダプティブForms — 埋め込み]** AEM Sitesページでコンポーネントを複数回作成する ( **[!UICONTROL フォームはフレームの幅全体をカバーします]** 」オプションが選択されている。 例えば、 **[!UICONTROL フォームはフレームの幅全体をカバーします]** 「 」オプションがオフの場合、AEM Sitesページでは、iframe なしで存在するアダプティブフォームが 1 つだけサポートされます。 を使用してアダプティブFormsをさらに追加するには **[!UICONTROL アダプティブForms — 埋め込み]** コンポーネント、選択 **[!UICONTROL フォームはフレームの幅全体をカバーします]** オプション。

## AEM Sites ページまたは AEM エクスペリエンスフラグメントでアダプティブフォームを作成する際の考慮事項 {#consideration}

* アダプティブフォームコンテナを使用してフォームを作成または追加する場合、フォームは AEM Sites 翻訳フローを通じて翻訳およびローカライゼーションが実行されます。言語ごとに、Sites ページと対応するフォームの個別のコピー（言語コピー）が生成され、コンテンツ作成者が親ページのフォームのルールを変更する場合は、全言語のフォームのコピーで同じ変更を行う必要があります。アダプティブフォームコンテナでは、AEM Sites ページの様々な機能（バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど）を使用できます。

* アダプティブフォーム - 埋め込みコンポーネントを使用してフォームを作成または追加する場合、そのフォームは AEM Forms の翻訳フローを使用して翻訳およびローカライゼーションが実行されます。この場合、単一のフォームが維持され、Sites ページのすべての言語コピーで参照されます。アダプティブフォーム - 埋め込みコンポーネントでは、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sites ページの様々な機能にアクセスできません。


## AEM Sites ページまたは AEM エクスペリエンスフラグメントでアダプティブフォームを作成または追加するための要件 {#before-you-start-creating-an-adaptive-form}

アダプティブフォームの作成を開始する前に、アダプティブフォームコアコンポーネントを有効にして、AEM Sites ページにアダプティブフォームクライアントライブラリを追加します。

### AEM Cloud Service 環境でのアダプティブフォームコアコンポーネントの有効化

お使いの AEM Cloud Service 環境でアダプティブフォームコアコンポーネントを有効にするには、最新版をインストールします。

### AEM Sites ページまたはエクスペリエンスへのアダプティブ Forms クライアントライブラリの追加

**ケース 1：個別の Sites ページコンポーネントの使用**

アダプティブフォームコンテナコンポーネントの完全な機能を有効にするには、デプロイメントパイプラインを使用して、Customheaderlibs および Customfooterlibs クライアントライブラリを AEM Sites ページに追加します。ライブラリを追加するには、次の手順を実行します。

1. [AEM Cloud Service Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html?lang=ja)にアクセスしてクローンを作成します。
1. プランテキストエディターで AEM Cloud Service Git リポジトリフォルダーを開きます。例えば Microsoft Visual Code などです。
1. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //Customheaderlibs.html
   
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [デプロイメントパイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=ja)して、クライアントライブラリを AEM as a Cloud Service 環境にデプロイします。

>[!NOTE]
>
> カスタム関数のクライアントライブラリは、すべてのフォームで必要な場合にのみハードコードします。 フォームタイプによって異なるライブラリの場合は、次の節で説明するように、テンプレートページポリシーを使用して追加します。

**ケース 2：同じ Sites ページコンポーネントの使用**

フォームを使用してページを作成するために使用するテンプレートのページポリシーに、ランタイムクライアントライブラリまたはカスタム関数ライブラリを含めます。

1. AEM Sites ページまたはエクスペリエンスフラグメントを編集用に開きます。ページを編集用に開くには、ページを選択して「**[!UICONTROL 編集]**」をクリックします。
2. Sites ページまたはエクスペリエンスフラグメントページのテンプレートを開きます。テンプレートを開くには、**[!UICONTROL ページ情報]**&#x200B;に移動し、![ページ情報](/help/forms/assets/Smock_Properties_18_N.svg)／**[!UICONTROL テンプレートを編集]**&#x200B;を選択します。対応するテンプレートがテンプレートエディターで開きます。
3. テンプレートの「**[!UICONTROL ページ情報]**![&#x200B; ページ情報 &#x200B;](/help/forms/assets/Smock_Properties_18_N.svg)」セクションに移動し、「**[!UICONTROL ページポリシー]**」オプションを選択します。 これにより、AEM Sites テンプレートのプロパティが開き、カスタム関数またはランタイムクライアントライブラリを定義できます。
4. 「**[!UICONTROL プロパティ]**」タブの「**[!UICONTROL 追加]**」ボタンをクリックして、新しいカスタム関数ライブラリまたはランタイムライブラリを追加します。
5. 「**[完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3476178?quality=12&learn=on)

### AEM Sites ページまたはエクスペリエンスフラグメントのアダプティブフォームコンテナの有効化

テンプレートのポリシーで[!UICONTROL アダプティブフォームコンテナ]コンポーネントを有効にするには、次の手順を実行します。

1. AEM Sites ページまたはエクスペリエンスフラグメントを編集用に開きます。ページを編集用に開くには、ページを選択して「編集」をクリックします。
1. Sites ページまたはエクスペリエンスフラグメントページのテンプレートを開きます。テンプレートを開くには、[!UICONTROL ページ情報]に移動し、![ページ情報](/help/forms/assets/Smock_Properties_18_N.svg)／[!UICONTROL テンプレートを編集]を選択します。対応するテンプレートがテンプレートエディターで開きます。
1. 構造ビューで、メニューバーから「**[!UICONTROL ポリシー]**」![ポリシー](/help/forms/assets/Smock_FeedManagement_18_N.svg)アイコンをクリックします。**[!UICONTROL 許可されたコンポーネント]**&#x200B;リストで、**[AEM アーキタイププロジェクト名] - アダプティブフォーム**&#x200B;の下にある&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;チェックボックスを選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

## アダプティブフォームを作成します {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

要件やデザインの環境設定に合わせて、AEM Sites ページまたはエクスペリエンスフラグメント内で直接新しいフォームを最初から作成できます。単一用途のフォームの場合は、AEM Sites ページへの直接オーサリングをお勧めします。一方、エクスペリエンスフラグメントは、web サイトの複数のページで再利用する必要があるフォームに最適です。

* [AEM Sites ページでフォームを作成](#create-an-adaptive-form-in-sites-editor)
* [エクスペリエンスフラグメント内にフォームを作成](#create-an-adaptive-form-in-experience-fragment)
* [AEM Sites ページ内のアダプティブフォームをエクスペリエンスフラグメントに変換](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### AEM Sites ページでフォームを作成 {#create-an-adaptive-form-in-sites-editor}

AEM ページエディターのアダプティブフォームコンテナコンポーネントを使用して、カスタムフォームを作成できます。このコンポーネントを使用すると、フォームコンポーネントをドラッグ＆ドロップしてフォームを作成できます。フォームコンポーネントは、コアコンポーネントに基づいています。これらは、組織の要件に応じて簡単にカスタマイズできます。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Sites ページでアダプティブフォームを作成するには、次の手順を実行します。

1. AEM Sites ページを編集モードで開きます。
1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントをコンポーネントブラウザーから Sites ページにラッグ＆ドロップします。ページ上にフォーム用のスペースが作成されます。レイアウトモードを使用して、コンテナスペースのサイズを変更できます。
1. アダプティブフォームのコアコンポーネントをコンテナスペースにドラッグ＆ドロップしてフォームを作成します。
1. 「送信」ボタンを追加します。

次に、[送信アクションを設定](#configure-submit-action-for-form)し、詳細プロパティを設定します。

### エクスペリエンスフラグメントでフォームを作成 {#create-an-adaptive-form-in-experience-fragment}

フォームを AEM エクスペリエンスフラグメントに追加すると、フォームの範囲を拡張して、複数のページやサイトでシームレスに再利用できます。例えば、エクスペリエンスフラグメント内にニュースレターのサインアップフォームを含めることができます。これにより、web サイトの複数のページでフラグメントを簡単に再利用できるので、フォームを繰り返し再作成する必要がなくなります。エクスペリエンスフラグメント内のニュースレターサインアップフォームに加えた更新や変更は、同じフォームを使用しているすべてのページに自動的に反映されます。これにより、プロセスが合理化され、web サイトのフォームの管理をシンプル化しながら、ユーザーエクスペリエンスをシームレス化することができます。

エクスペリエンスフラグメント内にアダプティブフォームを作成するには、次の手順を実行します。

1. エクスペリエンスフラグメントを開きます。
1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントを、コンポーネントブラウザーからエクスペリエンスフラグメントにドラッグ＆ドロップします。
1. アダプティブフォームコアコンポーネントをエクスペリエンスフラグメントのコンテナスペースにドラッグ＆ドロップして、フォームを作成します。
1. 「送信」ボタンを追加します。

次に、[送信アクションを設定](#configure-submit-action-for-form)し、詳細プロパティを設定します。

### AEM Sites ページ内のフォームをエクスペリエンスフラグメントに変換 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Sites ページエディター内にある既存のアダプティブフォームをエクスペリエンスフラグメントに変換すると、複数のページやサイトでフォームを再利用できます。

AEM Sites ページ内のアダプティブフォームをエクスペリエンスフラグメントに変換するには、次の手順を実行します。

1. アダプティブフォームを含む AEM Sites ページ（アダプティブフォームコンテナコンポーネント内）を編集モードで開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. メニューバーで、![「エクスペリエンスフラグメントバリエーションに変換」アイコン](/help/forms/assets/Smock_FilingCabinet_18_N.svg)を選択します。「エクスペリエンスフラグメントバリエーションに変換」アイコン。
   ![ファイルキャビネットのロゴをクリックして、AEM Sites ページのアダプティブフォームをエクスペリエンスフラグメントに変換](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   アダプティブフォームコンテナを新しいエクスペリエンスフラグメントに変換するか、既存のエクスペリエンスフラグメントに追加するためのダイアログボックスが表示されます。
1. エクスペリエンスフラグメントバリエーションに変換ダイアログボックスで、次のオプションの値を設定します。

   * **アクション：**&#x200B;新しいエクスペリエンスフラグメントを作成するか、既存のエクスペリエンスフラグメントに追加するかを選択します。
   * **親パス：**&#x200B;エクスペリエンスフラグメントをホストするフォルダーのパスを指定します。このオプションは、エクスペリエンスフラグメントを作成する場合にのみ使用できます。
   * **テンプレート：**&#x200B;エクスペリエンスフラグメントテンプレートのパスを指定します。エクスペリエンスフラグメントテンプレートがない場合は、[作成します](/help/implementing/developing/extending/experience-fragments.md)。このオプションは、アダプティブフォームを既存のエクスペリエンスフラグメントに追加する場合にのみ使用できます。
   * **フラグメントのタイトル：**&#x200B;エクスペリエンスフラグメントのタイトルを指定します。タイトルは、エクスペリエンスフラグメントを一意に識別します。


## AEM Sites ページまたはエクスペリエンスフラグメント内のフォームの送信アクションを設定する {#configure-submit-action-for-form}

送信アクションを使用すると、アダプティブフォーム経由で取り込んだデータの送信先を選択できます。送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。 アダプティブフォームには、すぐに使用できる送信アクションがいくつか含まれています。 デフォルトの送信アクションを拡張して、独自のカスタム送信アクションを作成することもできます。 フォームの送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/assets/configure-icon.svg)アイコン）をクリックします。送信アクションを設定するための、アダプティブフォームコンテナダイアログボックスが開きます。
   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、アダプティブフォームコンテナコンポーネントのデータモデルを設定します](/help/forms/assets/adaptive-forms-container.png)
1. 必要に応じて、送信アクションを選択して設定します。送信アクションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configuring-submit-actions.md)を参照してください。


## AEM Sites ページまたはエクスペリエンスフラグメント内のフォームに対して、スキーマまたはフォームデータモデル（FDM）を設定する {#configure-schema-or-data-model-for-form}

フォームデータモデル（FDM）を使用してフォームをデータソースに接続し、ユーザーのアクションに基づいてデータを送受信することができます。また、フォームを JSON スキーマに接続して、送信されたデータを事前に定義した形式で受信することもできます。要件に基づいて、次のようにフォームを JSON スキーマまたはフォームデータモデル（FDM）に接続します。

* [JSON スキーマを作成して環境にアップロードする](/help/forms/adaptive-form-json-schema-form-model.md)、または
* [フォームデータモデル（FDM）の作成](/help/forms/create-form-data-models.md)

フォームの JSON スキーマまたはフォームデータモデル（FDM）を設定するには：

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/assets/configure-icon.svg)アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![レンチアイコンをクリックして、アダプティブフォームのデータモデルを設定します](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. 要件に応じて、JSON スキーマまたはフォームデータモデル（FDM）を選択し、設定します。送信アクションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configuring-submit-actions.md)を参照してください。

   * 「**[!UICONTROL フォームモデル]**」オプションを選択する場合は、「**[!UICONTROL フォームデータモデルを選択]**」オプションを使用して、事前設定済みのフォームデータモデル（FDM）を選択します。
   * 「**[!UICONTROL スキーマ]**」オプションを選択する場合は、「**[!UICONTROL スキーマ]**」オプションを使用して、フォームの JSON スキーマを選択します。

1. 「**[!UICONTROL 完了]**」をクリックします。

## AEM Sites ページまたはエクスペリエンスフラグメント内のフォームに事前入力サービスを設定する {#configure-prefill-service-for-form}

事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動入力できます。ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。 次の操作を実行できます。

* [カスタム事前入力サービスを作成](/help/forms/prepopulate-adaptive-form-fields.md)
* [フォームデータモデルの事前入力サービスを使用](#fdm-prefill-service)

### フォームデータモデルの事前入力サービスを使用して、AEM Sites ページまたはエクスペリエンスフラグメント内のフォームのフィールドに事前入力する {#fdm-prefill-service}

フォームデータモデルの事前入力サービスでは、フォームデータモデルまたはカスタム事前入力サービスを使用して、AEM Sites ページまたはエクスペリエンスフラグメント内のアダプティブフォームのフィールドに事前入力できます。フォームデータモデルの事前入力サービスでは、[設定済みのフォームデータモデルのサービスを取得](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)を使用して、データを取得します。アダプティブフォームでフォームデータモデルの事前入力サービスを使用するには、次の手順を実行します。

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/assets/configure-icon.svg)アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![レンチアイコンをクリックしてアダプティブフォームコンテナダイアログボックスを開き、アダプティブフォームコンテナコンポーネントのデータモデルを設定します](/help/forms/assets/adaptive-forms-container.png)
1. フォームデータモデルを選択. 「**[!UICONTROL 基本]**」タブを開きます。事前入力サービスで、「**[!UICONTROL フォームデータモデルの事前入力サービス]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。 これで、アダプティブフォームがフォームデータモデルの事前入力を使用するように設定されました。 [ルールエディター](rule-editor.md)を使用して、フォームのフィールドに事前入力するルールを作成できるようになりました。


## フォーム送信時に、ユーザーをページにリダイレクトする、またはお礼のメッセージを表示する

フォームの送信時に、ユーザーを別の web ページまたはメッセージにリダイレクトできます。 ユーザーをリダイレクトするか、お礼のメッセージを設定するには、次の手順を実行します。

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。

1. 「**[!UICONTROL 送信]**」タブを開きます。

   * リダイレクト URL を設定するには、「送信時」オプションで、 **[!UICONTROL URL にリダイレクト]** 」オプションを選択し、AEM Sitesページを参照して選択するか、外部ページの URL を指定します。
   * カスタムメッセージまたはお礼のメッセージを設定するには、「送信」オプションで「**[!UICONTROL メッセージを表示]**」オプションを選択し、**[!UICONTROL メッセージコンテンツ]**&#x200B;ボックスにメッセージを入力します。 これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。


