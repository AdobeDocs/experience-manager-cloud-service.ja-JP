---
title: 基盤コンポーネントに基づいてアダプティブフォームに新しいロケールのサポートを追加する方法を教えてください。
description: アダプティブフォームでは、追加設定なしで提供されるロケールとは別に、他の言語用のロケールを追加できます。
feature: Adaptive Forms, Foundation Components
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1220'
ht-degree: 100%

---

# アダプティブフォームのローカライゼーションのための新しいロケールのサポート {#supporting-new-locales-for-adaptive-forms-localization}

>[!NOTE]
>
> [新しいアダプティブフォームを作成する](/help/forms/creating-adaptive-form-core-components.md)、または [AEM Sites ページにアダプティブフォームを追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)際には、最新の拡張可能なデータキャプチャである[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する従来の方法について説明します。


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html?lang=ja) |
| コアコンポーネント | [ここをクリックしてください](supporting-new-language-localization-core-components.md) |
| 基盤コンポーネント | この記事 |

AEM Forms が標準でサポートしているロケールは、英語（en）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ドイツ語（de）、日本語（ja）、ブラジルポルトガル語（pt-br）、中国語（zh-tn）、台湾中国語（zh-tw）、韓国語（ko-kr）です。その他のロケール（ヒンディー語（hi_IN）など）のサポートを追加することもできます。

## ロケールの辞書について {#about-locale-dictionaries}

アダプティブフォームのローカリゼーションは、次の 2 種類のロケールの辞書に基づいています。

* **フォーム固有の辞書**&#x200B;は、アダプティブフォーム使用する文字列を含みます。例：ラベル、フィールド名、エラーメッセージ、ヘルプの説明など。ロケールごとに、XLIFF ファイルのセットとして管理されています。`[author-instance]/libs/cq/i18n/gui/translator.html` からアクセスできます。

* **グローバル辞書** 2 つのグローバル辞書があり、AEM クライアントライブラリで JSON オブジェクトとして管理されています。これらの辞書にはデフォルトのエラーメッセージ、月名、通貨シンボル、日付と時間のパターンなどが含まれます。これらの辞書は `[author-instance]/libs/fd/xfaforms/clientlibs/I18N` にあります。これらの場所では、各ロケールごとに別々のフォルダーが用意されています。グローバルの辞書は頻繁に更新されることはありません。ロケールごとに個別の JavaScript ファイルを保持することで、ブラウザーはそれらをキャッシュし、同一サーバー上で異なるアダプティブフォームにアクセスする際に、ネットワーク帯域幅の使用量を減らすことができます。

## 新しいロケールへのサポートの追加 {#add-support-for-new-locales}

新しいロケールへのサポートを追加する手順は、次のとおりです。

1. [サポートされていないロケールにローカリゼーションのサポートを追加する](#add-localization-support-for-non-supported-locales)
1. [アダプティブフォームで追加されたロケールの使用](#use-added-locale-in-af)

### サポートされていないロケールにローカリゼーションのサポートを追加する {#add-localization-support-for-non-supported-locales}

現在、AEM Forms がサポートしているアダプティブフォームコンテンツのロケールは、英語（en）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ドイツ語（de）、日本語（ja）、ブラジルポルトガル語（pt-BR）、中国語（zh-CN）、台湾中国語（zh-TW）、韓国語（ko-KR）です。

アダプティブフォーム実行時に新しいロケールのサポートを追加するには、次を参照してください。

1. [リポジトリのクローン](#clone-the-repository)
1. [GuideLocalizationService へのロケールの追加](#add-a-locale-to-the-guide-localization-service)
1. [ロケール名固有のフォルダーの追加](#add-locale-name-specific-folder)
1. [辞書のロケールサポートの追加](#add-locale-support-for-the-dictionary)
1. [リポジトリ内の変更をコミットし、パイプラインをデプロイします](#commit-changes-in-repo-deploy-pipeline)

#### 1. リポジトリのクローンを作成する {#clone-the-repository}

1. コマンドラインで、Forms Cloud Service リポジトリのクローン先に移動します。
1. [Cloud Manager から取得](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)したコマンドを実行します。`git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/` のようになります。
1. git のユーザー名とパスワードを使用して、リポジトリのクローンを作成します。
1. 任意のエディターで、クローン作成された FormsCloud Service リポジトリフォルダーを開きます。

#### 2. ロケールを Guide Localization Service に追加する {#add-a-locale-to-the-guide-localization-service}

1. `Guide Localization Service.cfg.json` ファイルを見つけて、追加するロケールをサポート対象のロケールの一覧に追加します。

   >[!NOTE]
   >
   > まだ存在しない場合は、`Guide Localization Service.cfg.json` という名前のファイルを作成します。

#### 3. ロケール名固有のフォルダークライアントライブラリを追加する {#add-locale-name-specific-folder}

1. UI.content フォルダーで、`etc/clientlibs` フォルダーを作成します。
1. さらに、`etc/clientlibs` の下に `locale-name` という名前のフォルダーを作成して、xfa および af clientlibs のコンテナとして機能させます。

##### 3.1 ロケール用の XFA クライアントライブラリを locale-name フォルダーに追加する

`[locale-name]_xfa` という名前のノードを作成し、`etc/clientlibs/locale_name` の下に `cq:ClientLibraryFolder` と入力して、カテゴリ `xfaforms.I18N.<locale>` を指定し、次のファイルを追加します。

* `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N` で定義されている `<locale>` の `xfalib.locale.Strings` を定義している **I18N.js**。
* 以下を含む **js.txt** ファイル。
  */libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. ロケール用のアダプティブ フォームクライアントライブラリを locale-name フォルダーに追加する

1. `[locale-name]_af` という名前のノードを作成し、`etc/clientlibs/locale_name` の下に `cq:ClientLibraryFolder` と入力します。カテゴリを `guides.I18N.<locale>`、依存関係を `xfaforms.3rdparty`、`xfaforms.I18N.<locale>` および `guide.common` に指定します。
1. `javascript` という名前のフォルダーを作成し、次のファイルを追加します。

   * **i18n.js** は `guidelib.i18n` を定義し、`datePatterns` の「calendarSymbols」、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`、`typefaces`、`<locale>` のパターンを持つファイルです。これらは[ロケールセットの仕様](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)に記載されている XFA 仕様に従います。
   * **LogMessages.js** は、`/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js` で定義された `<locale>` の `guidelib.i18n.strings` と `guidelib.i18n.LogMessages` を定義します。

1. 以下を含む **js.txt** を追加します。

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. 辞書のロケールサポートを追加する {#add-locale-support-for-the-dictionary}

追加する `<locale>` が、`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` 以外の場合にのみ、この手順を実行してください。

1. まだ存在しない場合は、`etc` の下にフォルダー `languages` を作成します。

1. 既に存在しない場合は、複数の値を持つ文字列プロパティ `languages` をノードに追加します。
1. 既に存在しない場合は、`<locale-name>`デフォルトのロケール値`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` を追加します。

1. `<locale>` を `/etc/languages` の `languages` プロパティの値に追加します。
1. etc/META-INF/[folder hierarchy] の `filter.xml` に、作成したフォルダーを次のように追加します。

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

変更をAEM Git リポジトリにコミットする前に、[Git リポジトリ情報](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=jp#accessing-git)にアクセスする必要があります。

#### 5. リポジトリ内の変更をコミットし、パイプラインをデプロイする {#commit-changes-in-repo-deploy-pipeline}

ロケールサポートを追加した後、変更を Git リポジトリにコミットします。フルスタックパイプラインを使用してコードをデプロイします。[パイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)を学び、新しいロケールのサポートを追加します。
パイプラインが完了すると、新しく追加されたロケールが AEM 環境に表示されます。

### アダプティブフォームで追加されたロケールの使用 {#use-added-locale-in-af}

新しく追加されたロケールを使用してアダプティブフォームを使用しレンダリングするには、次の手順を実行します。

1. AEM オーサーインスタンスにログインします。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。
1. アダプティブフォームを選択し、「**辞書を追加**」をクリックすると、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードが表示されます。
1. **プロジェクトタイトル**&#x200B;を指定し、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードのドロップダウンメニューから「**ターゲット言語**」を選択します。
1. 「**完了**」をクリックし、作成した翻訳プロジェクトを実行します。
1. アダプティブフォームを選択し、「**HTML としてプレビュー**」をクリックします。
1. アダプティブフォームの URL に `&afAcceptLang=<locale-name>` を追加します。
1. ページを更新すると、アダプティブフォームは指定されたロケールでレンダリングされます。

アダプティブフォームのロケールを識別する方法は 2 つあります。アダプティブフォームがレンダリングされると、リクエストされたロケールが次のように識別されます。

* アダプティブフォームの URL の `[local]` セレクターを取得します。URL の形式は、`http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled` です。`[local]` セレクターを使用すると、アダプティブフォームをキャッシュできます。

* 次のパラメーターをリスト順に取得します。

   * リクエストパラメーター `afAcceptLang`
ユーザーのブラウザーロケールを上書きするには、`afAcceptLang` リクエストパラメーターを渡して、ロケールを強制的に指定します。例えば、次の URL はフォームをカナダのフランス語ロケールで強制的にレンダリングします。
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * ユーザー向けに設定されるブラウザーのロケールです。これは、`Accept-Language` ヘッダーを使用したリクエストで指定されます。

リクエストされたロケールのクライアントライブラリが存在しない場合、ロケールに含まれる言語コードのクライアントライブラリが存在するか確認します。例えば、リクエストされたロケールが `en_ZA`（南アフリカ英語）で `en_ZA` 用のクライアントライブラリが存在しない場合、アダプティブフォームは、`en`（英語）言語のクライアントライブラリがあればそれを使用します。ただし、どちらも存在しない場合、アダプティブフォームでは `en` ロケールの辞書が使用されます。


ロケールが識別されると、アダプティブフォームはフォーム固有の辞書を選択します。要求されたロケールに対応するフォーム固有の辞書が見つからない場合、アダプティブフォームが作成された言語の辞書が使用されます。

ロケール情報が存在しない場合、アダプティブフォームはフォームの元の言語で配信されます。元の言語は、アダプティブフォームの開発時に使用する言語です。

[サンプルクライアントライブラリ](/help/forms/assets/locale-support-sample.zip)を入手して、新しいロケールのサポートを追加してください。必要なロケールでフォルダーのコンテンツを変更する必要があります。

## 新しいローカライゼーションをサポートする上でのベストプラクティス {#best-practices}

* アドビは、アダプティブフォームの作成後に翻訳プロジェクトを作成することをお勧めします。

* 新しいフィールドが既存のアダプティブフォームに追加された場合：
   * **機械翻訳の場合**：辞書を再作成し、翻訳プロジェクトを実行します。 翻訳プロジェクトの作成後にアダプティブフォームに追加されたフィールドは、未翻訳になります。
   * **人間による翻訳の場合**：`[server:port]/libs/cq/i18n/gui/translator.html` から辞書を書き出します。 新しく追加されたフィールド用の辞書を更新し、アップロードします。


## 関連トピック {#see-also}

{{see-also}}