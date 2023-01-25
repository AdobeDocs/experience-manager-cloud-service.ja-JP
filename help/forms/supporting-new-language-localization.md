---
title: アダプティブフォームのローカリゼーション用に新しいロケールをサポート
seo-title: Supporting new locales for adaptive forms localization
description: AEM Formsでは、アダプティブフォームのローカライズ用に新しいロケールを追加できます。 英語 (en)、スペイン語 (es)、フランス語 (fr)、イタリア語 (it)、ドイツ語 (de)、日本語 (ja)、ポルトガル語 — ブラジル語 (pt-BR)、中国語 (zh-TW)、韓国語 (ko-KR) のロケールです。
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
source-git-commit: f8bbc6605e77cf2858c69dae96e9ab32698d1f16
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 34%

---

# アダプティブフォームのローカライゼーション用に新しいロケールをサポート{#supporting-new-locales-for-adaptive-forms-localization}

## ロケールの辞書について {#about-locale-dictionaries}

アダプティブフォームのローカリゼーションは、次の 2 種類のロケールの辞書に基づいています。

* **フォーム固有の辞書**&#x200B;は、アダプティブフォーム使用する文字列を含みます。例えば、ラベル、フィールド名、エラーメッセージ、ヘルプの説明文などです。各ロケールごとに、XLIFF ファイルのセットの形で管理されています。`[author-instance]/libs/cq/i18n/gui/translator.html` からアクセスできます。

* **グローバル辞書** 2 つのグローバル辞書があり、AEM クライアントライブラリで JSON オブジェクトの形で管理されています。これらの辞書にはデフォルトのエラーメッセージ、12 か月の名前、通貨シンボル、日付と時間のパターンなどが含まれます。これらの辞書は、 `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. これらの場所には、ロケールごとに別々のフォルダーが含まれます。 グローバル辞書は頻繁に更新されないので、各ロケールで別々の JavaScript ファイルを保持することで、同じサーバー上の異なるアダプティブフォームにアクセスする際にブラウザーがそれらをキャッシュし、ネットワーク帯域幅の使用量を削減できます。

AEM Formsの新しいローカライゼーションをサポートする手順：

1. [サポートされていないロケールにローカリゼーションのサポートを追加する](#add-localization-support-for-non-supported-locales-add-localization-support-for-non-supported-locales)
1. [Adaptive Formsで追加されたロケールを使用する](#use-added-locale-in-adaptive-forms-use-added-locale-in-af)

## サポートされていないロケールにローカリゼーションのサポートを追加する {#add-localization-support-for-non-supported-locales}

AEM Formsでは現在、アダプティブFormsコンテンツのローカライゼーションを英語 (en)、スペイン語 (es)、フランス語 (fr)、イタリア語 (it)、ドイツ語 (de)、日本語 (ja)、ポルトガル語 — ブラジル語 (pt-BR)、中国語 (zh-TW)、韓国語 (ko-KR) のロケールでサポートしています。

アダプティブフォーム実行時に新しいロケールのサポートを追加するには、次を参照してください。

1. [リポジトリを複製](#1-clone-the-repository-clone-the-repository)
1. [GuideLocalizationService へのロケールの追加](#1-add-a-locale-to-the-guide-localization-service-add-a-locale-to-the-guide-localization-service-br)
1. [locale-name 固有のフォルダーを追加](#3-add-locale-name-specific-folder-add-locale-name-specific-folder)
1. [XFA クライアントライブラリをロケール用に追加](#3-add-xfa-client-library-for-a-locale)
1. [アダプティブフォームのクライアントライブラリをロケール用に追加](#4-add-adaptive-form-client-library-for-a-locale-add-adaptive-form-client-library-for-a-locale-br)
1. [辞書のロケールサポートの追加](#5-add-locale-support-for-the-dictionary-add-locale-support-for-the-dictionary-br)
1. [リポジトリ内の変更をコミットし、パイプラインをデプロイします。](#7-commit-the-changes-in-the-repository-and-deploy-the-pipeline-commit-changes-in-repo-deploy-pipeline)

### 1.リポジトリのクローンを作成します。 {#clone-the-repository}

1. コマンドラインから、FormsCloud Serviceリポジトリのクローン先に移動します。
1. 次のコマンドを実行します。 [Cloud Manager から取得したもの。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) これは次のようになります。 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. git のユーザー名とパスワードを使用して、リポジトリを複製します。
1. クローンされたFormsCloud Serviceリポジトリフォルダーを任意のエディターで開きます。

### 2.ロケールを Guide Localization サービスに追加する {#add-a-locale-to-the-guide-localization-service-br}

1. を `Guide Localization Service.cfg.json` ファイルを作成し、追加するロケールを、サポート対象のロケールのリストに追加します。

   >[!NOTE]
   >
   >* という名前のファイルを作成します。 `Guide Localization Service.cfg.json` ファイルに含めます（存在しない場合）。


### 3.ロケール名固有のフォルダークライアントライブラリを追加する {#add-locale-name-specific-folder}

1. UI.content フォルダーで、 `etc/clientlibs` フォルダー。
1. さらに、という名前のフォルダーを作成します。 `locale-name` under `etc/clientlibs` xfa および af clientlibs のコンテナとして機能します。

#### 3.1 ロケール用の XFA クライアントライブラリを locale-name フォルダーに追加する

1. という名前のノードを作成します。 `[locale-name]_xfa` と入力します。 `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`、カテゴリ `xfaforms.I18N.<locale>`をクリックし、次のファイルを追加します。
* `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N` で定義されている `<locale>` の `xfalib.locale.Strings` を定義している **I18N.js**。
* 以下を含む **js.txt** ファイル。
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

#### 3.2.ロケール locale-name フォルダー用のアダプティブフォームクライアントライブラリを追加する {#add-adaptive-form-client-library-for-a-locale-br}

1. という名前のノードを作成します。 `[locale-name]_af` と入力します。 `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`、カテゴリを `guides.I18N.<locale>` および依存関係 `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` および `guide.common`.
1. という名前のフォルダーを作成します。 `javascript` 次のファイルを追加します。

   * **i18n.js** は `guidelib.i18n` を定義し、`datePatterns` の「calendarSymbols」、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`、`typefaces`、`<locale>` のパターンを持つファイルです。これらは[ロケールセットの仕様](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)に記載されている XFA 仕様に従います。
   * **LogMessages.js** は、`/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js` で定義された `<locale>` の `guidelib.i18n.strings` と `guidelib.i18n.LogMessages` を定義します。

1. 追加 **js.txt** には、次の情報が含まれます。

   ```text
     i18n.js
       LogMessages.js
   ```

### 4.辞書のロケールサポートを追加する {#add-locale-support-for-the-dictionary-br}

追加する `<locale>` が、`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` 以外の場合にのみ、この手順を実行してください。

1. フォルダーの作成 `languages` under `etc`（まだ存在しない場合）

1. 既に存在しない場合は、複数の値を持つ文字列プロパティ `languages` をノードに追加します。
1. 既に存在しない場合は、`<locale-name>`デフォルトのロケール値`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` を追加します。

1. `<locale>` を `/etc/languages` の `languages` プロパティの値に追加します。


```text
Add the newly created folders in the `filter.xml` under etc/META-INF/[folder hierarchy] as:
<filter root="/etc/clientlibs/[locale-name]"/>
<filter root="/etc/languages"/>
```

変更をAEM Git リポジトリにコミットする前に、 [Git リポジトリ情報](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

### 5.リポジトリ内の変更をコミットし、パイプラインをデプロイします {#commit-chnages-in-repo-deploy-pipeline}

新しいロケールサポートを追加した後、変更を GIT リポジトリにコミットします。 フルスタックパイプラインを使用してコードをデプロイします。 学ぶ [パイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 新しいロケールサポートを追加する。

パイプラインが完了すると、新しく追加されたロケールがAEM環境に表示されます。

### アダプティブFormsで追加されたロケールを使用する {#use-added-locale-in-af}

新しく追加されたロケールを使用してアダプティブフォームを使用してレンダリングする手順は次のとおりです。

1. AEM オーサーインスタンスにログインします。
1. に移動します。 **Forms** >  **Formsとドキュメント**.
1. アダプティブフォームを選択し、 **辞書を追加** および **辞書を翻訳プロジェクトに追加** ウィザードが表示されます。
1. 次を指定： **プロジェクトタイトル** をクリックし、 **ターゲット言語** を選択します。 **辞書を翻訳プロジェクトに追加** ウィザード。
1. クリック **完了** 作成した翻訳プロジェクトを実行します。
1. アダプティブフォームを選択し、 **プレビューをHTML**.
1. 追加 `&afAcceptLang=<locale-name>` アダプティブフォームの URL 内で使用する必要があります。
1. ページを更新すると、アダプティブフォームは指定されたロケールでレンダリングされます。

アダプティブフォームのロケールを識別する方法は 2 つあります。 アダプティブフォームがレンダリングされると、リクエストされたロケールが次のように識別されます。

* アダプティブフォームの URL の `[local]` セレクターを確認します。URL の形式は、`http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled` です。`[local]` セレクターを使用すると、アダプティブフォームをキャッシュできます。

* 指定した順序で次のパラメーターを確認します。

   * リクエストパラメーター`afAcceptLang`
ユーザーのブラウザーロケールを上書きするには、 
`afAcceptLang` リクエストパラメーターを渡して、ロケールを強制します。例えば、次の URL は、強制的にカナダ語とフランス語のロケールでフォームをレンダリングします。
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * ユーザー向けに設定されるブラウザーのロケールです。これは、`Accept-Language` ヘッダーを使用したリクエストで指定されます。

リクエストされたロケールでクライアントライブラリが存在しない場合、ロケールに含まれる言語コードがクライアントライブラリに存在しないかチェックします。例えば、要求されたロケールが `en_ZA` （南アフリカ英語）と `en_ZA` が存在しない場合、アダプティブフォームは次のクライアントライブラリを使用します： `en` （英語）言語（存在する場合）。 ただし、どちらも存在しない場合、アダプティブフォームでは `en` ロケールの辞書が使用されます。


ロケールが識別されると、アダプティブフォームはフォーム固有の辞書を選択します。 リクエストされたロケールのフォーム固有の辞書が見つからない場合、アダプティブフォームが作成されている言語用の辞書が使用されます。

ロケール情報が存在しない場合、アダプティブフォームはフォームの元の言語で配信されます。元の言語は、アダプティブフォームの開発時に使用する言語です。

取得 [サンプルクライアントライブラリ](/help/forms/assets/locale-support-sample.zip) 新しいロケールのサポートを追加する場合。 必要なロケールでフォルダーのコンテンツを変更する必要があります。

### 新しいローカライゼーションをサポートするためのベストプラクティス {#best-practices}

* Adobeは、アダプティブフォームの作成後に翻訳プロジェクトを作成することをお勧めします。

* 既存のアダプティブフォームに新しいフィールドが追加された場合：
   * **機械翻訳の場合**:辞書を再作成し、翻訳プロジェクトを実行します。 翻訳プロジェクトの作成後にアダプティブフォームに追加されたフィールドは、未翻訳のままです。
   * **人間による翻訳の場合**:辞書の書き出しに使用する手順 `[server:port]/libs/cq/i18n/gui/translator.html`. 新しく追加されたフィールドの辞書を更新し、アップロードします。
