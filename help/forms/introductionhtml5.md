---
title: HTML5 フォームの概要
description: HTML5 forms は、Adobe Experience Manager ソフトウェアの新しい機能で、HTML5 形式の XFA フォームテンプレートをレンダリングできます。
topic-tags: hTML5_forms
feature: HTML5 Forms,Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1496d7517d586c99c5f1001fff13d88275e91d09
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 85%

---

# HTML5 フォームの概要{#introduction-to-html-forms}

<span class="preview">HTML5 Forms 機能は、早期アクセスプログラムの一部として提供されています。アクセス権をリクエストするには、公式の（勤務先の）メールアドレスから aem-forms-ea@adobe.com にメールを送信してください。
</span>

HTML5 forms は、Adobe Experience Manager ソフトウェアの新しい機能で、HTML5 形式の XFA フォームテンプレートをレンダリングできます。 この機能により、XFA ベースの PDF がサポートされていないモバイルデバイスおよびデスクトップブラウザー上のフォームのレンダリングが可能です。HTML5 フォームは、XFA フォームテンプレートの既存の機能をサポートしているだけでなく、モバイルデバイス用に手書き署名などの新しい機能もあります。

HTML5 フォームは、標準の HTML5 構造に基づいてドキュメントを生成します。HTML5 フォームは、HTML5 をサポートする現時点のすべてのブラウザーで表示できます。ブラウザー用の追加のブラウザープラグインをインストールする必要はありません。<!--For more information about supported browsers, see [Supported client platforms](https://adobe.com/go/learn_aemforms_supportedplatforms_63).-->

![HTML5 フォームプレビュー](assets/mobile_form_on_an_ipad_date_14.png)

## HTML5 フォームの主な機能 {#key-capabilities-of-html-forms-br}

* 既存の XFA フォームを、互換性のあるすべてのブラウザーでサポートされる HTML5 でレンダリングします。
* 標準の XFA フォームデザイン機能を活用して、モバイルデバイス用のフォームをターゲットにします。
* 動的 XFA 機能を HTML5 形式で使用します。
* 高精度の SVG テキストレイアウト（SVG 1.1）を使用して、PDF テキストレイアウトと一致させます。
* JavaScript および FormCalc のサポートを提供します。
* データ主導のイベントまたはユーザー入力に基づいてフラグメントをインタラクティブなフォームに動的にアセンブリします。
* 企業の基準に合わせて、フォームの外観を設定するカスタム CSS をサポートします。
* カスタムウィジェットを有効化して、豊富なデータ取得操作を提供します。
* Web アプリへの統合をサポートします。

### マルチチャネル公開 {#multichannel-publishing}

フォーム開発者は XFA テンプレートを使用して、PDF および HTML5 形式でフォームをレンダリングできます。この機能は、HTML5 フォームのデザイン実行に合わせた変更が最小限だけ必要な XFA フォームの大規模なセットがあるシナリオで有益です。XFA ベースの PDF がまだサポートされていない様々なデバイスを対象として、既存の XFA フォームを HTML5 にレンダリングできます。

## HTML5 フォームの管理 {#manage-html-forms}

また AEM は、AEM Forms UI を使用して、すべてのフォームテンプレートをリストにして管理する際に、統一された表示方法を提供します。フォームのアクティベート、アクティベート解除、公開、プレビューを行うことができます。<!--For more information, see [Introduction to managing forms](../../forms/using/introduction-managing-forms.md).-->

### フォームのカスタマイズ {#forms-customization}

HTML5 フォームは、標準 HTML5 構成を使用して、フォームテンプレートをレンダリングします。これにより、Web テクノロジ、主にCSS および JavaScript を使用した、HTML5 形式のフォームの拡張およびカスタマイズが容易になります。既存のウィジェットの外観を簡単にカスタマイズし、独自のウィジェットを作成するか、フォームのカスタムスタイルを使用できます。カスタムウィジェットの作成、および既存のウィジェットのカスタマイズについて詳しくは、[HTML5 フォームのプラグインカスタムウィジェット](/help/forms/custom-widgets.md)を参照してください。
