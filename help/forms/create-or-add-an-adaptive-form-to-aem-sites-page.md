---
title: アダプティブフォームを作成するか、AEM Sitesページに追加する
description: アダプティブフォームを容易に作成したり、シームレスにAEM Sitesページに追加したりする方法を学びます。 動的でカスタマイズ可能なフォームを Web サイトに統合し、デジタルエクスペリエンスを最適化して最大限の効果を得るための、順を追った手法とベストプラクティスについて説明します。
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---


# アダプティブフォームを作成するか、AEM Sitesページに追加する {#create-or-add-an-adaptive-form-to-aem-sites-page}

AEM Formsを使用すれば、アダプティブフォームを Web ページにシームレスに組み込むことができます。 これにより、訪問者は、ページを離れることなく、フォームに簡単に入力して送信できます。 これにより、Web サイト上の他の要素とのやり取りを容易に行いながら、フォームを積極的に操作することができます。

次のオプションを使用すると、この機能を最大限に活用できます。

* **カスタムフォームの追加：** 要件やデザインの好みに合わせてカスタマイズし、新規フォームをゼロから作成します。

* **エクスペリエンスフラグメントの拡張：** AEMエクスペリエンスフラグメントにフォームを追加して、フォームのリーチを拡張し、複数のページやサイトでシームレスに再利用できます。

* **承認済みテンプレートを利用：** 事前に承認されたテンプレートを活用して、組織のブランディングガイドラインやデザイン標準に合ったフォームをすばやく作成できます。

* **既存のフォームの追加：** 作成済みのフォームを Web サイトに簡単に統合し、訪問者が直接操作できるようにします。

* **複数のフォームを追加：**  複数のフォームをページに追加して、ユーザーの環境設定や要件に基づいて複数のフォームをユーザーに提供します。 新規フォームと既存フォームを組み合わせることができます。

AEM Sitesエディターを使用すると、複数のフォームをすばやく作成してAEM Sitesページに追加できます。 AEM Sitesエディターを使用すると、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームのコンポーネントを活用して、Sites ページ内にシームレスなデータ取得エクスペリエンスを作成できます。 また、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sitesページの様々な機能を使用できます。

## 目的

* AEM Sitesエディターとエクスペリエンスフラグメントを使用してアダプティブフォームを作成する方法を説明します
* AEM Sitesページに追加されたアダプティブフォームのレイアウトとテーマを設定する方法と、
* AEM Sitesエディターとエクスペリエンスフラグメントを使用してアダプティブフォームを作成する


## 検討事項 {#consideration}

AEM FormsにはアダプティブフォームコンテナとアダプティブForms — 埋め込みコンポーネントが用意されています。 アダプティブフォームコンテナを使用して、エクスペリエンスフラグメントまたはAEM Sitesページに新しいフォームを作成および追加できます。アダプティブForms — 埋め込みコンポーネントでは、既存のアダプティブフォームを追加したり、Adaptive Formsエディターを使用して新しいフォームを作成できます。

アダプティブフォームコンテナを使用してフォームを作成または追加する場合、フォームはAEM Sites翻訳フローを通じて翻訳およびローカライゼーションされます。 言語ごとに、サイトページと対応するフォームの個別のコピー（言語コピー）が生成され、コンテンツ作成者が親ページのフォームのルールを変更する場合は、フォームのすべての言語コピーで同じ変更を行う必要があります。 アダプティブフォームコンテナでは、AEM Sitesページの様々な機能（バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど）を使用できます。

アダプティブフォームの埋め込みコンポーネントを使用してフォームを作成または追加する場合、そのフォームはAEM Formsの翻訳フローを使用して翻訳およびローカライゼーションされます。 この場合、1 つのフォームが維持され、Sites ページのすべての言語コピーで参照されます。 アダプティブフォーム埋め込みコンポーネントでは、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sitesページの様々な機能にアクセスできません。


## 事前準備 {#before-you-start}

+++  環境でのアダプティブFormsコアコンポーネントの有効化

次を確認します。 [アダプティブFormsコアコンポーネントがAEM Formsas a Cloud Service環境で有効になっている](enable-adaptive-forms-core-components.md).

+++

+++ 有効にする**[!UICONTROL アダプティブFormsコンテナ]

有効にするには [!UICONTROL アダプティブFormsコンテナ] テンプレートのポリシーのコンポーネントで、次の手順を実行します。

1. 編集するAEM Sitesページを開きます。 ページを編集用に開くには、ページを選択して「編集」をクリックします。
1. サイトページのテンプレートを開きます。 テンプレートを開くには、 [!UICONTROL ページ情報] ![ページ情報](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL テンプレートを編集]. 対応するテンプレートがテンプレートエディターで開きます。
1. 構造ビューで、 **[!UICONTROL ポリシー]** ![ポリシー](/help/forms/assets/Smock_FeedManagement_18_N.svg) アイコンをクリックします。 内 **[!UICONTROL 許可されたコンポーネント]** リストを表示し、 **[!UICONTROL アダプティブFormsコンテナ]**  の下のチェックボックス **[AEM Archetype プロジェクト名]  — アダプティブフォーム**.
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++


+++  AEM SitesページへのアダプティブFormsクライアントライブラリの追加

アダプティブFormsコンテナコンポーネントの完全な機能を有効にするには、デプロイメントパイプラインを使用して、Customheaderlibs および Customfooterlibs クライアントライブラリをAEM Sitesページに追加します。 ライブラリを追加するには：

1. にアクセスしてクローンを作成 [AEM Cloud Service Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. プランテキストエディターでAEM Cloud Service Git リポジトリフォルダーを開きます。 ( 例：Microsoft Visual Code)。
1. を開きます。 `ui.apps/src/main/content/jcr_root/apps/[your-project]/components/page/.content.xml` ファイルを編集し、 `sling:resourceSuperType`. 例えば、 `core/wcm/components/page/v3/page`.


   ![sling リソース](/help/forms/assets/slingresource.png)

1. に移動します。 `  ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\` `ui.apps/src/main/content/jcr_root/apps` 前の手順で説明した値と同じフォルダ構造を作成します。 例えば、値が前の手順の例と似ている場合、最終的なノード構造は次のようになります。 `ui.apps/src/main/content/jcr_root/apps/core/wcm/components/page/v3/page`

   ![オーバーレイ構造](/help/forms/assets/overlaystructure.png)

1. 作成 `customheaderlibs.html` および `customfooterlibs.html` 前の手順で作成したノード構造にあるファイルを次の内容で追加します。

   ```
        //Customheaderlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
        </sly> 
   
        //customfooterlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
        </sly> 
   ```

1. [デプロイメントパイプラインの実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) クライアントライブラリをAEM as a Cloud Service環境にデプロイする場合。

+++

## アダプティブフォームの作成 {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

新しいフォームを最初から作成し、要件やデザインの環境設定に合わせて、AEMのサイトページまたはエクスペリエンスフラグメント内で直接新しいフォームを作成できます。 単一使用フォームの場合は、AEMサイトページへの直接オーサリングをお勧めします。エクスペリエンスフラグメントは、Web サイトの複数のページで再利用する必要があるフォームに最適です。

* [AEM Sitesページでのフォームの作成](#create-an-adaptive-form-in-sites-editor)
* [エクスペリエンスフラグメント内にフォームを作成する](#create-an-adaptive-form-in-experience-fragment)

### AEM Sitesページでのフォームの作成 {#create-an-adaptive-form-in-sites-editor}

AEM Sitesエディターでアダプティブフォームコンテナコンポーネントを使用して、カスタムフォームを作成することができます。 このコンポーネントを使用すると、フォームコンポーネントをドラッグ&amp;ドロップしてフォームを作成できます。 フォームコンポーネントは、コアコンポーネントに基づいています。 これらは、組織の要件に応じて簡単にカスタマイズできます。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Sites ページでアダプティブフォームを作成するには：

1. AEM Sitesページを編集モードで開きます。
1. 次をドラッグ&amp;ドロップ： **[!UICONTROL アダプティブFormsコンテナ]** コンポーネントをコンポーネントブラウザーからサイトページに移動します。 ページ上にフォーム用のスペースが作成されます。 レイアウトモードを使用して、コンテナスペースのサイズを変更できます。
1. アダプティブフォームのコアコンポーネントをコンテナスペースにドラッグ&amp;ドロップしてフォームを作成します。
1. 「送信」ボタンを追加します。

次に、送信アクションと詳細プロパティを設定します。

### エクスペリエンスフラグメント内にフォームを作成する {#create-an-adaptive-form-in-experience-fragment}

フォームをAEMエクスペリエンスフラグメントに追加することで、フォームのリーチを拡大して、複数のページやサイトでシームレスに再利用できます。 例えば、エクスペリエンスフラグメント内にニュースレターのサインアップフォームを含めることができます。 これにより、Web サイトの複数のページでフラグメントを簡単に再利用できるので、フォームを繰り返し再作成する必要がなくなります。 エクスペリエンスフラグメント内のニュースレターサインアップフォームに加えられた更新や変更は、その更新が使用されるすべてのページに自動的に反映されます。 これにより、プロセスが合理化され、シームレスなユーザーエクスペリエンスを確保しながら、Web サイトのフォームの管理をシンプル化します。

エクスペリエンスフラグメント内にアダプティブフォームを作成するには：

## アダプティブフォームのレイアウトの変更 {#change-layout-of-an-adaptive-form}

AEM Sitesページで、 [レイアウトモード](/help/sites-cloud/authoring/features/responsive-layout.md) AEM Sitesページに追加されているアダプティブフォームコンテナコンポーネントのサイズを変更する場合。
