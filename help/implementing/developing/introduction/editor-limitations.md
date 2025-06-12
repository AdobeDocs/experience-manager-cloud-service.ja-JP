---
title: ページエディターの制限事項
description: ページエディターは、オーバーレイを利用して iframe 内に閉じ込められたコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 8b38e26b16c1fb565f122777f0577d332f62c39c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 88%

---


# ページエディターの制限事項 {#editor-limitations}

[ ページエディター ](/help/sites-cloud/authoring/page-editor/introduction.md) は、オーバーレイを利用して iframe 内に閉じ込められたコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項をまとめ、可能な限り解決策や回避策を提供します。

## 機能の制限事項 {#functional-limitations}

作成者は、エディターを使用してページを作成する際に、次の機能上の制限を受ける場合があります。

### リンクがアクティブにならない {#links-not-active}

[ページの編集](/help/sites-cloud/authoring/page-editor/edit-content.md)時に、リンクがアクティブになりません。

* [コンテンツ内のリンクを使用して移動するには、**プレビュー**&#x200B;モード](/help/sites-cloud/authoring/page-editor/introduction.md#preview-mode)に切り替えます。

### 構造ページ {#structure-pages}

ページに `structure` という名前を付けることはできません。`structure` と名前が付けられたページは、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターでの CSS の操作に次の制限を受ける場合があります。

### 要素が絶対配置される {#absolutely-positioned-elements}

絶対配置された要素により、そのオーバーレイの位置に問題が生じる可能性があります。

* この場合、エディターはまったく同じ寸法のオーバーレイを作成するので、絶対配置された要素の寸法が正しいことを確認します。

### vh 単位 {#vh-units}

iframe の高さは AEM によって自動調整されるので、`vh` 単位はサポートされません。

### 固定の背景画像 {#fixed-background-images}

固定の背景画像は、iframe 内に埋め込まれるので、スクロール時に固定されているように表示されない可能性があります。

* ヘッダーバーのアクションで「**公開済みとしてページを表示**」を選択すると、ページが正しく表示されます。

### 100 ％の高さ {#height}

ページの body 要素では、100 ％の高さはサポートされていません。

* フルスクリーンの body を実装するためには、次のように body 要素を「拡張」することで、回避策が可能になります。

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 余白の折りたたみ {#margin-collapsing}

余白の折りたたみの問題は、body 要素の最初の子要素に余白がある場合に発生することがあります。

* 解決策として、次のように body 要素レベルに clearfix を追加します。

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
