---
title: 翻訳統合フレームワークの設定
description: サードパーティの翻訳サービスと統合するためのTranslation Integration Frameworkの設定方法を説明します。
translation-type: tm+mt
source-git-commit: 66b2fb19cbc4c8aa480f1ace31a7f973dc7fb0f7
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 41%

---


# 翻訳統合フレームワークの設定 {#configuring-the-translation-integration-framework}

翻訳統合フレームワークは、AEM コンテンツの翻訳を組織化するためにサードパーティの翻訳サービスと統合されます。3つの基本的な手順が必要です。

1. [翻訳サービスプロバイダーに接続します。](#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定を作成します。](#creating-a-translation-integration-configuration)
1. [クラウド設定をページに関連付けます。](#configuring-pages-for-translation)

AEMのコンテンツ翻訳機能の概要については、[多言語サイト用のコンテンツの翻訳](overview.md)を参照してください。

## 翻訳サービスプロバイダーへの接続 {#connecting-to-a-translation-service-provider}

AEM を翻訳サービスプロバイダーに接続するためのクラウド設定を作成します。AEMには、デフォルトで[Microsoft Translator](connect-ms-translator.md)に接続する機能が含まれています。

以下の翻訳ベンダーは、翻訳プロジェクト用のAEM APIの実装を提供しています。

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (Adobe交換プレミアパートナー)
* [Clayタブレットテクノロジ](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [CrossLang NV](https://exchange.adobe.com/experiencecloud.details.90049.crosslang-xtm-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)

コネクターパッケージをインストールしたら、コネクター用のクラウド設定を作成できます。通常は、翻訳サービスで認証をおこなうための資格情報を指定する必要があります。Microsft Translator コネクター用のクラウド設定の追加については、[Microsoft Translator との統合](connect-ms-translator.md)を参照してください。

必要に応じて、同じコネクターに対して複数のクラウド設定を作成できます。例えば、同じベンダーを使用するアカウントまたはプロジェクトごとに設定を 1 つずつ作成します。

接続の設定が完了したら、その接続を使用する翻訳統合フレームワーク設定を作成できます。

## 翻訳統合フレームワーク設定の作成  {#creating-a-translation-integration-configuration}

翻訳統合フレームワーク設定を作成して、コンテンツの翻訳方法を指定します。この設定には以下の情報が含まれます。

* 使用する翻訳サービスプロバイダー
* 人による翻訳か機械による翻訳か
* タグなど、ページまたはアセットに関連付けられている他のコンテンツを翻訳するかどうか

フレームワーク設定を作成したら、その設定に従って、翻訳するページにクラウド設定を関連付けます。翻訳プロセスが開始すると、関連付けられているフレームワーク設定に従って翻訳ワークフローが進行します。

Web サイトのセクションごとに翻訳要件が異なる場合は、それに応じて複数のフレームワーク設定を作成します。例えば、多言語のWebサイトには、英語、スペイン語、日本語のコピーが含まれる場合があります。 サイトの所有者は、スペイン語と日本語の翻訳のために 2 つの異なる翻訳サービスプロバイダーを使用します。そのため、フレームワークの設定が 2 つ指定されます。使用する翻訳サービスプロバイダーは設定ごとに異なります。

翻訳統合フレームワークを設定したら、それを使用するページ](preparation.md)に[関連付けることができます。

>[!TIP]
>
>AEMのコンテンツ翻訳機能の概要については、[多言語サイト用のコンテンツの翻訳](overview.md)を参照してください。

フレームワークの単一の設定によって、ページのコンテンツとアセットの変換方法が制御されます。

![翻訳の設定](../assets/translation-configuration.png)

新しい翻訳設定を作成するには：

1. [グローバルナビゲーションメニューで、](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)**ツール/>Cloud Services/翻訳Cloud Services**&#x200B;をクリックまたはタップします。
1. コンテンツ構造内で設定を作成する場所に移動します。 これは多くの場合、特定のサイトに基づいているか、グローバルにすることができます。
1. フィールドに次の情報を入力し、「**作成**」をクリックまたはタップします。
   1. ドロップダウンで&#x200B;**Configuration Type**&#x200B;を選択します。
   1. 設定の&#x200B;**タイトル**&#x200B;を入力します。 **タイトル**&#x200B;は、**Cloud Services**&#x200B;コンソールの設定と、ページのプロパティのドロップダウンリストを示します。
   1. 必要に応じて、設定を保存するリポジトリノードに使用する&#x200B;**名前**&#x200B;を入力します。
1. **設定を編集**&#x200B;ウィンドウで、「**サイト**」タブと「**アセット**」タブのプロパティを設定し、「**保存して閉じる**」をクリックまたはタップします。

### 「サイト」の設定プロパティ{#sites-configuration-properties}

「**サイト**」タブは、ページコンテンツの翻訳の実行方法を制御します。

| プロパティ | 説明 |
|---|---|
| 翻訳ワークフロー | このプロパティは、フレームワークがサイトコンテンツに対して実行する翻訳方法を定義します。<br> — 機械翻訳：翻訳プロバイダは、リアルタイムに機械翻訳を用いて翻訳を行う。<br> — 人による翻訳：翻訳者が翻訳するコンテンツが翻訳プロバイダーに送信されます。<br> — 翻訳しない：コンテンツは翻訳用に送信されません。翻訳されないものの、最新のコンテンツに更新される可能性があるコンテンツのブランチをスキップする場合に使用します。 |
| 翻訳プロバイダー | このプロパティは、翻訳を実行する翻訳プロバイダーを定義します。 対応するコネクタが取り付けられると、リストにプロバイダが表示されます。 |
| コンテンツのカテゴリ | （機械翻訳のみ）このプロパティは、翻訳するコンテンツを説明するカテゴリです。 カテゴリは、コンテンツを翻訳する際の用語や言葉遣いの選択を左右します。 |
| タグを翻訳 | このオプションを選択すると、ページに関連付けられているタグを翻訳できます。 |
| ページのアセットを翻訳 | このプロパティは、ファイルシステムからコンポーネントに追加されたアセット、またはアセットから参照されたアセットを変換する方法を定義します。<br> — 変換しない：ページアセットは翻訳されません。<br> — サイト翻訳ワークフローの使用：アセットは、「サイト」タブの設定プロパティに従って処理され **** ます。<br> — アセット翻訳ワークフローを使用する：アセットは、「アセット」タブで設定されたプロパティに従って処理され **** ます。 |
| 翻訳を自動実行 | 翻訳プロジェクトの作成後に翻訳ジョブを自動的に実行するには、このプロパティを有効にします。 このオプションを選択すると、翻訳ジョブのレビューやスコーピングをおこなう機会はなくなります。 |

### 「アセット」の設定プロパティ{#assets-configuration-properties}

アセットプロパティは、アセットの設定方法を制御します。アセットの変換について詳しくは、[アセットの言語コピーの作成](/help/assets/translate-assets.md)を参照してください。

| プロパティ | 説明 |
|---|---|
| 翻訳ワークフロー | このプロパティは、フレームワークがアセットに対して実行する翻訳の種類を選択します。<br> — 機械翻訳：翻訳プロバイダは、機械翻訳を用いて直ちに翻訳を行う。<br> — 人による翻訳：コンテンツは翻訳プロバイダーに自動的に送信され、手動で翻訳されます。<br> — 翻訳しない：アセットは翻訳用に送信されません。 |
| 翻訳プロバイダー | このプロパティは、翻訳を実行する翻訳プロバイダーを定義します。 対応するコネクタが取り付けられると、リストにプロバイダが表示されます。 |
| コンテンツのカテゴリ | （機械翻訳のみ）このプロパティは、翻訳するコンテンツを説明します。 カテゴリは、コンテンツを翻訳する際の用語や言葉遣いの選択を左右します。 |
| アセットを翻訳 | 翻訳プロジェクトにアセットを含めるには、このプロパティをアクティブにします。 |
| メタデータを翻訳 | アセットのメタデータを変換するには、このプロパティをアクティブ化します。 |
| タグを翻訳 | アセットに関連付けられているタグを変換するには、このプロパティをアクティブにします。 |
| 翻訳を自動実行 | 翻訳プロジェクトの作成後に翻訳ジョブを自動的に実行するには、このプロパティを選択します。 このオプションを選択すると、翻訳ジョブのレビューやスコーピングをおこなう機会はなくなります。 |

## 翻訳するページの設定 {#configuring-pages-for-translation}

ソースページを他の言語に翻訳するように設定するには、そのページを次のクラウド設定に関連付けます。

* AEM を翻訳サービスプロバイダーに接続するためのクラウド設定
* 翻訳の詳細を設定する翻訳統合フレームワーク

翻訳統合フレームワークのクラウド設定によって、サービスプロバイダーへの接続に使用するクラウド設定が特定されます。ソースページをフレームワークのクラウド設定に関連付ける場合は、フレームワークのクラウド設定が使用するサービスプロバイダーのクラウド設定にページを関連付ける必要があります。

ページをクラウド設定に関連付ける場合は、そのページの子ページが関連付けを継承します。例えば、`/content/wknd/language-masters/en/magazine`ページを翻訳統合フレームワークに関連付けた場合、`magazine`ページとその下の子ページはフレームワークに従って翻訳されます。

必要に応じて、子ページの関連付けを上書きできます。例えば、Webサイトのコンテンツは主に旅行とライフスタイルに関するものです。 しかし、ページの 1 つのブランチには企業の説明が記述されています。この場合、サイトのルートページは、ライフスタイルカテゴリを使用して機械翻訳を指定するTranslation Integration Frameworkに関連付けられ、会社を説明する分岐は、一般カテゴリを使用して機械翻訳を実行するフレームワークを使用します。

### 翻訳プロバイダーへのページの関連付け {#associating-a-page-with-a-translation-provider}

ページおよび子ページの翻訳に使用する翻訳プロバイダーにページを関連付けます。

1. サイトコンソールで、設定するページを選択し、「**表示のプロパティ**」をクリックまたはタップします。
1. 「**Cloud Services**」タブをクリックまたはタップします。
1. **追加設定**&#x200B;ドロップダウンで、設定を選択します。
1. 「**保存して閉じる**」をクリックまたはタップします。

### 翻訳統合フレームワークへのページの関連付け {#associating-pages-with-a-translation-integration-framework}

ページおよび子ページの翻訳を実行する方法を定義する翻訳統合フレームワークにページを関連付けます。

1. サイトコンソールで、設定するページを選択し、「**表示のプロパティ**」をクリックまたはタップします。
1. 「**Cloud Services**」タブをクリックまたはタップします。
1. **追加設定**&#x200B;ドロップダウンで、設定を選択します。
1. 「**保存して閉じる**」をクリックまたはタップします。
