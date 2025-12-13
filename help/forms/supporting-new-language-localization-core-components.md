---
title: コアコンポーネントに基づいてアダプティブフォームに新しいロケールのサポートを追加するには、どうすればよいですか？
description: アダプティブフォームに新しいロケールを追加する方法を説明します。
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 98%

---

# コアコンポーネントに基づくアダプティブフォームのロケールの追加 {#supporting-new-locales-for-adaptive-forms-localization}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| 基盤コンポーネント | [ここをクリックしてください](supporting-new-language-localization.md) |
| コアコンポーネント | この記事 |

<span class="preview"> 右から左へ記述する言語サポート機能は、早期導入プログラムで利用できます。早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

AEM Forms が標準でサポートしているロケールは、英語（en）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ドイツ語（de）、日本語（ja）、ブラジルポルトガル語（pt-br）、中国語（zh-tn）、台湾中国語（zh-tw）、韓国語（ko-kr）です。その他のロケール（ヒンディー語（hi_IN）など）のサポートを追加することもできます。また、これらのロケールを追加すると、右横書き（RTL）言語（アラビア語、ペルシア語、ウルドゥー語など）でアダプティブフォームを表示することもできます。

>[!VIDEO](https://video.tv.adobe.com/v/3433132/adaptive-forms-rtl--arabic-hebrew-farsi)

## 適用性とユースケース

### 保険

## AEM Formsは多言語保険のユースケースをサポートしていますか？

はい。AEM Formsは、地域や言語を超えて事業を行う保険会社にとって重要な、多言語フォームのエクスペリエンスをサポートしています。

## AEM Forms では、アダプティブフォームのロケールをどのように判断しますか？

AEM Forms でアダプティブフォームのレンダリング用にロケールを選択する方法を理解することは、適切にローカライゼーションを行うために重要です。選択プロセスの分類を以下に示します。

### 優先度ベースのロケールの選択

AEM Forms では、アダプティブフォームのロケールを判断するために、次のメソッドを優先します。

1. **URL ロケールセレクター（[ロケール]）**：

   システムでは、[ロケール]セレクターを使用して URL 内で指定したロケールが優先されます。この形式を使用すると、キャッシュを使用してパフォーマンスを向上させることができます。

   形式：URL は、http:/[AEM Forms Server URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled の形式に従います。

   例：https://[server]/content/forms/af/contact-us.hi.html では、フォームをヒンディー語でレンダリングします。


1. **afAcceptLang リクエストパラメーター**：

   ユーザーのブラウザーロケールを上書きするには、URL で `afAcceptLang` パラメーターを使用します。

   例：https://[server]/forms/af/survey.ca-fr.html?afAcceptLang=ca-fr では、フォームをカナダのフランス語で強制的にレンダリングします。

1. **ユーザーのブラウザーロケール（使用可能言語ヘッダー）**：

   他のロケールを指定していない場合、AEM Forms では `Accept-Language` ヘッダーを使用して送信されたユーザーのブラウザーロケールを考慮します。


### フォールバックメカニズム：


* リクエスト済みのロケールのクライアントライブラリ（新しいロケールを追加するプロセス。このドキュメントで後述）が使用できない場合、AEM Forms ではロケール内の言語コードに基づいてライブラリを確認します。

  例：en_ZA（南アフリカ英語）をリクエスト済みで、en_ZA ライブラリがない場合は、使用可能であれば en（英語）が使用されます。

  適切なクライアントライブラリが見つからない場合は、フォームのオーサリング言語のデフォルトの辞書（ほとんどの場合 `en`）が使用されます。

  ロケール情報がない場合、アダプティブフォームは開発時に使用された元の言語で表示されます。


## ロケール追加の前提条件

アダプティブフォームに新しいロケールを追加する前に、次の点を確認してください。

**ソフトウェア：**

* プレーンテキストエディター（IDE）：どのプレーンテキストエディターでも機能しますが、[Microsoft Visual Studio Code](https://code.visualstudio.com/download) などの統合開発環境（IDE）では、編集を簡単にする高度な機能が提供されます。

* Git：コードの変更を管理するには、このバージョン管理システムが必須です。インストール済みでない場合は、[https://git-scm.com](https://git-scm.com) からダウンロードしてください。


**コードリポジトリ：**

アダプティブフォームコアコンポーネントリポジトリのクローンを作成：ロケールを追加するには、このリポジトリのクライアントライブラリが必要です。リポジトリのクローンを作成するには、以下を行います。

1. コマンドラインまたはターミナルウィンドウを開きます。

1. 保存したいマシン上の目的の場所（例：/adaptive-forms-core-components）にリポジトリを移動します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   このコマンドでリポジトリをダウンロードし、マシン上に `aem-core-forms-components` という名前のフォルダーを作成します。このガイドでは、このフォルダーを `[Adaptive Forms Core Components repository]` と呼びます。


## ロケールの追加 {#add-localization-support-for-non-supported-locales}

コアコンポーネントに基づいてアダプティブフォームに新しいロケールのサポートを追加するには、次の手順に従います。

### AEM as a Cloud Service Git リポジトリのクローンを作成

1. コマンドラインを開き、AEM as a Cloud Service リポジトリを保存するディレクトリ（例：`/cloud-service-repository/`）を選択します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   Git リポジトリのクローンを作成するには、次の情報が必要です。

   * **組織名**：Adobe Experience Manager as a Cloud Service（AEM as a Cloud Service）内のチームまたはプロジェクトが識別されます。

   * **プログラム ID**：リポジトリに関連付けられたプログラムが指定されます。

   * **資格情報**：リポジトリに安全にアクセスするには、ユーザー名とパスワード（または個人アクセストークン）が必要です。

   **この情報はどこにありますか？**

   これらの詳細を見つける手順について詳しくは、Adobe Experience League の記事「[Git へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git)」を参照してください。

   **プロジェクトの準備が整いました。**

   コマンドが正常に完了すると、ローカルディレクトリに新しいフォルダーが作成されます。このフォルダーには、プログラムにちなんだ名前（例：program-id）が付けられます。このフォルダーには、AEM as a Cloud Service Git リポジトリからダウンロードしたすべてのファイルとコードが含まれます。

   このガイドでは、このフォルダーを `[AEMaaCS project directory]` と呼びます。


### Guide Localization Service に新しいロケールを追加

1. エディターでリポジトリフォルダーを開きます。

   ![エディターでのリポジトリフォルダー](/help/forms/assets/repository-folder-in-an-editor.png)

1. `Guide Localization Service.cfg.json` ファイルを見つけます。このファイルは、AEM Forms アプリケーションでサポートされているロケールを制御します。このファイルを編集すると、新しいロケールを追加できます。

   * **既存のファイル**：ファイルが既に存在する場合は、AEM Forms プロジェクトディレクトリ内で見つけます。標準の場所は次のとおりです。

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     `<appid>` をプロジェクト固有のアプリ ID に置き換えます。AEM プロジェクトの `<appid>` は `archetype.properties` ファイルにあります。

     ![アーキタイププロパティ](/help/forms/assets/archetype-properties.png)

   * **新規ファイル**：ファイルが存在しない場合は、上記と同じ場所に作成する必要があります。このドキュメントからファイル名をコピー＆ペーストするのではなく、手動で名前を入力します。ファイル名 `Guide Localization Service.cfg.json` には、スペースが含まれます。これは意図的なもので、ドキュメント内の誤字ではありません。

     OOTB でサポートされているロケールのリストを含むサンプルファイルは次のとおりです。

     ```
         {
             "supportedLocales":[
             "en",
             "fr",
             "de",
             "ja",
             "pt-br",
             "zh-cn",
             "zh-tw",
             "ko-kr",
             "it",
             "es"
             ]
         }
     ```

1. 目的の言語のロケールコードをファイルに追加します。
   1. [ISO 639-1コードリスト](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes)を使用して、目的の言語を表す 2 文字のコードを見つけます。

   1. `Guide Localization Service.cfg.json` ファイルにロケールコードを含めます。以下に例を示します。

      * 左から右に記述する言語：
         * 英語（米国）：en-US
         * スペイン語（スペイン）：es-ES
         * フランス語（フランス）：fr-FR
      * 右から左に記述する言語：
         * アラビア語（アラブ首長国連邦）：ar-ae
         * ヘブライ語：he（または歴史的参照用の iw）
         * ペルシア語：fa

1. 変更を行った後、`Guide Localization Service.cfg.json` ファイルが有効な JSON ファイルとして正しく書式設定されていることを確認します。JSON の書式設定にエラーがあると、正しく機能しない場合があります。ファイルを保存します。



### サンプルクライアントライブラリを活用してロケールを簡単に追加

AEM Forms には、新しいロケールの追加を簡素化する便利なサンプルクライアントライブラリ `clientlib-it-custom-locale` が用意されています。このライブラリは、GitHub で入手できる[アダプティブフォームコアコンポーネントリポジトリ](https://github.com/adobe/aem-core-forms-components)の一部です。


開始する前に、[アダプティブフォームコアコンポーネントリポジトリ]のローカルコピーがあることを確認します。ない場合は、次のコマンドで Git を使用して簡単にクローンを作成できます。

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

このコマンドで、マシン上の aem-core-forms-components というディレクトリに、clientlib-it-custom-locale ライブラリを含むリポジトリ全体をダウンロードします。

![ローカルマシン上のアダプティブフォームコアコンポーネントリポジトリのディレクトリ](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### サンプルクライアントライブラリを統合

次に、AEM as a Cloud Service、[AEMaaCS プロジェクトディレクトリ]に `clientlib-it-custom-locale` ライブラリを組み込みます。

1. サンプルクライアントライブラリを見つけます。

   [アダプティブフォームコアコンポーネントリポジトリ]のローカルコピー内で、次のパスに移動します。

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. 次の手順に従って、ライブラリをコピー＆ペーストします。

   1. `clientlib-it-custom-locale` フォルダーをコピーします。

      ![clientlib-it-custom-locale のコピー](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. [AEMaaCS プロジェクトディレクトリ]内の次のディレクトリに移動します。

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **重要**：`<app-id>` をアプリケーションの実際の ID に置き換えます。

   1. コピーした `clientlib-it-custom-locale` フォルダーをこのディレクトリにペーストします。

      ![clientlib-it-custom-locale のペースト](/help/forms/assets/clientlib-it-custom-locale-paste.png)

1. `languageinit.js` の `aemLangUrl` パスを更新します

   1. [AEMaaCS プロジェクトディレクトリ]内の次のディレクトリに移動します。

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib/clientlib-it-custom-locale/js
      ```

   1. `languageinit.js` ファイルをエディターで開きます。
   1. `languageinit.js` ファイル内の次の行を探します。

      `const aemLangUrl = /etc.clientlibs/forms-core-components-it/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json;`

   1. 上記の行の `forms-core-components-it` を `<app-id>`（アプリケーションの実際の ID）に置き換えます。

      `const aemLangUrl = '/etc.clientlibs/<app-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json';`

      ![language-init-file](/help/forms/assets/language-init-name-change.png)

>[!NOTE]
>  
> `forms-core-components-it` をプロジェクト名または `<app-id>` に置き換えないと、日付選択コンポーネントは翻訳に失敗します。

### 次の手順に従って、新しいロケールのファイルを作成します。

1. ロケールディレクトリに移動します。

   `[AEMaaCS project directory]` 内で、次のパスに移動します。

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **重要**：`<program-id>` を実際のアプリケーション ID に置き換えます。

1. サンプルの英語ファイルを見つけます。

   AEM Forms では、[GitHub 上にサンプルの英語ロケールファイル（.json）](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json)が用意されています。

   英語の言語ファイルには、参照用のデフォルトの文字列セットが含まれます。ロケール固有のファイルは、英語の言語ファイルの構造を模倣する必要があります。

   アラビア語、ヘブライ語、ペルシア語などの言語では、テキストは英語のように左から右（LTR）ではなく、右から左（RTL）に読み取られます。これらの言語でフォームを正しく表示するには、サンプルロケールファイルをガイドとして使用することをお勧めします。これらのファイルは、RTL 言語のテキスト、日付およびその他の要素を書式設定する方法に関する参照を提供します。次のサンプルロケールファイルを確認できます。

   * [アラビア語](/help/forms/assets/ar-ae.json)
   * [ヘブライ語](/help/forms/assets/he.json)
   * [ペルシア語](/help/forms/assets/fa.json)

   これらのサンプルファイルを活用することで、RTL 言語で作業するユーザーにシームレスなエクスペリエンスをフォームで提供できます。


1. ロケールファイルを作成します。

   1. `i18n` ディレクトリ内に新しい .json ファイルを作成します。
   1. 目的の言語の適切なロケールコードを使用してファイルに名前を付けます（例：フランス語の場合は fr-FR.json、アラビア語の場合は ar-ae.json）。このファイルの構造は、英語ロケールファイルと同じである必要があります。


1. 構造と翻訳：

   1. 新しく作成したファイルをテキストエディターで開きます。

   1. 英語の値を、ターゲット言語の対応する翻訳に置き換えます。

   1. 文字列の翻訳が完了したら、ファイルを保存します。




### 辞書にロケールサポートを追加

この手順は、英語（en）、ドイツ語（de）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ポルトガル語（ブラジル）（pt-br）、中国語（簡体字 - zh_cn）、中国語（繁体字 - zh_tw）、日本語（ja）および韓国語（ko_kr）の一般的にサポートされているロケール以外のロケールにのみ適用されます。

1. 設定フォルダーを見つけます。

   [AEMaaCS プロジェクトディレクトリ]内の次のディレクトリに移動します。

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. 必要なフォルダーを作成します（ない場合）。

   `jcr_root` フォルダー内に `etc` フォルダーが存在しない場合は作成します。`etc` 内に `languages` という名前の別のフォルダーがない場合は作成します。

1. ロケール設定ファイルを作成します。

   `languages` フォルダー内に、`.content.xml` という名前の新しいファイルを作成します。このドキュメントからファイル名をコピー＆ペーストするのではなく、手動で名前を入力します。

   ![`.content.xml`](etc-content-xml.png) という名前の新しいファイルを作成

   このファイルを開き、次の内容をペーストします。[LOCALE_CODE] を実際のロケールコード（例：アラビア語の場合は ar-ae）に置き換えます。


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   警告：既存のリストを置き換えないでください。代わりに、次のように（例として ar-ae を使用）新しいロケールコードを角括弧で囲み、コンマで区切って追加します。

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. 新しいフォルダーを filter.xml に含めます。

   [AEMaaCS プロジェクトディレクトリ]内の `/ui.content/src/main/content/meta-inf/vault/filter.xml` ファイルに移動します。

   ファイルを開き、最後に次の行を追加します。

   ```
   <filter root="/etc/languages"/>
   ```

   ![作成したフォルダーを `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png) の下にある `filter.xml` に追加します。

1. ファイルを保存します。

### 新しく作成したロケールを AEM 環境にデプロイ

これで、アダプティブフォームで新しいロケールを使用するすべての設定が完了しました。次の操作を実行できます。

* AEM as a Cloud Service の [AEMaaCS プロジェクトディレクトリ]をローカル開発環境にデプロイし、ローカルマシンで新しいロケール設定を試します。ローカル開発環境にデプロイするには：

   1. ローカル開発環境が起動および実行されていることを確認します。ローカル開発環境をまだ設定していない場合は、[AEM Forms のローカル開発環境の設定](/help/forms/setup-local-development-environment.md)のガイドを参照してください。

   1. ターミナルウィンドウまたはコマンドプロンプトを開きます。

   1. [AEMaaCS プロジェクトディレクトリ]に移動します。

   1. 次のコマンドを実行します。

      ```
      mvn -PautoInstallPackage clean install
      ```

* AEM as a Cloud Service の [AEMaaCS プロジェクトディレクトリ]を Cloud Service 環境にデプロイします。Cloud Service 環境にデプロイするには：

   1. 次の手順に従って、変更内容をコミットします。

      新しいロケール設定を追加したら、ロケールの追加を説明する明確な Git メッセージ（例：「[ロケール名のサポートが追加されました]」）を付けて変更内容をコミットします。

   1. 次の手順に従って、更新済みコードをデプロイします。

      [既存のフルスタックパイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)を通じてコードのデプロイメントをトリガーします。これにより、新しいロケールサポートを含む更新済みコードが自動的に作成およびデプロイされます。

      パイプラインをまだ設定していない場合は、[AEM Forms as a Cloud Service のパイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)のガイドを参照してください。


## 新しく追加されたロケールでのアダプティブフォームのプレビュー

次の手順では、新しく追加したロケールでアダプティブフォームをプレビューする方法について説明します。

1. AEM Forms as a Cloud Service インスタンスにログインします。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。
1. アダプティブフォームを選択し、「**辞書を追加**」をクリックすると、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードが表示されます。
1. **プロジェクトタイトル**&#x200B;を指定し、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードのドロップダウンメニューから「**ターゲット言語**」を選択します。
1. 「**完了**」をクリックし、作成した翻訳プロジェクトを実行します。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。
1. アダプティブフォームを選択し、「**HTML としてプレビュー**」オプションを選択します。
1. プレビュー URL に `&afAcceptLang=<locale-name>` を追加し、Return キーを押します。`<locale-name>` を実際のロケールコードに置き換えます。アダプティブフォームが指定したロケールで表示されます。

## 新しいローカライゼーションをサポートする上でのベストプラクティス {#best-practices}

* アドビでは、アダプティブフォームの作成後に翻訳プロジェクトを作成することをお勧めします。これにより、ローカライゼーションプロセスが効率化されます。
* 数値ボックスコンポーネントと日付選択コンポーネントを特定のロケールに翻訳すると、書式設定の問題が発生する場合があります。この問題を軽減するために、[日付選択コンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker#format-tab)と[数値ボックスコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/numeric-box#formats-configure-tab)の設定ダイアログに「**言語**」オプションが組み込まれました。


* 新しいフィールドの処理：

   * **機械翻訳**：機械翻訳を使用する場合は、既存のアダプティブフォームに新しいフィールドを追加した後、辞書を再作成し、再び[翻訳プロジェクトを実行](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md)する必要があります。最初の翻訳プロジェクト後に追加した新しいフィールドは、未翻訳のままになります。

   * **人間翻訳**：人間翻訳ワークフローの場合は、`[AEM Forms Server]/libs/cq/i18n/gui/translator.html` の UI を使用して辞書を書き出します。新しいフィールドの辞書を更新し、改訂バージョンをアップロードします。


## 関連トピック {#see-also}

{{see-also}}

* [アダプティブフォームにおけるレコードのドキュメントの生成](/help/forms/generate-document-of-record-core-components.md)
* [AEM Sites ページまたはエクスペリエンスフラグメントにアダプティブフォームの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

