---
title: ContextHub の診断
description: ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 58%

---

# ContextHub の診断 {#contexthub-diagnostics}

ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります。このページを開くには、AEM オーサーインスタンスの `contexthub.diagnostics.html` ページに移動します。例：

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub の診断ページには、作成されたストアおよび UI モジュール、読み込まれているクライアントライブラリフォルダー、役立つページへのリンクに関する情報が表示されます。

>[!NOTE]
>
>診断情報を返すには、デバッグモードを有効にする必要があります。有効にしない場合は、診断ページが空白になります。 詳しくは、 [このドキュメント](configuring-contexthub.md#debugging-contexthub) デバッグモードを有効にする方法の詳細については、を参照してください。

## ストア {#stores}

「ストア」セクションには、設定されたすべての ContextHub ストアが一覧表示されます。 リスト内の各項目は、次の情報で構成されます。

* **タイトル：**&#x200B;ストアのベースとなっている[ストアタイプ](sample-stores.md)。
* **パス：** 設定を保持するリポジトリノードへのパス。
* **resourceType:** ストアタイプが定義されているリポジトリノードのパス。
* **clientlibs:** 読み込まれ、ストアタイプを実装するクライアントライブラリのカテゴリ。

## モジュール {#modules}

「モジュール」セクションには、設定されたすべての ContextHub UI モジュールが一覧表示されます。 リスト内の各項目は、次の情報で構成されます。

* **タイトル**：UI モジュールのベースとなっている [UI モジュールタイプ](sample-modules.md)。
* **パス：** 設定を保持するリポジトリノードへのパス。
* **resourceType:** UI モジュールタイプが定義されているリポジトリノードのパス。
* **clientlibs:** 読み込まれ、UI モジュールタイプを実装するクライアントライブラリのカテゴリ。

## Clientlibs {#clientlibs}

Clientlibs セクションには、ContextHub によって読み込まれたすべての[クライアントライブラリフォルダー](/help/implementing/developing/introduction/clientlibs.md)が一覧表示されます。クライアントライブラリは次のように分類されます。

* **kernel.js：** ContextHub フレームワーク、セグメントエンジン、ストアタイプを実装するクライアントライブラリ。
* **ui.js：** ContextHub UI および UI モジュールタイプを実装するクライアントライブラリ。
* **style.css:** クライアントライブラリから読み込まれる CSS ファイル。

## URL {#urls}

URL セクションには、次の ContextHub 機能へのリンクが含まれます。

* **設定エディター**：ストア、UI モードおよび UI モジュールを設定できる [ContextHub 設定ページ](configuring-contexthub.md)を開きます。
* **ContextHub モジュールの設定**：`/etc/cloudsettings/default/contexthub.config.kernel.js` ファイルを開きます。このファイルには、ContextHub ストア設定の JavaScript オブジェクト表現が格納されています。
* **ContextHub UI の設定**：`/etc/cloudsettings/default/contexthub.config.ui.js` ファイルを開きます。このファイルには、ContextHub UI モード設定の JavaScript オブジェクト表現が格納されています。
* **kernel.js**：`/etc/cloudsettings/default/contexthub.kernel.js` ファイルを開きます。このファイルには、ContextHub フレームワークおよびセグメントエンジン、ストアタイプを実装するクライアントライブラリのソースコードが格納されています。
* **ui.js**：`/etc/cloudsettings/default/contexthub.ui.js` ファイルを開きます。このファイルには、ContextHub UI および UI モジュールタイプを実装するクライアントライブラリのソースコードが格納されています。
* **style.css**：`/etc/cloudsettings/default/contexthub.styles.css` ファイルを開きます。このファイルには、ContextHub UI および UI モジュールの CSS スタイルが格納されています。
