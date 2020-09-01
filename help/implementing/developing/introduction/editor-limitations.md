---
title: エディターの制限事項
description: タッチ操作対応の UI のエディターは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 65%

---


# エディターの制限事項 {#editor-limitations}

タッチ操作対応の UI のエディターは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項をまとめ、可能な限り解決策や回避策を提供します。

## 機能の制限 {#functional-limitations}

作成者がエディターを使用してページを作成する際、以下の機能の制限が発生する可能性があります。

### リンクがアクティブにならない {#links-not-active}

When [editing a page](/help/sites-cloud/authoring/fundamentals/editing-content.md), links are not active.

* [**プレビュー**](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) モードに切り替えて、コンテンツ内のリンクを使用して移動します。

### 構造ページ {#structure-pages}

ページに名前を付けることはできません `structure`。 名前が付けられたページ `structure` は、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターの CSS のインタラクションに関して以下の制限が発生する可能性があります。

### 要素が絶対配置される {#absolutely-positioned-elements}

絶対配置された要素により、そのオーバーレイの位置に問題が生じる可能性があります。

* エディターではまったく同じサイズでオーバーレイが作成されるので、この問題が発生した場合は、絶対配置された要素のサイズが正しいことを確認します。

### vh 単位 {#vh-units}

`vh` iframeの高さはAEMで自動的に調整される必要があるので、単位はサポートされません。

### 固定の背景画像 {#fixed-background-images}

iframe内に埋め込まれているため、スクロール時に背景画像が固定として表示されない場合があります。

* Selecting **View Page as Published** in the header bar actions displays the page properly.

### 100 ％の高さ {#height}

ページの body 要素では、100 ％の高さはサポートされていません。

* 次のようにbody要素を「ストレッチ」してフルスクリーンボディを実装するには、回避策があります。

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
