---
title: HTML5 フォームのカスタムプロファイルの作成
description: HTML5 フォームプロファイルは Apache Sling のリソースノードです。それは HTML5 フォームレンダリングサービスのカスタマイズされたバージョンを表します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms,Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 96%

---

# HTML5 フォームのカスタムプロファイルの作成 {#creating-a-custom-profile-for-html-forms}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

プロファイルは [Apache Sling](https://sling.apache.org/) のリソースノードです。それは HTML5 フォームレンダリングサービスのカスタマイズされたバージョンを表します。HTML5 フォームレンダリングサービスを使用して、HTML5 フォームの外観、動作、インタラクションをカスタマイズできます。Profile ノードは JCR リポジトリーの `/content` フォルダーにあります。ノードは `/content` フォルダー直下か、`/content` フォルダーのサブフォルダーに入れることができます。

Profile ノードには **xfaforms/profile** のデフォルト値を持つ **sling:resourceSuperType** プロパティがあります。このノードのレンダリングスクリプトは、/libs/xfaforms/profile にあります。

Sling スクリプトは JSP スクリプトです。JSP スクリプトはリクエストされたフォームと必要な JS／CSS アーティファクトの HTML を組み立てるためのコンテナとして機能します。これらの Sling スクリプトは&#x200B;**プロファイルレンダラースクリプト**&#x200B;とも呼ばれます。プロファイルレンダラーは要求されたフォームをレンダリングするために Forms OSGi サービスを呼び出します。

GET と POST リクエストのためのプロファイルスクリプトは html.jsp と html.POST.jsp 内にあります。これらのファイルをコピーして変更することで、上書きして独自のカスタマイズを追加できます。インプレースでの変更はおこなわないでください。このような変更は、パッチのアップデートによって上書きされてしまいます。

プロファイルにはさまざまなモジュールが含まれています。これらのモジュールは、formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp、および footer.jsp です。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp モジュールには、クライアントライブラリの参照が含まれています。これは、リクエストからロケール情報を抽出し、ローカライズしたメッセージをリクエストに含めるなどのための方法も示します。formRuntime.jsp に独自のカスタム javascript ライブラリやスタイルを含めることができます。

## config.jsp {#config-jsp}

config.jsp モジュールには、ログ、プロキシサービス、動作バージョンなど、様々な設定が含まれています。独自の設定およびウィジェットカスタマイズを config.jsp モジュールに追加できます。カスタムウィジェット登録などの設定を config.jsp モジュールに追加することもできます。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp は、カラーのツールバーを作成するためのコードを含みます。ツールバーを削除するには、toolbar.jsp を HTML.jsp から削除します。

## formBody.jsp {#formbody-jsp}

formBody.jsp モジュールは、XFA フォームの HTML 表現のためのものです。

## nav_footer.jsp {#nav-footer-jsp}

最初に、HTML5 フォームはフォームの最初のページのみをレンダリングします。ユーザーがフォームをスクロールすると、フォームの残りの部分が読み込まれます。こうすることで読み込みのエクスペリエンスが高速になります。nav_footer.jsp コンポーネントには、すべてのスタイルとスクロール時のページの読み込みを支援するために必要な要素が含まれます。 

## footer.jsp {#footer-jsp}

footer.jsp モジュールは空です。これにより、ユーザーインタラクションのみに使用するスクリプトを追加できます。

## カスタムプロファイルの作成 {#creating-custom-profiles}

カスタムプロファイルを作成するには、次の手順を実行します。

### プロファイルノードの作成 {#create-profile-node}

1. URL:`https://'[server]:[port]'/crx/de` で CRX DE インターフェイスに移動し、管理者の資格情報でインターフェイスにログインします。

1. 左のペインで */content/xfaforms/profiles* に移動します。

1. default ノードをコピーし、*hrform* という名前で別のフォルダー（*/content/profiles*）にそのノードをペーストします。

1. 新しいノード、*hrform* を選択し、*hrform/demo* の値を持つ文字列プロパティ *sling:resourceType* を追加します。

1. ツールバーメニューで「すべて保存」をクリックして、変更を保存します。

### プロファイルレンダラースクリプトを作成 {#create-the-profile-renderer-script}

カスタムプロファイルの作成後、このプロファイルにレンダラーの情報を追加します。新しいプロファイルのリクエストを受け取る際に、CRX はレンダリングする JSP ページの /apps フォルダーの存在を確認します。JSP ページを /apps フォルダーに作成します。

1. 左のペインで、`/apps` フォルダーに移動します。
1. `/apps` フォルダーを右クリックして選択し、「**hrform**」という名前のフォルダーを作成します。
1. **hrform** フォルダー内で、「**demo**」という名前のフォルダーを作成します。
1. 「**すべて保存**」ボタンをクリックします。
1. `/libs/xfaforms/profile/html.jsp` に移動して、**html.jsp** のノードをコピーします。
1. **html.jsp** ノードを同じ名前「**html.jsp**」で `/apps/hrform/demo` フォルダーに貼り付けて、「**保存**」をクリックします。
1. プロファイルスクリプトのその他のコンポーネントがある場合は、手順 1 から 6 に従って、/apps/hrform/demo フォルダーにそのコンポーネントをコピーします。

1. プロファイルの作成を確認するには、URL（`https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`）を開きます。

フォームを検証するには、ローカルファイルシステムから AEM Forms に&#x200B;**フォームをインポート**&#x200B;し、AEM サーバーオーサーインスタンスで[フォームをプレビュー](/help/forms/previewing-forms.md)します。
