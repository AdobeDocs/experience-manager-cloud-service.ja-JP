---
title: コアコンポーネントに基づいてアダプティブフォームに新しいロケールのサポートを追加するには、どうすればよいですか？
description: AEM Forms は、アダプティブフォームのローカライズ用に新しくロケールを追加できます。
source-git-commit: 0a1310290c25a94ffe6f95ea6403105475ef5dda
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 33%

---

# コアコンポーネントに基づくアダプティブFormsのロケールの追加 {#supporting-new-locales-for-adaptive-forms-localization}


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| 基盤コンポーネント | [ここをクリックしてください](supporting-new-language-localization.md) |
| コアコンポーネント | この記事 |

AEM Forms が標準でサポートしているロケールは、英語（en）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ドイツ語（de）、日本語（ja）、ブラジルポルトガル語（pt-br）、中国語（zh-tn）、台湾中国語（zh-tw）、韓国語（ko-kr）です。

その他のロケール（ヒンディー語（hi_IN）など）のサポートを追加することもできます。

<!-- 
## Understanding locale dictionaries {#about-locale-dictionaries}

The localization of adaptive forms relies on two types of locale dictionaries:

*   **Form-specific dictionary** Contains strings used in adaptive forms. For example, labels, field names, error messages, help descriptions. It is managed as a set of XLIFF files for each locale and you can access it at `[AEM Forms as a Cloud Service Author instance]/libs/cq/i18n/gui/translator.html`.

*   **Global dictionaries** There are two global dictionaries, managed as JSON objects, in AEM client library. These dictionaries contain default error messages, month names, currency symbols, date and time patterns, and so on.  These locations contain separate folders for each locale. Because global dictionaries are not updated frequently, keeping separate JavaScript files for each locale enables browsers to cache them and reduce network bandwidth usage when accessing different adaptive forms on same server.

-->

## 前提条件 {#prerequistes}

新しいロケールのサポートを追加する前に、

* 編集を容易にするために、プレーンテキストエディター (IDE) をインストールします。 このドキュメントの例は、Microsoft VS Code に基づいています。
* アダプティブFormsコアコンポーネントリポジトリーのクローンを作成します。 リポジトリのクローンを作成するには：
   1. コマンドラインまたはターミナルウィンドウを開き、リポジトリを保存する場所に移動します。 例：`/adaptive-forms-core-components`
   1. 次のコマンドを実行して、リポジトリのクローンを作成します。

      ```SHELL
          git clone https://github.com/adobe/aem-core-forms-components.git
      ```

  リポジトリには、ロケールの追加に必要なクライアントライブラリが含まれます。


## ロケールを追加 {#add-localization-support-for-non-supported-locales}

新しいロケールのサポートを追加するには、次の手順に従います。

![ロケールをリポジトリに追加する](add-a-locale-adaptive-form-core-components.png)

### AEMas a Cloud ServiceGit リポジトリのクローン {#clone-the-repository}

1. コマンドラインを開き、リポジトリを保存するディレクトリ（例： ）を選択します。 `/cloud-service-repository/`.

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/
   ```

   置換 `<my-org>` および `<my-program>` 上記の URL に、組織名とプログラム名を入力します。 組織名、プログラム名、または Git リポジトリの完全パスと、リポジトリのクローンに必要な資格情報を取得する詳しい手順については、 [Git へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 記事。

   コマンドが正常に完了した後、フォルダ `<my-program>` が作成されました。 Git リポジトリから複製されたコンテンツが含まれます。 記事の残りの部分では、フォルダーは次のようにレファリングされます。 `[AEM Forms as a Cloud Service Git repostory]`.


### 新しいロケールを Guide Localization Service に追加する {#add-a-locale-to-the-guide-localization-service}

1. 前の節で複製したリポジトリフォルダーを、プレーンテキストエディターで開きます。
1. `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config` フォルダーに移動します。次の項目が見つかります。 `<appid>` （内） `archetype.properties` プロジェクトのファイル。
1. `[AEM Forms as a Cloud Service Git repostory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config/Guide Localization Service.cfg.json` ファイルを編集用として開きます。ファイルが存在しない場合は作成します。 サポートされているロケールを含むサンプルファイルは、次のようになります。

   ![Guide Localization Service.cfg.json のサンプル](locales.png)

1. 次を追加： [言語のロケールコード](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 例えば、ヒンディー語に「hi」を追加しようとしています。
1. ファイルを保存して閉じます。

### クライアントライブラリを作成してロケールを追加する

AEM Formsには、新しいロケールを簡単に追加できるサンプルのクライアントライブラリが用意されています。 をダウンロードして、 `clientlib-it-custom-locale` GitHub のアダプティブFormsコアコンポーネントリポジトリーからForms as a Cloud Serviceリポジトリーへのクライアントライブラリ。 クライアントライブラリを追加するには、次の手順に従います。

1. プレーンテキストエディターでアダプティブFormsコアコンポーネントリポジトリを開きます。 リポジトリを複製しない場合は、 [前提条件](#prerequistes) を参照してください。
1. `/aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs` ディレクトリに移動します。
1. をコピーします。 `clientlib-it-custom-locale` ディレクトリ。
1. に移動します。 `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/moonlightprodprogram/clientlibs` をクリックし、 `clientlib-it-custom-locale` ディレクトリ。


### ロケール固有のファイルの作成 {#locale-specific-file}

1. `[AEM Forms as a Cloud Service Git repostory]/ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/` に移動します。
1. 次を見つけます。 [GitHub の英語ロケール.json ファイル](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json)：製品に含まれるデフォルトの文字列の最新セットが含まれます。
1. 特定のロケール用の新しい.json ファイルを作成します。
1. 新しく作成した.json ファイルで、英語のロケールファイルの構造を反映します。
1. .json ファイル内の英語の文字列を、対応するローカライズされた言語の文字列に置き換えます。
1. ファイルを保存して閉じます。


### 辞書にロケールサポートを追加する {#add-locale-support-for-the-dictionary}

追加する `<locale>` が、`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` 以外の場合にのみ、この手順を実行してください。

1. `[AEM Forms as a Cloud Service Git repostory]/ui.content/src/main/content/jcr_root/etc/` フォルダーに移動します。

1. の作成 `etc` フォルダーの下に `jcr_root` フォルダー（存在しない場合）。

1. フォルダーの作成 `languages` の下に `etc` フォルダー（存在しない場合）。

   ![代替テキスト](etc-content-xml.png)

1. の作成 `.content.xml` 下のファイル `languages` フォルダー。 ファイルに次のコンテンツを追加します。

   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr]"/>
   ```

1. ロケールコードを `languages` プロパティ。 例えば、以下のコード例では、hindi の hi を追加しています。


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
   jcr:primaryType="nt:unstructured"
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

1. 新しく作成したフォルダーを `filter.xml` under `/ui.content/src/main/content/meta-inf/vault/filter.xml` 形式：

   ```
   <filter root="/etc/languages"/>
   ```

   ![新しく作成したフォルダーを `filter.xml` under `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

### 変更をコミットし、パイプラインをデプロイします。 {#commit-changes-in-repo-deploy-pipeline}

新しいロケールサポートを追加した後、変更を Git リポジトリにコミットします。 フルスタックパイプラインを使用してコードをデプロイします。 [パイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)を学び、新しいロケールのサポートを追加します。

パイプラインの実行が成功すると、新しく追加されたロケールを使用する準備が整います。

## 新しく追加されたロケールでアダプティブフォームをプレビューする {#use-added-locale-in-af}

新しく追加されたロケールでアダプティブフォームをプレビューするには、次の手順を実行します。

1. AEM Forms as a Cloud Serviceインスタンスにログインします。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。
1. アダプティブフォームを選択し、「**辞書を追加**」をクリックすると、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードが表示されます。
1. **プロジェクトタイトル**&#x200B;を指定し、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードのドロップダウンメニューから「**ターゲット言語**」を選択します。
1. 「**完了**」をクリックし、作成した翻訳プロジェクトを実行します。
1. アダプティブフォームを選択し、「**HTML としてプレビュー**」をクリックします。
1. アダプティブフォームの URL に `&afAcceptLang=<locale-name>` を追加します。
1. ページを更新すると、アダプティブフォームは指定されたロケールでレンダリングされます。

アダプティブフォームのロケールを識別する方法は 2 つあります。アダプティブフォームがレンダリングされると、リクエストされたロケールが次のように識別されます。

* アダプティブフォームの URL の `[local]` セレクターを取得します。URL の形式は、`http:/[AEM Forms Server URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled` です。`[local]` セレクターを使用すると、アダプティブフォームをキャッシュできます。

* 次のパラメーターをリスト順に取得します。

   * リクエストパラメーター `afAcceptLang`
ユーザーのブラウザーロケールを上書きするには、 `afAcceptLang` リクエストパラメーターを使用して、ロケールを強制的に指定します。 例えば、次の URL はフォームをカナダのフランス語ロケールで強制的にレンダリングします。
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * ユーザー向けに設定されるブラウザーのロケールです。これは、`Accept-Language` ヘッダーを使用したリクエストで指定されます。

要求されたロケールのクライアントライブラリが存在しない場合は、ロケールに存在する言語コードがクライアントライブラリにないかを確認します。 例えば、要求されたロケールが `en_ZA` （南アフリカ英語）と `en_ZA` が存在しない場合、アダプティブフォームは次の目的でクライアントライブラリを使用します： `en` （英語）言語（存在する場合）。 ただし、どちらも存在しない場合、アダプティブフォームでは `en` ロケールの辞書が使用されます。

ロケールが識別されると、アダプティブフォームはフォーム固有の辞書を選択します。リクエストされたロケールのフォーム固有の辞書が見つからない場合は、アダプティブフォームが作成された言語の辞書が使用されます。

使用可能なロケール情報がない場合、アダプティブフォームは、フォーム開発時に使用された言語で元の言語で表示されます。

<!--
Get [sample client library](/help/forms/assets/locale-support-sample.zip) to add support for new locale. You need to change the content of the folder in the required locale.

## Best Practices to support for new localization {#best-practices}

*   Adobe recommends creating a translation project after creating an Adaptive Form.

*   When new fields are added in an existing Adaptive Form:
    * **For machine translation**: Re-create the dictionary and run the translation project. Fields added to an Adaptive Form after creating a translation project remain untranslated. 
    * **For human translation**: Export the dictionary through `[server:port]/libs/cq/i18n/gui/translator.html`. Update the dictionary for the newly added fields and upload it.
-->
