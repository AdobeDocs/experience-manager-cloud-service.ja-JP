---
title: HTML5 フォームのエラーメッセージのカスタマイズ
description: HTML5 フォームのエラーメッセージの表示をカスタマイズする方法（メッセージの位置や表示方法の変更を含む）について説明します。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: HTML5 Forms,Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 95%

---

# HTML5 フォームのエラーメッセージのカスタマイズ {#customizing-error-messages-for-html-forms}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

出荷時の設定の状態の HTML5 フォームでは、エラーメッセージおよび警告の位置と表示方法（フォントおよび色）は固定されており、エラーは選択したフィールドのみに、1 つだけ表示されます。

この記事では、以下のことができるように HTML5 フォームのエラーメッセージをカスタマイズする手順が説明されています。

* エラーメッセージの外観と位置を変更する手順を説明します。エラーの表示位置は、フィールドの上側、下側、または右側から選べます。
* 複数のフィールドのエラーメッセージを任意の時点で表示できます。
* フィールドが選択されているかどうかに関わらずエラーを表示できます。

## エラーメッセージのカスタマイズ {#customizing-error-messages-nbsp}

エラーメッセージをカスタマイズする前に、添付のパッケージ（CustomErrorManager-1.0-SNAPSHOT.zip）をダウンロードして解凍します。

パッケージを抽出したら、CustomErrorManager-1.0-SNAPSHOT フォルダーを開きます。jcr_root および META-INF フォルダーが含まれます。これらのフォルダーには、エラーメッセージのカスタマイズに必要な CSS ファイルと .JS ファイルが含まれています。

[ファイルを入手](assets/customerrormanager-1.0-snapshot.zip)

### エラーメッセージの位置のカスタマイズ {#customizing-the-position-of-error-messages-nbsp}

エラーメッセージの位置をカスタマイズするには、それぞれのエラーおよび警告フィールドに対して &lt;div> タグを追加し、&lt;div> タグを左側または右側に配置して、&lt;div> タグに CSS スタイルを適用します。詳しくは、以下に示す手順を参照してください。

1. `CustomErrorManager-1.0-SNAPSHOT` フォルダーに移動し、`etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` フォルダーを開きます。
1. `customErrorManager.js` ファイルを編集用として開きます。ファイル内の `markError` 関数は、次のパラメーターを受け付けます。

   |   |  |
   |---|---|
   | jqWidget | jqWidget はウィジェットのハンドルです |
   | msg | エラーメッセージを格納します |
   | type | エラーか警告かを示します |

1. 出荷時の設定での実装では、エラーメッセージはフィールドの右側に表示されます。エラーメッセージを上側に表示するには、次のコードを使用します。

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. ファイルを保存して閉じます。
1. `CustomErrorManager-1.0-SNAPSHOT` フォルダーに移動し、jcr_root フォルダーと META-INF フォルダーのアーカイブを作成します。アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージマネージャーを使用し、パッケージをアップロードしてインストールします。

## 複数のフィールドのエラーメッセージを表示 {#display-error-messages-for-multiple-fields-nbsp}

すべてのフィールドのエラーメッセージを同時に表示するには、添付されているパッケージを使用します。エラーメッセージを単独で表示するには、デフォルトのプロファイルを使用します。

### エラーメッセージの表示方法のカスタマイズ  {#customizing-the-appearance-of-error-messages-nbsp}

1. etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css フォルダーに移動します。

1. sample.css ファイルを開いて編集します。CSS ファイルには、#customError と #customWarning の 2 つの ID が含まれています。これらの ID を使用して、色やフォントサイズなどの様々なプロパティを変更できます。

   次のコードを使用して、エラーメッセージや警告メッセージのフォントサイズと色を変更します。

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. ファイルを保存して閉じます。
1. CustomErrorManager-1.0-SNAPSHOT フォルダーに移動し、jcr_root および META-INF フォルダーのアーカイブを作成します。アーカイブの名前を CustomErrorManager-1.0-SNAPSHOT.zip に変更します。
1. パッケージマネージャーを使用し、パッケージをアップロードしてインストールします。

## 新しいプロファイルでフォームをレンダリングします。  {#render-the-form-with-the-new-profile-nbsp}

出荷時の設定では、HTML5 フォームはデフォルトのプロファイル `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;` を使用します。

カスタムエラーメッセージを含むフォームを表示するには、`https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;` のエラープロファイルを含むフォームをレンダリングします。

>[!NOTE]
>
>エラープロファイルは、添付されているパッケージによりインストールされます。
