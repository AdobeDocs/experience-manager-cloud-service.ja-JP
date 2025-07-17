---
title: HTML5 フォームのデバッグ
description: このドキュメントでは、様々な既知の問題をトラブルシューティングするための手順をリストしています。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: HTML5 Forms,Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 100%

---

# HTML5 フォームのデバッグ {#debugging-html-forms}

このドキュメントには様々なトラブルシューティングのシナリオが含まれています。各シナリオにつき、問題をトラブルシューティングするためにいくつかの手順が提供されています。次の手順を実行しても、引き続き問題が発生する場合は、ロガーを設定してエラーや警告のログを取得し、確認します。HTML5 フォームのロギングについて詳しくは、[HTML5 フォームのログの生成](/help/forms/enable-logs.md)を参照してください。

## 問題：フォームをレンダリングすると、org.apache.sling.api.SlingException 例外ページが表示される {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

例外詳細で、「**caused by**」という語句を検索します。

推定原因は、URL にある 1 つ以上のパラメーターが間違っていることです。

次のパラメーターを確認します。

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>テンプレート</td>
   <td>テンプレートのファイル名</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>テンプレートと関連リソースが存在するパス</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>テンプレートと結合されているデータファイルの絶対パス。<br />メモ：パスはデータファイルの絶対パスを定義します。</td>
  </tr>
  <tr>
   <td>データ</td>
   <td>テンプレートと結合される UTF-8 でエンコードされたデータバイト。</td>
  </tr>
 </tbody>
</table>

## 問題：フォームをレンダリングできない（エラーメッセージが表示される） {#problem-unable-to-render-form}

1. 指定したパラメーターが正しいことを確認します。パラメーター関する詳しい情報については、[パラメーターのレンダリング](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page)を参照してください。
1. https://&lt;server>:&lt;port>/crx/packmgr/index.jsp で CRX パッケージマネージャーにログインし、以下のパッケージが正しくインストールされているかどうか確認します。

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. https://&lt;server>:&lt;port>/system/console/bundles で CQ web コンソール（Felix コンソール）にログインします。

   次のバンドルのステータスが「アクティブ」であることを確認します。

   * scala-lang.bundle [osgi]

   （com.adobe.livecyclescala-lang.bundle）

   * Adobe XFA Forms Renderer

   （com.adobe.livecycle.adobe-lc-forms-core）

   * Adobe XFA Forms LC Connector

   （com.adobe.livecycle.adobe-lc-forms-lc-connector）

## 問題：フォームがスタイルなしでレンダリングされる {#problem-form-renders-without-styles}

1. お使いのブラウザーで、**開発ツール**&#x200B;を開きます。profile.css が存在することを確認します。
1. profile.css ファイルが存在しない場合は、https://&lt;server>:&lt;port>/crx/de で CRX DE にログインします。
1. 左のフォルダー階層で、/etc/clientlibs/fd/xfaforms/ に移動します。フォルダーにリストされている css.txt ファイルを開きます。

   * プロファイル
   * runtime
   * scrollnav
   * ツールバー
   * xfalib

1. css.txt 内に記載されているファイルが /libs/fd/xfaforms/clientlibs/xfalib/css の CRX DE lite 内に存在することを確認します。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. これらのファイルがない場合、adobe-lc-forms-runtime-pkg-&lt;version>.zip パッケージを再びインストールします。

### 問題：予期しないエラーが発生した {#problem-unexpected-error-encountered}

1. フォームの URL にクエリーパラメーター「debugClientLibs」を追加し、その値を「true」に設定します（例：https://&lt;サーバー>:&lt;ポート>/content/xfaforms/profiles/test.html?contentRoot=&lt;パス>&amp;template=&lt;xdp ファイル名>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true）
1. Chrome のようなデスクトップブラウザーでデベロッパーツール／コンソールに移動します。
1. ログを開いて、エラーのタイプを特定します。ログについて詳しくは、[HTML5 フォームのログ](/help/forms/enable-logs.md)を参照してください。
1. デベロッパーツール／コンソールに移動します。スタックトレースを使用して、エラーの原因となっているコードを探します。エラーをデバッグして問題を解決します。

   >[!NOTE]
   >
   >スクリプティングの失敗の場合は、フォームの PDF レンダリングでも問題が発生するかを確認します。発生する場合は、フォームスクリプティングのロジックに問題があります。

## 問題：フォームを送信できない {#problem-unable-to-submit-the-form}

1. AEM サーバーにアクセスする権限を持っていること、およびサーバーに接続されていることを確認します。
1. パラメーター submitUrl が正しいことを確認します。
1. **1-a5-b5-c5** をデバッグオプションとして使用し、[HTML5 フォームのログ](/help/forms/enable-logs.md)に記載されている通りにクライアントサイドログを有効にします。次に、フォームをレンダリングし、送信をクリックします。ブラウザーのデバッグコンソールを開き、エラーがあるかどうかを確認します。
1. [HTML5 フォームのログ](/help/forms/enable-logs.md)に記載されている通りに、サーバーログを見つけます。サーバーログで送信の際にエラーが発生したかを確認します。

## 問題：ローカライズされたエラーメッセージが表示されない {#problem-localized-error-messages-do-not-display}

1. デスクトップブラウザーで、追加のクエリパラメーター **debugClientLibs=true** でフォームをレンダリングしてから、デベロッパーツール／リソースに移動して、I18N.css のファイルの存在を確認します。
1. ファイルが存在しない場合は、https://&lt;サーバー>:&lt;ポート>/crx/de で CRX DE にログインします。
1. 左のフォルダー階層で /libs/fd/xfaforms/clientlibs/I18N に移動し、次のファイルとフォルダーが存在することを確認します。

   * Namespace.js
   * LogMessages.js
   * 言語用のフォルダー

1. 上記のファイルまたはフォルダーで存在しないものがある場合は、**adobe-lc-forms-runtime-pkg-&lt;version>.zip** パッケージを再度インストールします。
1. ロケールの名前と同じ名前のフォルダーに移動し、そのコンテンツを確認します。フォルダーには次のファイルが含まれている必要があります。

   * I18N.js
   * js.txt

1. js.txt のコンテンツを確認して、次のエントリがあることを確かめます。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：画像が表示されない {#problem-image-not-showing-up}

1. 画像 URL が正しいことを確認します。
1. ブラウザーがこのタイプの画像をサポートしているかどうかを確認します。
1. 例外詳細で、「**caused by**」という語句を検索します。

   推定原因は、URL にある 1 つ以上のパラメーターが間違っていることです。

   次のパラメーターを確認します。
ステップテキスト

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>テンプレート</td>
   <td>テンプレートのファイル名</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>テンプレートと関連リソースが存在するパス</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>テンプレートと結合されているデータファイルの絶対パス。<br />メモ：パスはデータファイルの絶対パスを定義します。</td>
  </tr>
  <tr>
   <td>データ</td>
   <td>テンプレートと結合される UTF-8 でエンコードされたデータバイト。</td>
  </tr>
 </tbody>
</table>

1. デスクトップブラウザーで、デベロッパーツール／リソースに移動します。

   画像が表示される場合は、左側で「フレーム」を確認します。
