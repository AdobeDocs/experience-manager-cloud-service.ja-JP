---
title: ビジュアルコンテンツフラグメント
description: HTML テンプレートを使用して、ビジュアルコンテンツフラグメントを視覚化および公開する方法について説明します。
feature: Content Fragments
role: User, Developer
source-git-commit: 9ad53c41534c552f485a2d57d3c81c270180dfaf
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 0%

---

# ビジュアルコンテンツフラグメント {#visual-content-fragments}

コンテンツフラグメントには、デザインやレイアウトを使用せずにJSON出力を行うための構造化コンテンツが含まれています。 HTML テンプレートを追加すると、HTML形式の構造化されたコンテンツを使用して、完全に装飾された視覚的なエクスペリエンスを作成できます。

* コンテンツフラグメントを視覚化することで、コンテンツの品質保証が可能になり、関係者はコンテンツフラグメントエディターを開かなくても、コンテンツを使用する前にコンテンツを確認できます

* ビジュアルフラグメントを提供することで、オムニチャネル配信を促進し、web、電子メール、モバイルアプリなどのチャネルをまたいでモジュール型のエクスペリエンスを再利用できます。

添付されたAEM テンプレートのレイアウトとデザインを使用するHTML コンテンツフラグメントのレンダリング出力は、*ビジュアルコンテンツフラグメント*&#x200B;と呼ばれます。

<!-- CQDOC-23232 - remove when GA -->

>[!NOTE]
>
>ビジュアルコンテンツフラグメントは現在、限定的でご利用いただけます。
>
>参加を希望される場合は、公式メールアドレスから[experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com)にリクエストを送信してください。

HTMLのテンプレートには、レイアウトやデザインに関する情報が含まれているため、コンテンツフラグメントを視覚化することができます。 テンプレートとコンテンツフラグメント間の接続は、Handlebars構文を使用して、HTML タグをコンテンツフラグメントモデルで定義されたデータタイプ（フィールド）にマッピングするために確立されます。 この定義により、コンテンツフラグメントエディターのそれぞれのフィールドで作成されたコンテンツを、テンプレート内の適切な場所に表示できます。

お客様または開発チームは、[独自のHTML テンプレートを作成してカスタマイズし、[1つ以上をコンテンツフラグメントモデル ](#upload-and-assign-your-template)にアップロードして添付することで、対応するフラグメントをエクスペリエンスにレンダリングできます。[ プレビュー](#preview-your-fragment-with-a-template)および[必要に応じて配信](#deliver-your-visual-content-fragment)。](/help/implementing/developing/extending/content-fragments-visualization-templates.md)

>[!NOTE]
>
>**汎用テンプレート**&#x200B;は、常にAEM内でデフォルトとして使用でき、すべてのモデルに関連付けられます。 このテンプレートを使用すると、構造化されたコンテンツのキーと値のペアを、クリーンで表スタイルのフォーマットで表示して、コンテンツのQuality Assurance（QA）ユースケースをサポートできます。

## テンプレートの作成 {#create-a-template}

Handlebarsを使用して開発されたHTML テンプレートを使用すると、ビジュアルコンテンツフラグメントをHTML形式でプレビューおよび配信できます。 Handlebars.js構文は、コンテンツフラグメントフィールドで作成されるコンテンツのプレースホルダーを定義します。

独自のテンプレートの開発について詳しくは、[ ビジュアルコンテンツフラグメント – テンプレート ](/help/implementing/developing/extending/content-fragments-visualization-templates.md)を参照してください。

## テンプレートのアップロードと割り当て {#upload-and-assign-your-template}

テンプレートはコンテンツフラグメントモデルに関連付けられているため、そのモデルから作成された任意のコンテンツフラグメントで使用できます。

新しいHTML テンプレートをアップロードするには：

1. コンテンツフラグメントコンソールで、**コンテンツフラグメントモデル**&#x200B;のタブを開きます。
1. フラグメントモデルの場所に移動します。
1. 必要なモデルの情報アイコン（i）を選択します。

   ![ コンテンツフラグメントコンソール – 情報アイコン ](/help/sites-cloud/administering/content-fragments/assets/cfc-information-icon.png)

   右側のパネルが表示されます。
1. 下にスクロールして&#x200B;**HTML テンプレート**&#x200B;を表示します。**汎用テンプレート**&#x200B;は既にデフォルトとしてリストされています。

   ![汎用HTML テンプレートを使用したフラグメントのプレビュー](/help/sites-cloud/administering/content-fragments/assets/cf-visual-html-template-configure-default.png)

1. **+**&#x200B;を選択して、HTML ファイル （`.html`）からテンプレートをアップロードします。 ダイアログでは、ローカルファイルシステムを&#x200B;**参照**&#x200B;し、テンプレートファイルを選択できます。
1. アップロードされたテンプレートの2つのビューは、レビュー用に表示されます。

   * 左：コンテンツのないテンプレートのレンダリング
   * 右：AEMに読み込む前にここで編集できるHTML コード

   ![ アップロード時にHTML テンプレートをレビュー](/help/sites-cloud/administering/content-fragments/assets/cf-visual-html-template-upload-review.png)

1. 続行するには、**次へ**&#x200B;を選択してください。
1. AEMで使用する&#x200B;**テンプレート名**&#x200B;を入力します。
1. **テンプレートの作成**&#x200B;を確認します。
1. テンプレートはAEMで作成され、**HTML テンプレート**の下にコンテンツフラグメントモデルのプロパティで一覧表示されます。
読み込みが完了すると、[ フラグメントのプレビュー](#preview-your-fragment-with-a-template)に使用できます。 テンプレートを&#x200B;**[ダウンロード](#download-your-template)**&#x200B;または&#x200B;**[削除](#download-your-template)**&#x200B;することもできます。

## テンプレートを使用したフラグメントのプレビュー {#preview-your-fragment-with-a-template}

テンプレートを使用してコンテンツフラグメントをプレビューするには：

>[!NOTE]
>
>**汎用テンプレート**&#x200B;は常に使用できるため、カスタムテンプレートを読み込まずにフラグメントをプレビューできます。

1. コンテンツフラグメントコンソールで、フラグメントの場所に移動します。

1. 以下のいずれかの操作を行います。
   * コンソールでフラグメントを選択します
   * エディターでフラグメントを開きます

1. 次の一番上のツールバーから&#x200B;**プレビュー**&#x200B;を選択します。

   * コンテンツフラグメントコンソール
   * エディター。ここで&#x200B;**テンプレート**&#x200B;を選択できます

どちらの場合も、新しいモーダルウィンドウが開きます。

1. 利用できるカスタムテンプレートがない場合、AEMは&#x200B;**汎用テンプレート**&#x200B;を使用してフラグメントを表示します。 **汎用テンプレート**:

   * フラグメントのフィールドを表形式で表示します。名前と内容
   * 同じビュー内の参照フラグメントの完全にハイドレートされたコンテンツを表示します

1. カスタムテンプレートが使用可能な場合は、使用するテンプレート（**汎用テンプレート**&#x200B;を含む）を選択できます。

1. コンテンツフラグメントが公開されている場合は、その&#x200B;**プレビューURL**&#x200B;と&#x200B;**公開URL**&#x200B;を表示してコピーすることもできます。

例えば、**汎用テンプレート**&#x200B;でプレビューします。

![汎用HTML テンプレートを使用したフラグメントのプレビュー](/help/sites-cloud/administering/content-fragments/assets/cf-visual-html-template-referenced-fragment.png)

## ビジュアルコンテンツフラグメントを配信し {#deliver-your-visual-content-fragment}

ビジュアルコンテンツフラグメントは、HTML形式で様々なターゲットに配信できます。

### ブラウザーに配信 {#deliver-to-the-browser}

**プレビューURL**&#x200B;または&#x200B;**公開URL**&#x200B;をコピーします。 ブラウザーから直接アクセスして、ビジュアルコンテンツフラグメントを表示できます。

### Edge Delivery Servicesへの配信 {#deliver-to-edge-delivery-services}

ビジュアルフラグメントは、Edge Delivery Service （EDS）ページで配信できます。

1. EDS プロジェクトに移動します。
1. タイプ **[埋め込み](https://sidekick-library--aem-block-collection--adobe.aem.page/tools/sidekick/library.html?plugin=blocks&path=/block-collection/embed&index=0)**&#x200B;の&#x200B;**[ブロック ](https://www.aem.live/developer/block-collection)**&#x200B;を追加またはアクセスします。
1. **公開URL**&#x200B;をブロックに貼り付けます。
1. EDS ページを公開します。 フラグメントのHTML表現が表示されます。

>[!NOTE]
>
>詳しくは、[Edge Delivery Servicesとの統合（埋め込みブロック） ](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#integration-with-edge-services-embed-block)を参照してください

### AEM ページへの配信 {#deliver-to-an-AEM-page}

コアコンポーネントのコンテンツフラグメントを使用すると、AEM ページでビジュアルコンテンツフラグメントを配信できます。

ページ ](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page)で&#x200B;**コンテンツフラグメント** [ コンポーネントを設定する場合：

1. 必要な&#x200B;**コンテンツフラグメント**&#x200B;を指定します。
1. **コンテンツフラグメントのビジュアライゼーション**&#x200B;を選択します。
1. ドロップダウンリストから必要な&#x200B;**ビジュアライゼーションテンプレート**&#x200B;を選択します。

   ![ ビジュアルフラグメントのコンテンツフラグメントコンポーネントの設定](/help/sites-cloud/administering/content-fragments/assets/cf-visual-template-aem-page.png)

1. ビジュアルフラグメントがページに表示されます。

>[!NOTE]
>
>詳しくは、[統合 – コアコンポーネントを含むAEM Sites](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#integration-aem-sites-with-core-components)を参照してください

## テンプレートをダウンロード {#download-your-template}

AEMからHTML テンプレートをダウンロードするには：

1. コンテンツフラグメントコンソールで、**コンテンツフラグメントモデル**&#x200B;のタブを開きます。
1. フラグメントモデルの場所に移動します。
1. 必要なモデルの情報アイコン（i）を選択します。

   ![ コンテンツフラグメントコンソール – 情報アイコン ](/help/sites-cloud/administering/content-fragments/assets/cfc-information-icon.png)

   右側のパネルが表示されます。

1. 下にスクロールして&#x200B;**HTML テンプレート**&#x200B;を表示します。
1. ダウンロードするテンプレートで楕円形を選択します。
1. 「**ダウンロード**」を選択します。
1. ファイル名と場所を指定します。
1. **保存**&#x200B;で確認します。

## テンプレートを削除 {#delete-your-template}

（AEMから）新しいHTML テンプレートを削除するには：

1. コンテンツフラグメントコンソールで、**コンテンツフラグメントモデル**&#x200B;のタブを開きます。
1. フラグメントモデルの場所に移動します。
1. 必要なモデルの情報アイコン（i）を選択します。

   ![ コンテンツフラグメントコンソール – 情報アイコン ](/help/sites-cloud/administering/content-fragments/assets/cfc-information-icon.png)

   右側のパネルが表示されます。
1. 下にスクロールして&#x200B;**HTML テンプレート**&#x200B;を表示します。
1. ダウンロードするテンプレートで楕円形を選択します。
1. 「**削除**」を選択します。
1. 次のダイアログで、**削除**&#x200B;でアクションを確認します。
