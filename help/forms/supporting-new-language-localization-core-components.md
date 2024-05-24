---
title: コアコンポーネントに基づくアダプティブフォームに新しいロケールのサポートを追加するにはどうすればよいですか？
description: アダプティブフォームに新しいロケールを追加する方法を説明します。
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
source-git-commit: 9cb3b52d0cf172c16777eadbc4d78b267c3db513
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 12%

---

# コアコンポーネントに基づくアダプティブフォームのロケールの追加 {#supporting-new-locales-for-adaptive-forms-localization}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| 基盤コンポーネント | [ここをクリックしてください](supporting-new-language-localization.md) |
| コアコンポーネント | この記事 |

<span class="preview"> 右から左に筆記する言語のサポート機能は、早期導入プログラムで利用できます。 早期導入プログラムに参加し、機能へのアクセスをリクエストするには、公式のメール ID で aem-forms-ea@adobe.com までメールを送信してください。</span>

AEM Forms が標準でサポートしているロケールは、英語（en）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ドイツ語（de）、日本語（ja）、ブラジルポルトガル語（pt-br）、中国語（zh-tn）、台湾中国語（zh-tw）、韓国語（ko-kr）です。その他のロケール（ヒンディー語（hi_IN）など）のサポートを追加することもできます。また、これらのロケールを追加すると、右横書き（RTL）言語（アラビア語、ペルシア語、ウルドゥー語など）でアダプティブフォームを表示することもできます。

## AEM Formsはアダプティブフォームのロケールをどのように決定しますか？

アダプティブフォームのレンダリング用のロケールをAEM Formsがどのように選択するかを理解することは、適切なローカライゼーションにとって重要です。 選択プロセスの分類を次に示します。

### 優先度ベースのロケールの選択

AEM Formsは、アダプティブフォームのロケールを決定するために、次のメソッドを優先します。

1. **URL ロケールセレクター（[locale]）**:

   システムは次を使用して、URL 内で指定されたロケールに優先順位を付けます [locale] セレクター。 この形式を使用すると、キャッシュのパフォーマンスが向上します。

   形式：URL は次の形式になります。http:/[AEM Forms Server の URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled.

   例：https://[サーバー]/content/forms/af/contact-us.hi.html は、フォームをヒンディー語でレンダリングします。


1. **afAcceptLang リクエストパラメーター**:

   ユーザーのブラウザーロケールを上書きするには、 `afAcceptLang` URL のパラメーター。

   例：https://[サーバー]/forms/af/survey.ca-fr.html?afAcceptLang=ca-fr は、カナダのフランス語でフォームを強制的にレンダリングします。

1. **ユーザーのブラウザーロケール （Accept-Language ヘッダー）**:

   他のロケールが指定されていない場合、AEM Formsは、 `Accept-Language` ヘッダー。


### フォールバックメカニズム：


* 要求されたロケールのクライアントライブラリ（新しいロケールを追加するプロセス。このドキュメントで後述）が使用できない場合、AEM Formsはロケール内の言語コードに基づいてライブラリをチェックします。

  例：en_ZA （南アフリカ英語）が要求され、en_ZA ライブラリがない場合、利用可能であれば en （英語）が使用されます。

  適切なクライアントライブラリが見つからない場合は、デフォルトの辞書（ほとんどの場合） `en`）が使用されます。

  ロケール情報がない場合、アダプティブフォームは開発時に使用された元の言語で表示されます。


## ロケール追加の前提条件

アダプティブFormsの新しいロケールの追加を開始する前に、次のものが揃っていることを確認します。

**ソフトウェア：**

* プレーンテキストエディター（IDE）：任意のプレーンテキストエディターも使用できますが、次のような統合開発環境（IDE）も使用できます [Microsoft Visual Studio Code](https://code.visualstudio.com/download) は、編集を容易にする高度な機能を提供します。

* Git：このバージョン管理システムは、コードの変更を管理するために必要です。 インストールされていない場合は、からダウンロードします。 [https://git-scm.com](https://git-scm.com).


**コードリポジトリー：**

アダプティブ Forms コアコンポーネントリポジトリを複製する：ロケールを追加するには、このリポジトリのクライアントライブラリが必要です。 リポジトリのクローンを作成するには、以下を行います。

1. コマンドラインまたはターミナルウィンドウを開きます。

1. リポジトリを保存するマシン上の目的の場所に移動します（例えば、/adaptive-forms-core-components）。

1. 次のコマンドを実行して、リポジトリをクローンします。

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   このコマンドは、リポジトリをダウンロードし、という名前のフォルダーを作成します。 `aem-core-forms-components` お使いのマシン上。 このガイド全体では、このフォルダーをと呼びます。 `[Adaptive Forms Core Components repository]`


## ロケールの追加 {#add-localization-support-for-non-supported-locales}

コアコンポーネントに基づいてアダプティブフォームに新しいロケールのサポートを追加するには、次の手順に従います。

### AEMas a Cloud ServiceGit リポジトリのクローン

1. コマンドラインを開き、AEMas a Cloud Serviceリポジトリを格納するディレクトリ（など）を選択します。 `/cloud-service-repository/`.

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   Git リポジトリを複製するには、次の情報が必要です。

   * **組織名**：これにより、Adobe Experience Manager as a Cloud Service内のチームまたはプロジェクトが識別されます（AEMas a Cloud Service）。

   * **プログラム ID**：リポジトリに関連付けられたプログラムを指定します。

   * **資格情報**：リポジトリに安全にアクセスするには、ユーザー名とパスワード（または個人用アクセストークン）が必要です。

   **この情報はどこにありますか？**

   これらの詳細を見つける手順については、Adobe Experience Leagueの記事「」を参照してください[Git へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git)」と入力します。

   **プロジェクトの準備が整いました。**

   コマンドが正常に完了すると、ローカルディレクトリに新しいフォルダーが作成されます。 このフォルダーには、プログラムの名前を付けます（例：program-id）。 このフォルダーには、AEMas a Cloud ServiceGit リポジトリーからダウンロードされたすべてのファイルとコードが含まれています。

   このガイド全体では、このフォルダーをと呼びます。 `[AEMaaCS project directory]`.


### 新しいロケールを Guide Localization Service に追加する

1. リポジトリフォルダーをエディターで開きます。

   ![エディターのリポジトリーフォルダー](/help/forms/assets/repository-folder-in-an-editor.png)

1. を見つけます。 `Guide Localization Service.cfg.json` ファイル。 このファイルは、AEM Forms アプリケーションでサポートされているロケールを制御します。 このファイルを編集して新しいロケールを追加できます。

   * **既存のファイル**：ファイルが既に存在する場合は、AEM Forms プロジェクトディレクトリ内で見つけます。 典型的な場所は次のとおりです。

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     置換 `<appid>` プロジェクト固有のアプリ ID を使用します。 次を見つけることができます `<appid>` におけるAEM プロジェクトの場合 `archetype.properties` ファイル。

     ![アーキタイププロパティ](/help/forms/assets/archetype-properties.png)

   * **新規ファイル**：ファイルが存在しない場合は、上記と同じ場所にファイルを作成する必要があります。 このドキュメントからファイル名を手動で入力するのではなく、コピーして貼り付けてください。 ファイル名 `Guide Localization Service.cfg.json` スペースを含みます。 これは意図的なもので、ドキュメントの誤字ではありません。

     OOTB でサポートされているロケールのリストを含むファイルのサンプルは次のとおりです。

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
   1. の使用 [ISO 639-1 コードの一覧](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) をクリックして、目的の言語を表す 2 文字のコードを検索します。

   1. ロケールコードをに含めます。 `Guide Localization Service.cfg.json` ファイル。 次に例を示します。

      * 左から右の言語：
         * 英語（米国）:en-US
         * スペイン語（スペイン）: es-ES
         * フランス語（フランス）: fr-FR
      * 右から左に筆記する言語：
         * アラビア語（アラブ首長国連邦）:ar-ae
         * ヘブライ語：he （または歴史的参考のための iw）
         * ペルシア語：fa

1. 変更を行った後、必ず `Guide Localization Service.cfg.json` ファイルは有効な JSON ファイルとして正しくフォーマットされています。 JSON 形式のエラーにより、正しく機能しない場合があります。 ファイルを保存します。



### サンプルクライアントライブラリを利用すると、ロケールを簡単に追加できます

AEM Formsは、便利なサンプルクライアントライブラリを提供します。 `clientlib-it-custom-locale`新しいロケールの追加を簡素化する。 このライブラリは、 [アダプティブ Forms コアコンポーネントリポジトリ](https://github.com/adobe/aem-core-forms-components)、GitHub で入手可能。


開始する前に、のローカルコピーを用意します [アダプティブ Forms コアコンポーネントリポジトリ]. そうでない場合は、次のコマンドを使用して、Git を使用して簡単にクローンを作成できます。

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

このコマンドは、clientlib-it-custom-locale ライブラリを含むリポジトリ全体を、マシン上の aem-core-forms-components という名前のディレクトリにダウンロードします。

![ローカルマシン上のアダプティブ Forms コアコンポーネントのリポジトリーディレクトリ](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### サンプルクライアントライブラリの統合

次に、を組み込みます `clientlib-it-custom-locale` AEMas a Cloud Serviceにライブラリを追加する。 [AEMaaCS プロジェクトディレクトリ]:

1. サンプルクライアントライブラリを見つけます。

   ローカルコピー内 [アダプティブ Forms コアコンポーネントリポジトリ]に移動し、次のパスに移動します。

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. ライブラリをコピーして貼り付けます。

   1. をコピーします `clientlib-it-custom-locale` フォルダー。

      ![clientlib-it-custom-locale のコピー](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. 内の次のディレクトリに移動します。 [AEMaaCS プロジェクトディレクトリ]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **重要**:Replace `<app-id>` とアプリケーションの実際の ID。

   1. コピーしたを貼り付けます `clientlib-it-custom-locale` フォルダーをこのディレクトリに追加します。

      ![clientlib-it-custom-locale の貼り付け](/help/forms/assets/clientlib-it-custom-locale-paste.png)


### 新しいロケール用のファイルを作成します。

1. ロケールディレクトリに移動します。

   内で `[AEMaaCS project directory]`に移動し、次のパスに移動します。

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **重要**:Replace `<program-id>` 実際のアプリケーション ID を使用します。

1. サンプルの英語ファイルを見つけます。

   AEM Formsはを提供します。 [github のサンプルの英語ロケールファイル（.json）](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json).

   英語の言語ファイルには、参照用のデフォルトの文字列セットが含まれています。 ロケール固有のファイルは、英語のファイルの構造に類似している必要があります。

   アラビア語、ヘブライ語、ペルシア語などの言語では、テキストは英語のように左から右（LTR）ではなく、右から左（RTL）に読み上げられます。 これらの言語でフォームを正しく表示するには、サンプルのロケールファイルを参考にすることをお勧めします。 これらのファイルは、RTL 言語のテキスト、日付およびその他の要素のフォーマット方法のリファレンスを提供します。 次のサンプルのロケールファイルを確認できます。

   * [アラビア語](/help/forms/assets/ar-ae.json)
   * [ヘブライ語](/help/forms/assets/he.json)
   * [ペルシ](/help/forms/assets/fa.json)

   これらのサンプルファイルを活用することで、RTL 言語で作業するユーザーにシームレスなエクスペリエンスをフォームで提供できます。


1. ロケールファイルの作成：

   1. 内に新しい.json ファイルを作成 `i18n` ディレクトリ。
   1. 目的の言語に適したロケールコードを使用してファイルに名前を付けます（例えば、フランス語の場合は fr-FR.json、アラビア語の場合は ar-ae.json など）。 このファイルの構造は、英語ロケールファイルを反映している必要があります。


1. 構造と翻訳：

   1. 新しく作成したファイルをテキストエディターで開きます。

   1. 英語の値をターゲット言語の対応する翻訳に置き換えます。

   1. 文字列の翻訳が完了したら、ファイルを保存します。




### 辞書へのロケールサポートの追加

この手順は、英語（en）、ドイツ語（de）、スペイン語（es）、フランス語（fr）、イタリア語（it）、ポルトガル語（pt-br）、中国語（簡体字 – zh_cn）、中国語（繁体字 – zh_tw）、日本語（ja）、韓国語（ko_kr）の一般的にサポートされているロケール以外にのみ適用されます。

1. 設定フォルダーを見つけます。

   次のディレクトリに移動します。 [AEMaaCS プロジェクトディレクトリ]:

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. 必要なフォルダー（ない場合）を作成します。

   次の場合 `etc` 内にフォルダーが存在しません `jcr_root` フォルダーを作成します。 内側 `etc`という名前の別のフォルダーを作成します。 `languages` 見つからない場合。

1. ロケール設定ファイルを作成します。

   内 `languages` フォルダーに、という名前の新しいファイルを作成します。 `.content.xml`. このドキュメントからファイル名を手動で入力するのではなく、コピーして貼り付けてください。

   ![という名前の新しいファイルを作成します。 `.content.xml`](etc-content-xml.png)

   このファイルを開き、次の内容を貼り付けます。を置き換えます。 [LOCALE_CODE] 実際のロケールコードを使用します（例：アラビア語の場合は ar-ae）。


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   警告：既存のリストを置き換えません。 代わりに、次のようにコンマで区切って、新しいロケールコードを角括弧で囲んで追加します（例として ar-ae を使用）。

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. 新規フォルダーを filter.xml に含めます。

   に移動します。 `/ui.content/src/main/content/meta-inf/vault/filter.xml` 内のファイル [AEMaaCS プロジェクトディレクトリ].

   ファイルを開き、末尾に次の行を追加します。

   ```
   <filter root="/etc/languages"/>
   ```

   ![作成したフォルダーを `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png) の下にある `filter.xml` に追加します。

1. ファイルを保存します。

### 新しく作成したロケールをAEM環境にデプロイします。

これで、アダプティブFormsで新しいロケールを使用する設定がすべて完了しました。 次のことができます

* AEMas a Cloud Service環境をデプロイします。 [AEMaaCS プロジェクトディレクトリ]をローカル開発環境に送信して、ローカルマシンで新しいロケール設定を試します。 ローカル開発環境にデプロイする手順は次のとおりです。

   1. ローカル開発環境が稼働していることを確認します。 ローカル開発環境をまだ設定していない場合は、のガイドを参照してください。 [AEM Formsのローカル開発環境の設定](/help/forms/setup-local-development-environment.md).

   1. ターミナルウィンドウまたはコマンドプロンプトを開きます。

   1. に移動します。 [AEMaaCS プロジェクトディレクトリ]

   1. 次のコマンドを実行します。

      ```
      mvn -PautoInstallPackage clean install
      ```

* AEMas a Cloud Service環境をデプロイします。 [AEMaaCS プロジェクトディレクトリ]をCloud Service環境に追加します。 Cloud Service環境にデプロイする手順は次のとおりです。

   1. 変更内容をコミットします。

      新しいロケール設定を追加した後、ロケールの追加を説明する明確な Git メッセージ（例：「のサポートの追加」）を使用して変更をコミットします [ロケール名]``）に含まれます。

   1. 更新されたコードをデプロイします。

      を使用したコードのデプロイメントのトリガー [既存のフルスタックパイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline). これにより、新しいロケールサポートを含む更新されたコードが自動的にビルドおよびデプロイされます。

      まだパイプラインを設定していない場合は、でガイドを参照してください [AEM Formsas a Cloud Service用のパイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline).


## 新しく追加されたロケールでのアダプティブフォームのプレビュー

次の手順では、新しく追加されたロケールでアダプティブフォームをプレビューする手順を説明します。

1. AEM Forms as a Cloud Service インスタンスにログインします。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。
1. アダプティブフォームを選択し、「**辞書を追加**」をクリックすると、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードが表示されます。
1. **プロジェクトタイトル**&#x200B;を指定し、**辞書を翻訳プロジェクトに追加**&#x200B;ウィザードのドロップダウンメニューから「**ターゲット言語**」を選択します。
1. 「**完了**」をクリックし、作成した翻訳プロジェクトを実行します。
1. **Forms**／**フォームとドキュメント**&#x200B;に移動します。
1. アダプティブフォームを選択し、 **HTMLとしてプレビュー** オプション。
1. Append `&afAcceptLang=<locale-name>` をプレビュー URL に移動し、Return キーを押します。 置換 `<locale-name>` 実際のロケールコードを使用します。 アダプティブフォームは指定したロケールで表示されます。

## 新しいローカライゼーションをサポートする上でのベストプラクティス {#best-practices}

* Adobeでは、アダプティブフォームの作成後に翻訳プロジェクトを作成することをお勧めします。 これにより、ローカライゼーションプロセスが合理化されます。


* 新しいフィールドの処理：

   * **機械翻訳**：機械翻訳を使用する場合は、辞書を再作成して再作成する必要があります。[翻訳プロジェクトの実行](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) 新しいフィールドを既存のアダプティブフォームに追加した後、 初回翻訳プロジェクトの後に追加された新しいフィールドは、未翻訳のままになります。

   * **人間による翻訳**：人間による翻訳のワークフローの場合、の UI を使用して辞書を書き出します。 `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. 新しいフィールド用の辞書を更新し、改訂されたバージョンをアップロードします。


## 関連トピック {#see-also}

{{see-also}}

* [アダプティブフォームにおけるレコードのドキュメントの生成](/help/forms/generate-document-of-record-core-components.md)
* [AEM Sites ページまたはエクスペリエンスフラグメントにアダプティブフォームの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

