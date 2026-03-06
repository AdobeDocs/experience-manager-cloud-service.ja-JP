---
title: AEM Sites テーマへのアダプティブ Forms テーマの埋め込み
description: アダプティブFormsのテーマ（キャンバスなど）をAEM Sitesのテーマに統合して、Sites ページや埋め込まれたアダプティブFormsが統一されたテーマとデプロイメントを共有できるようにする方法を説明します。
keywords: アダプティブフォームのテーマ，サイトテーマ，AEM Sites テーマ，フォームテーマの統合，フロントエンドパイプライン，テーマの埋め込み
feature: Adaptive Forms, Core Components
role: Developer
exl-id: 0607e11c-84d2-42cb-be9f-acd7c328a342
source-git-commit: 343fc4fdc9b2947ff7771e3b74e77c679cf5c204
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 1%

---

# AEM Sites テーマへのアダプティブ Forms テーマの埋め込み

アダプティブ Forms テーマ（[AEM Forms キャンバステーマ ](https://github.com/adobe/aem-forms-theme-canvas) など）をAEM Sites テーマに埋め込むことができます。 これにより、1 つのテーマを使用して、[Forms フロントエンドパイプライン ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html) を介した 1 つのビルドと 1 つのデプロイメントで、サイトページとそれらのページに埋め込まれたアダプティブAEMの両方を駆動できます。

この記事は、標準（またはカスタム）のForms テーマを管理またはカスタマイズし、個別のAEM Sites テーマのデプロイメントを管理せずに、アダプティブフォームのスタイル設定を含める開発者向けです。

## 前提条件 {#prerequisites}

開始する前に、次のことを確認します。

* サイトテーマ用に設定された **フロントエンドパイプライン** を持つ [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)。
* **サイトテーマのソース** – 例えば、[ 標準サイトテンプレートテーマ ](https://github.com/adobe/aem-site-template-standard) （`theme/` や `src/theme.scss` などの `src/components/` を含んだリポジトリ）です。
* **Forms テーマソース** - [AEM Forms キャンバステーマ ](https://github.com/adobe/aem-forms-theme-canvas) （または別の互換性のあるアダプティブFormsテーマ）がローカルでクローンまたはダウンロードされました。
* **Node.js および npm** - サイトテーマを作成します（サポートされているバージョンについては、テーマの README を参照してください）。
* **Maven** – 完全なサイトテンプレートパッケージをビルドする場合（テーマのみの作業の場合はオプション）。

>[!NOTE]
>
>**テーマ名：** Forms テーマをサイトテーマに埋め込み、フロントエンドパイプラインを介してデプロイする場合、**テーマ名を変更する必要はありません**。 フォームスタイルは、現在の名前で構築およびデプロイされる既存のサイトテーマの一部になります。 テーマ名の変更（`package.json` など）が必要になるのは、専用のテーマリポジトリーから **スタンドアロン** Forms テーマをデプロイする場合のみです。そのシナリオについては、[ テーマを使用したコアコンポーネントベースのアダプティブFormsのスタイル設定 ](/help/forms/using-themes-in-core-components.md) を参照してください。

## 手順 1：アダプティブフォームコンポーネントフォルダーを作成する {#step-1-create-folder}

サイトテーマリポジトリで、Forms テーマが格納されるフォルダーを作成します。

```text
theme/src/components/adaptiveform/
```

すべてのForms テーマのアセットはこのフォルダーの下に配置されるので、既存のサイトコンポーネントとは別に配置されます。

## 手順 2:Formsのテーマコンポーネントと画像をコピーする {#step-2-copy-components-and-images}

**Forms テーマ** （例：`aem-forms-theme-canvas`）および **サイトテーマ** のパスを使用：

1. **コンポーネントフォルダーをコピー**\
   Formsのテーマから、`src/components/` のコンテンツ全体を次のようにサイトテーマにコピーします。

   ```text
   theme/src/components/adaptiveform/
   ```

   次のようなパスが得られます。

   ```text
   theme/src/components/adaptiveform/button/
   theme/src/components/adaptiveform/checkbox/
   theme/src/components/adaptiveform/container/
   … (one folder per component)
   ```

   ![ アダプティブフォームコンポーネントの追加 ](/help/forms/assets/theme-add-adaptiveform-component.png)

2. **画像をコピー**\
   Formsのテーマの画像をサイトテーマにコピーします。

   ```text
   Forms theme:  src/resources/images/*
   Site theme:   theme/src/components/adaptiveform/resources/images/
   ```

   存在しない場合 `theme/src/components/adaptiveform/resources/images/` 作成し、すべての画像アセット（`question.svg`、`Chevron-Left.svg`、`busy-state.gif` など）をコピーします。

   ![ 画像を追加 ](/help/forms/assets/theme-add-images.png)

## 手順 3：変数と Mixin のコピー {#step-3-copy-variables-and-mixins}

Forms テーマは、`src/site/` の下で共有変数と Mixin を使用します。 これら 2 つのファイルのみを **の** ルート `adaptiveform/` にコピーします（`site` サブフォルダー内にはコピーしません）。

| Source（Forms テーマ） | 宛先（サイトテーマ） |
|---------------------------|---------------------------------------------------|
| `src/site/_variables.scss` | `theme/src/components/adaptiveform/_variables.scss` |
| `src/site/_mixin.scss` | `theme/src/components/adaptiveform/_mixin.scss` |

残りのForms テーマの **フォルダーはコピーしない** ください `src/site/` 埋め込まれたフォームスタイルに必要なのは、これら 2 つのファイルのみです。

![ 変数と Mixin の追加 ](/help/forms/assets/theme-add-mixin-variable.png)

## 手順 4:SCSS での画像パスの修正 {#step-4-fix-image-paths}

Formsのテーマでは、コンポーネントの SCSS ファイルが、`./resources/` や `url(resources/` などのパスを持つ画像を参照することがよくあります。 サイトテーマにコピーした後、これらのパスは `theme/src/components/adaptiveform/resources/images/` を指す必要があります。

**標準のサイト テンプレート テーマ** では、`url()` からパスを解決する区画 `theme/src/` 使用します。 そのため、画像が `theme/src/components/adaptiveform/resources/images/` にある場合は、（**`components/adaptiveform/resources/images/`** に対する）パス `theme/src/` を使用します。

**検索と置換** を `.scss` の下のすべての `theme/src/components/adaptiveform/` で行います。

| 検索 | 置換文字列 |
|------|------------------|
| `./resources/` | `components/adaptiveform/resources/` |
| `url(resources/` | `url(components/adaptiveform/resources/` |
| `url('resources/` | `url('components/adaptiveform/resources/` |
| `url(../resources/` | `url(components/adaptiveform/resources/` |

**例** – 前（Forms テーマ）:

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(./resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

**後** （サイトテーマ、`adaptiveform/resources/images/` の画像）:

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(components/adaptiveform/resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

![ 画像の変更 URL](/help/forms/assets/theme-change-url.png)

画像（ボタン、アコーディオン、ウィザード、コンテナ、手書きなど）を参照する `adaptiveform/` の下のすべての SCSS ファイルに対して繰り返します。 IDE で `theme/src/components/adaptiveform/` を介してプロジェクト全体で検索/置換を行うことをお勧めします。

## 手順 5：アダプティブフォームのエントリポイント SCSS の作成 {#step-5-create-adaptiveform-scss}

サイトテーマに **`theme/src/components/adaptiveform/_adaptiveform.scss`** を作成します。 このファイルは次の条件を満たす必要があります。

1. 共有変数と Mixin を読み込みます。
2. 各アダプティブフォームコンポーネントのメイン SCSS ファイルを読み込みます。

以下を完全なエントリポイントとして使用します（すべてのコアコンポーネントベースのフォームコンポーネントとの標準統合に一致します）。

```scss
//== Adaptive Form components (forms theme integration)
// Variables and mixins for adaptive form components
@import 'variables';
@import 'mixin';

//== Core adaptive form components
@import './button/_button.scss';
@import './checkboxgroup/_checkboxgroup.scss';
@import './container/_container.scss';
@import './datepicker/_datepicker.scss';
@import './dropdown/_dropdown.scss';
@import './fileinput/_fileinput.scss';
@import './footer/_footer.scss';
@import './image/_image.scss';
@import './numberinput/_numberinput.scss';
@import './panelcontainer/_panelcontainer.scss';
@import './radiobutton/_radiobutton.scss';
@import './text/_text.scss';
@import './textinput/_textinput.scss';
@import './accordion/_accordion.scss';
@import './tabsontop/_tabsontop.scss';
@import './pageheader/_pageheader.scss';
@import './wizard/_wizard.scss';
@import './title/_title.scss';
@import './telephoneinput/_telephoneinput.scss';
@import './emailinput/_emailinput.scss';
@import './recaptcha/_recaptcha.scss';
@import './verticaltabs/_verticaltabs.scss';
@import './checkbox/_checkbox.scss';
@import './termsandconditions/_termsandconditions.scss';
@import './switch/_switch.scss';
@import './hcaptcha/_hcaptcha.scss';
@import './turnstile/_turnstile.scss';
@import './review/_review.scss';
@import './scribble/_scribble.scss';
@import './datetime/_datetime.scss';
```

![ アダプティブフォーム scss](/help/forms/assets/theme-adaptive-form-scss.png)

Forms テーマで一部のコンポーネント（手書きメモや captcha など）が省略された場合は、ビルドエラーを避けるために、対応する `@import` 行を削除またはコメントアウトします。 上記のリストは [ キャンバステーマ ](https://github.com/adobe/aem-forms-theme-canvas) 構造と一致します。

## 手順 6：サイトテーマにアダプティブフォームテーマを読み込む {#step-6-import-in-theme-scss}

ま **`theme/src/theme.scss`**、ファイルの **最後** に（他のコンポーネントの読み込みの後に）単一の読み込みを追加します。

```scss
//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

**例** - `theme.scss` 末：

```scss
// ... existing site component imports ...
@import './components/embed/_embed.scss';
@import './components/pdfviewer/_pdfviewer.scss';
@import './components/socialmediasharing/_social_media_sharing.scss';

//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

![ アダプティブフォームの scss を追加 ](/help/forms/assets/theme-add-adaptive-form-scss-theme.png)

これは既存のサイトテーマ構造に必要な唯一の変更です。フォーム固有のコードはすべて `src/components/adaptiveform/` 下に置かれます。

## 手順 7：ビルドとデプロイ {#step-7-build-and-deploy}

1. テーマルートからサイトテーマを作成します。

   ```bash
   cd theme
   npm install
   npm run build
   ```

   ![ ビルドの実行 ](/help/forms/assets/theme-mpm-run-build.png)

2. 既存の [ フロントエンドパイプライン ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html) を介してデプロイします。 デプロイ後は、同じテーマ CSS がサイトページと埋め込みアダプティブFormsの両方に適用されます。

## トラブルシューティング {#troubleshooting}

| 問題 | チェック対象 |
|-------|-------------------------------|
| ビルド失敗：イメージの「ファイルが見つかりません」 | すべてのフォーム画像が `theme/src/components/adaptiveform/resources/images/` に表示されていることを確認します。 `.scss` の下のすべての `adaptiveform/` で、パスが `url(components/adaptiveform/resources/images/...)` から解決されるように `theme/src/` を使用します（パーセルを使用した標準のサイトテーマビルドで必要）。 バンドラーがファイルごとにパスを解決しない限り、`../resources/` または `resources/` を単独で使用しないでください。その後、画像フォルダーに一致するパスを使用します。 |
| ビルドに失敗します：`_variables.scss` または `_mixin.scss` の「ファイルが見つかりません」 | 両方のファイルをForms テーマの `src/site/` から `theme/src/components/adaptiveform/` （アダプティブフォームのルート）に、`site` サブフォルダー内ではなくコピーします。 |
| ビルド失敗：コンポーネントの「ファイルが見つかりません」（例：`_scribble.scss`） | Formsのテーマに、そのコンポーネントが含まれていない場合があります。 ま `theme/src/components/adaptiveform/_adaptiveform.scss`、そのコンポーネントの `@import` 行を削除またはコメントアウトします。 |
| フォームはレンダリングされますが、スタイルはありません | ページで、構築されたテーマ CSS を含むクライアントライブラリを使用し、その `theme.scss` に `@import './components/adaptiveform/_adaptiveform.scss';` 行を含み、テーマが再構築およびデプロイされたことを確認します。 |
| サイトとフォームのコンポーネントでスタイルが競合しています | フォームコンポーネントクラスは名前空間が使用されます（例：`cmp-adaptiveform-button`）。 クラッシュが発生した場合は、カスタムサイト CSS がそれらのクラスをオーバーライドするかどうかを調べ、個別の設定または順序を調整します。 |

## 関連トピック {#see-also}

* [テーマを使用して、コアコンポーネントベースのアダプティブFormsのスタイルを設定します](/help/forms/using-themes-in-core-components.md)
* [ フロントエンドパイプラインを使用した開発 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)
