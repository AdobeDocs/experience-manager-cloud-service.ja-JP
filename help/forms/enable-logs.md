---
title: HTML5 フォーム内でのログの有効化
description: ロガーユーティリティはフォームのログを可能にし、フォーム関連の問題のデバッグに役立ちます。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 96%

---

# HTML5 フォーム内でのログの有効化{#enable-logging-for-html-forms}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

ロガーユーティリティを設定することで、HTML5フォームでログの作成を開始することができます。ロガーユーティリティにはいくつかのレベルがあり、要件に応じてレベルを設定することができます。HTML5 フォームは、サーバーコンポーネントとクライアントコンポーネントから構成されています。両方のコンポーネントに対してログを設定できます。 

## サーバーサイドのログの設定 {#configuring-server-side-logging}

次の手順を実行して、サーバー側のログを設定します。

1. `https://'[server]:[port]'/system/console/configMgr` に移動します。*Apace Sling ロギングロガー設定* オプションを探して開きます。ダイアログボックスが表示されます。

   ![Apace Sling ロギングのロガー設定オプションのダイアログボックス](assets/logconfig.png)

   Apace Sling ロギングロガー設定オプション

1. **ログレベル**&#x200B;を&#x200B;**デバッグ**&#x200B;に変更します。 

1. **ログファイル**&#x200B;のパスと名前を指定します。

   >[!NOTE]
   >
   >HTML5 Forms ログディレクトリ内にログを生成する場合は、ファイル名の前に ../logs/ を追加します。

1. **ロガー**&#x200B;を **HTMLFormsPerfLogger** に変更します。「**保存**」をクリックします。

## クライアントログの設定 {#configuring-client-logging}

次の方法により、HTML5 フォームのクライアント側のログを有効にできます。

* `log` という名前の要求パラメーターの使用
* CQ Configuration Manager の使用

### リクエストパラメーターの使用によるログの有効化 {#enabling-logging-using-request-parameter}

この方法を使用して、特定のリクエストに対するログを生成できます。リクエストパラメーター名は `log` です。ログ URL は次のとおりです。

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

ログの設定はログレベルとロガーカテゴリで構成されています。

#### ログの宛先 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>ログの宛先</strong></th>
   <th><strong>説明</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>ログはブラウザーの<strong>コンソール</strong>に送信されます。</td>
  </tr>
  <tr>
   <td>2</td>
   <td>ログはクライアント側の JavaScript オブジェクトに収集され、<strong>サーバー</strong>にポストできます。 </td>
  </tr>
  <tr>
   <td>3</td>
   <td>両方の上記のオプション<br /> </td>
  </tr>
 </tbody>
</table>

#### ログレベル {#log-levels}

<table>
 <tbody>
  <tr>
   <th>ログレベル</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>0</td>
   <td>オフ<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>1</td>
   <td>重大<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>エラー <br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>警告<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>情報<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>デバッグ<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>トレース<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>すべて<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### ロガーカテゴリ {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>ログカテゴリ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>a</td>
   <td>xfa （スクリプティングエンジン関連ログ）</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView （レイアウトエンジン関連ログ）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf （パフォーマンス関連ログ）<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### ログの設定 {#log-configuration}

ログ URL では、ログ設定クエリの文字列パラメーターは次のとおりに定義します。

`{destination}-{a level}-{b level}-{c level}`

次に例を示します。

<table>
 <tbody>
  <tr>
   <th>ログの設定</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>保存場所：サーバー<br /> xfa レベル：情報<br /> xfaView レベル：デバッグ<br /> xfaPerf レベル：トレース</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>a（xfa）、b（xfaView）、および c（xfaPerf）のそれぞれのログカテゴリに対するデフォルトログレベルは 2（エラー）です。そのため、ログ設定 2-b6 では、異なるカテゴリのログレベルは：
>>a（xfa）：2（デフォルトレベルのエラー）
>>b（xfaView）：6（ユーザー指定トレース）
>>a（xfaPerf）：2（デフォルトレベルのエラー）

### Configuration Manager の使用によるログの有効化 {#enabling-logging-using-configuration-manager}

ログを有効化するために Configuration Manager を使用すると、ログが再び無効化されるまで、すべてのレンダリング要求に対してログが生成されます。

1. CQ Configuration Manager に `https://'[server]:[port]'/system/console/configMgr` でログインし、管理者の資格情報でログインしてください。
1. **Mobile Forms の設定**&#x200B;を探してクリックします。
1. 「デバッグオプション」テキストボックスで、前のセクションで説明されたとおりにログ設定を入力します。例：**2-a4-b5-c6**

   ![Forms 設定](assets/forms_configuration.png)

   Forms 設定

## ログのアップロード {#uploading-logs}

宛先が 1 として設定されている場合、すべてのクライアントスクリプトのログメッセージはコンソールに送信されます。管理者がサーバーログと供にこれらのログを必要とする場合は、出力先レベルを 2 に設定します。このレベルでは、すべてのログはクライアント側の JS オブジェクトに収集されて、フォームがデフォルトプロファイルでレンダリングされる場合、ツールバーの&#x200B;**既存のフィールドのハイライト**&#x200B;ボタンの左に&#x200B;**ログを送信**&#x200B;ボタンが表示されます。ユーザーがリンクをクリックすると、収集されたすべてのログはサーバーに投稿され、サーバー上の設定されたエラーログファイルに記録されます。

デフォルトでは、すべての情報が /crx-repository/logs/ ディレクトリに保存されている error.log ファイルに追加されます。

ログファイルの場所と名前を変更するには、次の操作を実行します。

1. 管理者として「 Configuration Manager」にログインします。Configuration Manager のデフォルトの URL は、`https://'[server]:[port]'/system/console/configMgr` です。
1. 「**Apache Sling Logging Logger Configuration**」をクリックします。ダイアログボックスが表示されます。

   ![logconfig-1](assets/logconfig-1.png)

1. **ログレベル**&#x200B;をデバッグに変更します。 

1. **ログファイル**&#x200B;のパスと名前を指定します。

   >[!NOTE]
   >
   >他のログファイルが保存されている同じディレクトリにログを作成するには、Log Files プロパティで ../logs/&lt;filename> を指定します。

1. **Logger** を **HTMLFormsPerfLogger** に変更し、「**保存**」をクリックします。
