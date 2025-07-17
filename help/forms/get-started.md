---
title: HTML5 forms の概要
description: 開始にあたって、AEM Forms アドオンパッケージをデプロイし、既存の HTML5 フォームを AEM に読み込みます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f276d150-8936-4bfb-8475-7ca36815b233
feature: HTML5 Forms,Mobile Forms
exl-id: a3245f05-6ea3-4f90-8981-bfa89d2e7335
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 56%

---

# HTML5 forms の概要 {#getting-started-with-html-forms}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

HTML5 フォームはモバイル対応の機能を多数用意しています。HTML5 ブラウザーを使用するタブレットやスマートフォンデバイスに対して現在のソリューションとワークフローを拡張することに役立ちます。次にいくつかの機能を挙げます。

* **HTML5 ベースの XFA フォームテンプレートのレンダリング：**&#x200B;通常の PDF フォームに加え、既存の XFA ベースフォームを HTML5 形式でレンダリングできます。それはクライアントプラットフォームを HTML5 をサポートし、XFA フォームを含む Adobe Reader をサポートしないモバイルデバイス（Apple iPad、Android タブレット、スマートフォンなど）に拡張することに役立ちます。HTML5 ベースのレンダリング機能について詳しくは、[HTML5 フォームの概要](/help/forms/introductionhtml5.md)を参照してください。

* **フォームの管理：**&#x200B;さらに、AEM にはフォームの整理と管理のプロセスを簡単にする新しい機能が含まれています。フォームのアクティベート、アクティベート解除、公開、プレビューを行うことができます。<!--For more information, see [Introduction to managing forms](/help/forms/using/introduction-managing-forms.md).-->

## HTML5 forms 用の環境の設定 {#installing-html-forms}

フォーム送信およびHTML5 Formsの適切なレンダリングを有効にするには、次の手順を実行します。

* **Dispatcher フィルターを追加する：** HTML5 Formsに必要なリクエストを許可するように、`src/conf.dispatcher.d/filters/filters.any` ファイルを更新します。 次のフィルタールールを追加します。

  ```
  /0103 { /type "allow" /method '(HEAD|POST)' /url "/content/xfaforms/profiles/default.submit.html" }  # allow POSTs to form selectors under content
  /0104 { /type "allow" /method '(GET|HEAD|POST)' /url "/*.xdp.html" }
  ```

* **送信用にパッケージを追加：** フォーム送信機能をサポートするには、プロジェクトでパッケージを `src/main/content/jcr_root/content` フォルダーに追加します。

* **HTML5 Formsの読み込み：** フォームをローカルファイルシステムからAEM Formsに読み込みます。
