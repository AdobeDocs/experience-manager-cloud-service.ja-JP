---
title: エディターの制限事項
description: タッチ操作対応の UI のエディターは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 100%

---


# エディターの制限事項 {#editor-limitations}

タッチ操作対応の UI のエディターは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項をまとめ、可能な限り解決策や回避策を提供します。

## 機能の制限  {#functional-limitations}

作成者がエディターを使用してページを作成する際、以下の機能の制限が発生する可能性があります。

### リンクがアクティブにならない  {#links-not-active}

[ページの編集](/help/sites-cloud/authoring/fundamentals/editing-content.md)時に、リンクがアクティブになりません。

* [コンテンツ内のリンクを使用して移動するには、**プレビュー**&#x200B;モード](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)に切り替えます。

### 構造ページ {#structure-pages}

ページに `structure` と名前が付けられない 。`structure` と名前が付けられたページは、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターの CSS のインタラクションに関して以下の制限が発生する可能性があります。

### 要素が絶対配置される  {#absolutely-positioned-elements}

絶対配置された要素により、そのオーバーレイの位置に問題が生じる可能性があります。

* エディターではまったく同じサイズでオーバーレイが作成されるので、この問題が発生した場合は、絶対配置された要素のサイズが正しいことを確認します。

### vh 単位  {#vh-units}

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
