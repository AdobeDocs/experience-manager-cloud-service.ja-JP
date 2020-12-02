---
title: DHTML ビューアのサポート終了に関する FAQ
description: 2014 年 1 月 31 日をもって、Scene7 の DHTML ビューアプラットフォームは正式にサポート終了となります。このページでは、新しい HTML5 ビューアプラットフォームへの移行に備えて、よくある質問にお答えします。
translation-type: tm+mt
source-git-commit: 24d929702fd9eb31b95fdd6d97c7b9978d919804
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 97%

---


# DHTML ビューアのサポート終了に関する FAQ{#dhtml-viewer-end-of-life-faqs}

2014 年 1 月 31 日をもって、Scene7 の DHTML ビューアプラットフォームは正式にサポート終了となります。このページでは、新しい HTML5 ビューアプラットフォームへの移行に備えて、よくある質問にお答えします。

**何が変わるのですか？**

Scene7 は、DHTML ビューアプラットフォームのサポートを 2014 年 1 月 31 日に正式に終了します。

**サポート終了とはどういうことですか？**

サポート終了とは、Scene7 が（1）DHTML ビューアプラットフォームに機能改良を追加しなくなる、（2）DHTML ビューアプラットフォームのバグ修正に対応またはリリースしなくなる、（3）カスタマーケアが DHTML に関連するビューアの問題や質問に対するトラブルシューティングまたはサポート提供をおこなわなくなることを意味します。

**なぜそのように変わるのですか？**

Web 標準は日々進化しています。DHTML は比較的古い Web 開発テクノロジーであり、HTML5 への置き換えが急速に進んでいます。プラットフォームとしての DHTML の最大の制限は、リッチなエクスペリエンスへの対応にあります。HTML5 ならば、クロスブラウザーの一貫したリッチなエクスペリエンスを容易にサポートできますが、DHTML では困難です。例えば、DHTML では以下の機能をクロスブラウザーでサポートできません。

* カスタムカーソル
* 角丸
* アニメーション（ページの反転、ズームのイージングなど）
* エフェクト（シャドウ、グローなど）
* すべてのフォントのサポート
* プラグインを使用しないビデオ再生

Scene7 の DHTML ビューアプラットフォームに固有の問題としては、JSP ベースのソリューションと JavaScript API はどちらも、モバイルデバイスのマルチタッチ機能とジェスチャー機能を利用できるように最適化されていませんでした。また、2011 年から 2012 年前半にリリースされた DHTML ビューアは、モバイル向けに最適化されていても、柔軟な SDK コンポーネントベースの開発フレームワークがないので、カスタマイズや保守が困難でした。

DHTML に関するこのような制限や、デスクトップとモバイルにまたがる新たな標準として HTML5 が業界で急速に注目を集めている点を考慮して、Scene7 では HTML5 ベースのビューアプラットフォームに注力することになりました。この新しいプラットフォームは、デスクトップ、iOS および Android デバイスなど様々な画面で利用できる、よりリッチで魅力的なインタラクティブビューアを構築するための堅牢な基盤となります。

**現在のビューアが DHTML プラットフォームを使用しているかどうかはどうすればわかりますか？**

現在使用しているビューアが DHTML かどうか、そして今回の変更によって影響を受けるかどうかを判断するには、次の点を確認してください。

1. 次の表で「ビューアテクノロジー」が「DHTML」と表示されている標準提供の Scene7 ビューアを使用している。

   [https://help.adobe.com/ja_JP/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/ja_JP/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 次の表で「ビューアテクノロジー」が「DHTML」と表示されている標準提供の Scene7 ビューアをベースとして、新しいプリセットとして作成されたビューアを使用している。

   [https://help.adobe.com/ja_JP/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. JSP ベースの DHTML ソリューションから作成されたカスタムビューアを使用している。

   [https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#JSP_Reference)

1. JavaScript API から作成されたカスタムビューアを使用している。

   [https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#API_Reference)

1. DHTML マルチスクリーンフライアウト API を使用して作成されたカスタムビューアを使用している。

   [https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. DHTML デスクトップフライアウト API を使用して作成されたカスタムビューアを使用している。

   [https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. DHTML ビューアパッケージに含まれるデバイス検出ライブラリを使用している。

   コード内の &quot;sj_deviceDetect.js&quot; という JS インクルードを探してください。

   これは、新しい JS デバイス検出コード（[https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Detecting_devices_and_browsers)）に置き換えられました。

**代わりとなるビューアプラットフォームはどのようなものですか？**

DHTML の代わりとなる Scene7 HTML5 ビューアプラットフォームは、以下のものから構成されます。

* 標準提供の HTML5 ビューア。これらのビューアは、様々なビューアタイプにまたがって最適化された、基本ズーム、フライアウトズーム、画像セット、スウォッチセット、多次元スピン、混在メディアなどのモバイルインタラクションに対応しています。このようなビューアの最新の例については、[https://microsite.omniture.com/t2/help/ja_JP/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/ja_JP/s7/vlist/vlist.html) を参照してください。
* HTML5 ビューア SDK。この SDK は、Adobe Scene7 ビューアを HTML5 対応のサイトおよびデバイス（iOS や Android など）向けに大幅にカスタマイズし、ビューアの外観と双方向性を際立たせるための強力な柔軟性と創造性をもたらします。再利用可能でパフォーマンスが最適化されたコンポーネントを使用することで、ビューア開発全体のコストを低減し、カスタム開発を促進できます。

**DHTML ビューアプラットフォームから移行するために必要な機能は、いつ HTML5 ビューアプラットフォームに搭載されますか？**

Scene7 は初の HTML5 ビューア SDK を 2011 年秋にバージョン 5.5 と共にリリースしました。それ以降、このプラットフォームには多数の機能が追加され、サポートされるビューアの種類も増えています。ごく一般的なビューア要件であれば、HTML5 ビューアプラットフォームはすぐに移行する場合に必要な機能を既に備えていると考えられます。アドビは今後も四半期ごとのリリースで、このビューアプラットフォームを積極的に拡張していく予定です。

現在の HTML5 ビューアプラットフォームでビューア要件を満たせるかどうかを判断するには、以下のドキュメントを参照してください。

[https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#About_HTML5_Viewers)（標準提供のビューア機能とカスタマイズ機能について）

[https://help.adobe.com/ja_JP/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/ja_JP/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html)（SDK API ドキュメントにアクセスする方法）

それでも HTML5 ビューア SDK が要件を満たせるかどうか判断できない場合は、アドビのプロフェッショナルサービスチームにお問い合わせください。

**ビューアを HTML5 プラットフォームに移行するにはどうすればいいですか？**

ビューアを HTML5 プラットフォームに移行するには、次の選択肢があります。

1. Scene7 の標準提供 HTML5 ビューアのいずれかを使用する。ビューアの例については、[https://microsite.omniture.com/t2/help/ja_JP/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html) を参照してください。
1. SPS アプリケーションの設定に従って、Scene7 の標準提供 HTML5 ビューアのいずれかを設定する。これにより、ビューアのサイズ、トランジション、ズームなどの動作をカスタマイズできます。[https://help.adobe.com/ja_JP/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/ja_JP/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. CSS を編集してボタンのアートワーク、配置、透過性、背景色などのビジュアルデザインを変更することによって、Scene7 の標準提供 HTML5 ビューアのルックアンドフィールをカスタマイズする。[https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/ja_JP/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. SDK を使用してカスタム HTML5 ビューアを最初から作成する。SDK は、[https://help.adobe.com/ja_JP/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) からダウンロードできます。プロフェッショナルサービスを利用してカスタムビューアを作成したり、社内の Web 開発チームにカスタムビューアを作成させることができます。

**HTML5 をサポートしていないブラウザーはどうなりますか？**

HTML5 は多くのモバイルデバイスと Web ブラウザーでサポートされており、現在もサポート範囲が広がっています。本来、バージョン 8 以前の Internet Explorer は HTML5 をサポートしていませんが、Scene7 の HTML5 ビューアプラットフォームでは、IE 7 および IE 8 でも HTML5 をサポートできます。Scene7 の HTML5 ビューアプラットフォームを使用すると、単一の開発プラットフォームで、圧倒的多数のデスクトップユーザーとモバイルユーザーにリーチできます。

HTML5 SDK バージョン 2.2.1 の現在の必要システム構成は、以下のとおりです。

* Microsoft® Windows® XP 以降、Macintosh® OS X 10.6 以降
* Firefox 17、Safari 5.1、Chrome 23、Internet Explorer 7 以降
* iOS 3.2.2 以降
* iPhone3 以降および iPad1 以降（ネイティブブラウザー）で認定済み
* Android OS 2.2 以降

お使いのブラウザーにアドビの HTML5 ビューアプラットフォームとの互換性があるかどうかを確認するには、次のサンプルビューアを起動してください。

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

メイン画像の上にマウスカーソルを置くか、指でドラッグしたときに、ズームインした画像が表示される場合は、そのブラウザーまたはデバイスは互換性を持っています。

**既存の DHTML ビューアを実稼動環境で引き続き利用する場合は、どのような選択肢がありますか？**

DHTML ベースのビューアを実稼動環境で引き続き利用していただくことは可能ですが、2014 年 1 月 31 日以降は、機能強化、バグ修正、カスタマーケアがなくなることにご注意ください。そのため、より堅牢な HTML5 ビューアプラットフォームに移行することをすべてのお客様に強くお勧めします。ただし、ビジネス状況によってサポート終了日までに移行できない場合は、プロフェッショナルサービスに連絡して、サポート対象の保守期間を延長することができます。詳しくは、アカウントマネージャーにお問い合わせください。

**詳細についての問い合わせ先を教えてください。**

このFAQが全ての質問に回答しなかった場合は、[Admin Consoleを使ってサポートケース](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)を作成するか、Adobeのアカウントマネージャーにお問い合わせください。
