---
title: アダプティブフォームのローカリゼーション用に新しいロケールをサポート
seo-title: Supporting new locales for Adaptive Forms localization
description: AEM Forms は、アダプティブフォームのローカライズ用に新しくロケールを追加できます。デフォルトでサポートされているロケールは、英語、フランス語、ドイツ語、日本語です。
seo-description: AEM Forms allows you to add new locales for localizing Adaptive Forms. The supported locales by default are English, French, German, and Japanese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 100%

---


# アダプティブフォームのローカリゼーション用に新しいロケールをサポート{#supporting-new-locales-for-adaptive-forms-localization}

## ロケールの辞書について {#about-locale-dictionaries}

アダプティブフォームのローカリゼーションは、次の 2 種類のロケールの辞書に基づいています。

**フォーム固有の辞書**&#x200B;は、アダプティブフォーム使用する文字列を含みます。例えば、ラベル、フィールド名、エラーメッセージ、ヘルプの説明文などです。各ロケールごとに、XLIFF ファイルのセットの形で管理されています。`https://<host>:<port>/libs/cq/i18n/translator.html` からアクセスできます。

**グローバル辞書** 2 つのグローバル辞書があり、AEM クライアントライブラリで JSON オブジェクトの形で管理されています。これらの辞書にはデフォルトのエラーメッセージ、12 か月の名前、通貨シンボル、日付と時間のパターンなどが含まれます。これらの辞書は CRXDe Lite の /libs/fd/xfaforms/clientlibs/I18N にあります。これらの場所では、各ロケールごと別々のフォルダーが用意されています。グローバルの辞書は頻繁に更新されることはありません。各ロケールごとに別の JavaScript ファイルを保持することで、ブラウザーによりそれらがキャッシュされるため、同一サーバー上で異なるアダプティブフォームにアクセスする際に、ネットワーク帯域幅の使用量を減らすことができます。

### アダプティブフォームのローカリゼーションの仕組み {#how-localization-of-adaptive-form-works}

アダプティブフォームのロケールを識別する方法は 2 つあります。アダプティブフォームがレンダリングされると、リクエストされたロケールが次のように識別されます。

* アダプティブフォームの URL の `[local]` セレクターを確認します。URL の形式は、`http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled` です。`[local]` セレクターを使用すると、アダプティブフォームをキャッシュできます。

* 指定した順序で次のパラメーターを確認します。

   * リクエストパラメーター`afAcceptLang`
ユーザーのブラウザーロケールを上書きするには、 
`afAcceptLang` リクエストパラメーターを渡して、ロケールを強制します。例えば、次の URL は日本語ロケールでのフォームのレンダリングを強制します。
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * ユーザー向けに設定されるブラウザーのロケールです。これは、`Accept-Language` ヘッダーを使用したリクエストで指定されます。

   * AEM のユーザー指定の言語設定です。

   * ブラウザーのロケールはデフォルトで有効です。ブラウザーロケール設定を変更するには
      * 設定マネージャーを開きます。URL は `http://[server]:[port]/system/console/configMgr` です
      * 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネル]**」の設定を検索して開きます。
      * 「**[!UICONTROL ブラウザーロケールを使用]**」オプションのステータスを変更して設定を「**[!UICONTROL 保存]**」します。

ロケールが識別されると、アダプティブフォームはフォームに固有の辞書を参照します。要求されたロケールに対応するフォーム固有の辞書が見つからない場合、アダプティブフォームが作成された言語の辞書が使用されます。

ロケール情報が存在しない場合、アダプティブフォームはフォームの元の言語で配信されます。元の言語は、アダプティブフォームの開発時に使用する言語です。

リクエストされたロケールでクライアントライブラリが存在しない場合、ロケールに含まれる言語コードがクライアントライブラリに存在しないかチェックします。例えば、リクエストされたロケールが `en_ZA`（南アフリカ英語）で `en_ZA` 用のクライアントライブラリが存在しない場合、アダプティブフォームは、`en`（英語）言語が存在する場合、このクライアントライブラリを使用します。ただし、どちらも存在しない場合、アダプティブフォームでは `en` ロケールの辞書が使用されます。

## サポートされていないロケールにローカリゼーションのサポートを追加する {#add-localization-support-for-non-supported-locales}

現在、[!DNL AEM Forms] がサポートしているアダプティブフォームコンテンツのロケールは、英語（en）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ドイツ語（de）、日本語（ja）、ブラジルポルトガル語（pt-BR）、中国語（zh-CN）、台湾中国語（zh-TW）、韓国語（ko-KR）です。

アダプティブフォーム実行時に新しいロケールのサポートを追加するには、次を参照してください。

1. [GuideLocalizationService へのロケールの追加](supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [XFA クライアントライブラリをロケール用に追加](supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [アダプティブフォームのクライアントライブラリをロケール用に追加](supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [辞書のロケールサポートの追加](supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [サーバーの再起動](supporting-new-language-localization.md#p-restart-the-server-p)

### Guide Localization Service へのロケールの追加 {#add-a-locale-to-the-guide-localization-service-br}

1. `https://'[server]:[port]'/system/console/configMgr` にアクセスします。
1. **Guide Localization Service** をクリックしてコンポーネントを編集します。
1. 追加するロケールを、サポート対象のロケールの一覧に追加します。

![GuideLocalizationService](assets/configservice.png)

### XFA クライアントライブラリをロケール用に追加 {#add-xfa-client-library-for-a-locale-br}

`etc/<folderHierarchy>` の下にカテゴリ `xfaforms.I18N.<locale>` のタイプ `cq:ClientLibraryFolder` のノードを作成し、次のファイルをクライアントライブラリに追加します。

* `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N` で定義されている `<locale>` の `xfalib.locale.Strings` を定義している **I18N.js**。

* 以下を含む **js.txt** ファイル。

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### アダプティブフォームのクライアントライブラリをロケール用に追加 {#add-adaptive-form-client-library-for-a-locale-br}

`etc/<folderHierarchy>` の下にタイプ `cq:ClientLibraryFolder` のノードを作成します。カテゴリは `guides.I18N.<locale>`、依存関係は `xfaforms.3rdparty`、`xfaforms.I18N.<locale>`、`guide.common` です。

クライアントライブラリに次のファイルを追加します。

* **i18n.js** は `guidelib.i18n` を定義し、`<locale>` の「calendarSymbols」、`datePatterns`、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`、`typefaces` のパターンを持つファイルです。これらは[ロケールセットの仕様](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)に記載されている XFA 仕様に従います。また、サポート対象の他のロケールがどのように定義されているか、`/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js` で確認することができます。
* **LogMessages.js** は、`/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js` で定義された `<locale>` の `guidelib.i18n.strings` と `guidelib.i18n.LogMessages` を定義します。
* 以下を含む **js.txt** ファイル。

```text
i18n.js
LogMessages.js
```

### 辞書のロケールサポートの追加 {#add-locale-support-for-the-dictionary-br}

追加する `<locale>` が、`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` 以外の場合にのみ、この手順を実行してください。

1. 既に存在しない場合は、`nt:unstructured` の下に、`languages` ノード `etc` を作成します。

1. 既に存在しない場合は、複数の値を持つ文字列プロパティ `languages` をノードに追加します。
1. 既に存在しない場合は、`<locale>`デフォルトのロケール値`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` を追加します。

1. `<locale>` を `/etc/languages` の `languages` プロパティの値に追加します。

`<locale>` は `https://'[server]:[port]'/libs/cq/i18n/translator.html` に表示されます。

### サーバーの再起動 {#restart-the-server}

追加したロケールを有効にするために AEM サーバーを再起動します。

## スペイン語サポートを追加する場合のサンプルライブラリ {#sample-libraries-for-adding-support-for-spanish}

スペイン語サポートを追加する場合のサンプルクライアントライブラリ

[ファイルを入手](assets/sample.zip)
