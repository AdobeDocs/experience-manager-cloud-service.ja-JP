---
title: エディターの制限事項
description: タッチ操作対応 UI のエディターは、オーバーレイを使用して iframe に含まれるコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 60%

---

# エディターの制限事項 {#editor-limitations}

タッチ操作対応 UI のエディターは、オーバーレイを使用して iframe に含まれるコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項の概要を説明し、可能な場合は解決策や回避策を提供します。

## 機能の制限 {#functional-limitations}

作成者は、エディターを使用してページを作成する際に、次の機能上の制限を受ける場合があります。

### リンクがアクティブではありません {#links-not-active}

[ページの編集](/help/sites-cloud/authoring/fundamentals/editing-content.md)時に、リンクがアクティブになりません。

* [コンテンツ内のリンクを使用して移動するには、**プレビュー**&#x200B;モード](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)に切り替えます。

### 構造ページ {#structure-pages}

ページに `structure` と名前が付けられない 。`structure` と名前が付けられたページは、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターでの CSS の操作に次の制限が生じる場合があります。

### 絶対位置の要素 {#absolutely-positioned-elements}

絶対に配置された要素は、オーバーレイの位置で問題を引き起こす可能性があります。

* この場合、エディターはまったく同じ寸法のオーバーレイを作成するので、絶対位置にある要素の寸法が正しいことを確認してください。

### vh 単位 {#vh-units}

iframe の高さは AEM によって自動調整されるので、`vh` 単位はサポートされません。

### 固定の背景画像 {#fixed-background-images}

固定の背景画像は、iframe 内に埋め込まれるので、スクロール時に固定されているように表示されない可能性があります。

* ヘッダーバーのアクションで「**公開済みとしてページを表示**」を選択すると、ページが正しく表示されます。

### 100 ％の高さ {#height}

ページの body 要素では、100 ％の高さはサポートされていません。

* フルスクリーンの body を実装するために次のように body 要素を「拡張」することで、回避することが可能です。

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
