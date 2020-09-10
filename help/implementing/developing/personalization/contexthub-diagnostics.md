---
title: ContextHub の診断
description: ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります
translation-type: tm+mt
source-git-commit: e361f24b943eff68982a37ac0dc2597f92450026
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 65%

---


# ContextHub の診断 {#contexthub-diagnostics}

ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります。To open the page, go to the `contexthub.diagnostics.html` page of your AEM author instance, for example:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub の診断ページには、作成されたストアおよび UI モジュール、読み込まれているクライアントライブラリフォルダー、役立つページへのリンクに関する情報が表示されます。

>[!NOTE]
>
>診断情報が返されるようにするために、デバッグモードを有効にする必要があります。そうしないと、診断ページが空白になります。デバッグモードを有効にする方法について詳しくは、[このドキュメント](configuring-contexthub.md#debugging-contexthub)を参照してください。

## ストア {#stores}

ストアセクションには、設定されているすべての ContextHub ストアが一覧表示されます。リストの各項目は、次の情報で構成されます。

* **タイトル：**&#x200B;ストアのベースとなっている[ストアタイプ](sample-stores.md)。
* **パス：**&#x200B;設定を保持しているリポジトリノードへのパス。
* **リソースタイプ：**&#x200B;ストアタイプが定義されているリポジトリノードのパス。
* **クライアントライブラリ：**&#x200B;読み込まれ、ストアタイプを実装するクライアントライブラリのカテゴリ。

## モジュール {#modules}

モジュールセクションには、設定されているすべての ContextHub UI モジュールが一覧表示されます。リストの各項目は、次の情報で構成されます。

* **タイトル：** UIモジュールが基にしている [UIモジュールタイプ](sample-modules.md) 。
* **パス：**&#x200B;設定を保持しているリポジトリノードへのパス。
* **リソースタイプ：** UI モジュールタイプが定義されているリポジトリノードのパス。
* **クライアントライブラリ：**&#x200B;読み込まれ、UI モジュールタイプを実装するクライアントライブラリのカテゴリ。

## Clientlibs {#clientlibs}

Clientlibs セクションには、ContextHub によって読み込まれたすべてのクライアントライブラリフォルダーが一覧表示されます。クライアントライブラリは次のように分類されます。

* **kernel.js：** ContextHub フレームワーク、セグメントエンジン、ストアタイプを実装するクライアントライブラリ。
* **ui.js：** ContextHub UI および UI モジュールタイプを実装するクライアントライブラリ。
* **style.css：**&#x200B;クライアントライブラリから読み込まれる CSS ファイル。

## URL {#urls}

URL セクションには、次の ContextHub 機能へのリンクが含まれます。

* **設定エディター：** ストア、UIモ [ード](configuring-contexthub.md) 、UIモジュールを設定できるContextHub設定ページを開きます。
* **ContextHubモジュールの設定：** ContextHubストア設定のJavaScriptオブジェクト表現を含む `/etc/cloudsettings/default/contexthub.config.kernel.js` ファイルを開きます。
* **ContextHub UIの設定：** ContextHub UIモード設定のJavaScriptオブジェクト表現を含む `/etc/cloudsettings/default/contexthub.config.ui.js` ファイルを開きます。
* **kernel.js:** ContextHubフレームワーク、セグメントエンジン、およびストアの種類を実装するクライアントライブラリのソースコードを含む `/etc/cloudsettings/default/contexthub.kernel.js` ファイルを開きます。
* **ui.js:** ContextHub UIとUIモジュールタイプを実装するクライアントライブラリのソースコードを含む `/etc/cloudsettings/default/contexthub.ui.js` ファイルを開きます。
* **style.css:** ContextHub UIおよびUIモジュールのCSSスタイルを含む `/etc/cloudsettings/default/contexthub.styles.css` ファイルを開きます。
