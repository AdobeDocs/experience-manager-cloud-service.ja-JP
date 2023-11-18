---
title: ContextHub データを使用したページのプレビュー
description: ContextHub ツールバーは、ContextHub ストアからのデータを表示し、ストアデータを変更することができ、コンテンツのプレビューに立ちます。
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 72%

---

# ContextHub データを使用したページのプレビュー  {#previewing-pages-using-contexthub-data}

ContextHub ツールバーを使用すると、ContextHub ストアからデータを表示して、ストアデータを変更できます。ContextHub ツールバーは、ContextHub ストア内のデータに基づいて決定されるコンテンツのプレビューに役立ちます。

このツールバーは、1 つ以上の UI モジュールを含む一連の UI モードで構成されます。

* UI モードは、ツールバーの左側に表示されるアイコンです。アイコンを選択すると、そのアイコンに含まれる UI モジュールがツールバーに表示されます。
* UI モジュールは、1 つ以上の ContextHub ストアのデータを表示します。また、一部の UI モジュールでは、ストアデータを操作することもできます。

ContextHub によって、いくつかの UI モードと UI モジュールがインストールされます。管理者が、異なる UI モードと UI モジュールを表示するように [ContextHub を設定](/help/implementing/developing/personalization/configuring-contexthub.md)している場合があります。

## ContextHub ツールバーの表示 {#revealing-the-contexthub-toolbar}

ContextHub ツールバーは、プレビューモードで使用できます。このツールバーは、オーサーインスタンス上で、管理者が有効にしている場合にのみ使用できます。

![ContextHub ツールバー](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. 編集用にページを開いた状態で、ツールバーの「プレビュー」を選択します。

   ![「プレビュー」ボタン](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. ツールバーを表示するには、ContextHub アイコンを選択します。

   ![ContextHub ボタン](/help/sites-cloud/authoring/assets/contexthub-button.png)

## UI モジュールの機能 {#ui-module-features}

提供する機能セットは UI モジュールごとに異なりますが、次のタイプの機能は共通しています。UI モジュールは拡張可能なので、開発者は必要に応じて他の機能を実装できます。

### ツールバーのコンテンツ {#toolbar-content}

UI モジュールは、1 つ以上の ContextHub ストアのデータをツールバーに表示できます。UI モジュールは、アイコンとタイトルで識別されます。

![ContextHub ペルソナ](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### ポップアップコンテンツ {#popup-content}

一部の UI モジュールは、クリックまたはタップされるとポップアップオーバーレイを表示します。 通常、ポップアップには、ツールバーに表示される以外の追加情報が含まれます。

![ContextHub プロファイル情報](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### ポップアップフォーム {#popup-forms}

モジュールのポップアップオーバーレイには、ContextHub ストア内のデータを変更できるフォーム要素を含めることができます。 ページのコンテンツがストアデータによって決まる場合は、このフォームを使用してページコンテンツの変更を監視できます。

### 全画面表示モード {#fullscreen-mode}

ポップアップオーバーレイには、ポップアップコンテンツを展開してブラウザーウィンドウまたは画面全体に表示するアイコンを含めることができます。

![全画面表示ボタン](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
