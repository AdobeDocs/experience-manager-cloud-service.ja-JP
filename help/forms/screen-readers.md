---
title: HTML5 フォーム向けのスクリーンリーダー
description: HTML5 フォームでサポートされるスクリーンリーダーを一覧表示します。
content-type: reference
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1496d7517d586c99c5f1001fff13d88275e91d09
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 100%

---

# HTML5 フォーム向けのスクリーンリーダー {#screen-readers-for-html-forms}

<span class="preview">HTML5 Forms 機能は、早期アクセスプログラムの一部として提供されています。アクセス権をリクエストするには、公式の（勤務先の）メールアドレスから aem-forms-ea@adobe.com にメールを送信してください。
</span>

HTML5 フォームコンポーネントは、XFA フォームテンプレートを HTML5 形式にレンダリングします。これらのフォームは、HTML5 をサポートするすべての標準ブラウザーでレンダリングできます。PDF フォームおよび HTML5 フォームで同様のデータキャプチャエクスペリエンスをサポートするために、PDF forms のレイアウトは HTML5 フォームでも保持されます。

HTML5 フォームは標準の HTML 構成を使用し、これらのフォームで HTML の通常のアクセシビリティツールを使用できます。アクセシブルなフォームのベストプラクティスに従ってデザインされたフォームは、サポートされているスクリーンリーダーで動作します。また、このようなフォームはキーボード操作に対して有効になります。

## アクセシビリティ標準 {#accessibility-standards}

HTML5 フォームは、既知の例外を除き、アクセシビリティに関してリハビリテーション法第 508 条に準拠しています。詳しくは、[HTML5 フォームの VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf)を参照してください。

## HTML5 フォーム向けに認定されたスクリーンリーダー {#certified-screen-readers-for-html-forms}

* Microsoft® Windows の JAWS 14.0
* macOS X とiPadの VoiceOver

### JAWS {#jaws}

すべてのデフォルトのキーストロークとショートカットは HTML5 フォームで機能します。JAWS の使用について詳しくは、[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp) にアクセスしてください。

### VoiceOver {#voiceover}

HTML5 フォームは VoiceOver のすべてのデフォルトのキーストロークとジェスチャーをサポートします。VoiceOver の設定と使用について詳しくは、[https://www.apple.com/jp/accessibility/vision/](https://www.apple.com/jp/accessibility/vision/) を参照してください。

## 既知の問題 {#known-issues}

* **（Internal Explorer 9 のみ）** HTML5 フォームでは、ページはオンデマンドで（動的に）読み込まれます。オンデマンドのページ読み込みは、スクリーンリーダーの機能で問題が生じます。スクリーンリーダーのフォーカスがページの最後のフィールドにあり、ユーザーがタブを押すと、スクリーンリーダーはフォームの最初のページの最初のフィールドにフォーカスを戻します。
* **（Internal Explorer 9 のみ）** HTML5 フォームの日付選択のコントロールはキーボードで完全にアクセスできません。日付選択のコントロールで、上向き／下向き矢印キーを複数回押した場合、日付選択のコントロールが閉じて、フォーカスが次／最後のフィールドに移動します。 

* VoiceOver は、iPad safari では日付ウィジェットで矢印キーを検出できません。
