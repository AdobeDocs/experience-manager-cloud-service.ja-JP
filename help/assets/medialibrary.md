---
title: AEM Assets と AEM Media Library との比較
description: AEM Assets と AEM Media Library の違いなど、両者に関するよくある質問。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 100%

---


# AEM Assets と AEM Media Library の比較に関するよくある質問 {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager (AEM) Assets は、AEM プラットフォームの不可欠な構成要素です。このスムーズな統合は AEM の大きなメリットとしてとらえられており、これによってコンテンツ管理における整合性とコンテンツ作成者の高い生産性が確保されます。

## AEM Assets とは何ですか。 {#what-is-aem-assets}

AEM Assets は、AEM プラットフォーム上のアプリケーションです。お客様はこのアプリケーションを使用して、Web ベースのリポジトリ内でデジタルアセット（画像、ビデオ、ドキュメントおよびオーディオクリップ）を管理できます。AEM Assets には、メタデータのサポート、レンディション、デジタルアセット管理ファインダー、ユーザーインターフェイスを介した管理が含まれています。

## AEM Media Library とは何ですか。 {#what-is-the-aem-media-library}

AEM Media Library は、画像やその他の共有リソースの保存専用に設けられた、AEM WCM コンテンツリポジトリ内の構成要素です。Media Library は、AEM WCM のデジタルアセット管理機能を使用します。

## AEM WCM にはない AEM Assets の機能 {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

AEM Assets のお客様だけが使用できる独自の機能は次のとおりです。

1. タイトル、タグ、説明以外のメタデータを抽出して編集する機能
1. AEM Assets Admin（ようこそ画面の siteadmin の隣にある 2 つ目のボタンをクリックすると表示されます）
1. デジタルアセット管理に関連するすべてのワークフローステップ（AEM Assets 取り込み、AEM Assets 削除、AEM Assets サブアセット操作、AEM Assets メタデータ抽出）
1. パッケージ領域に含まれるライブラリ（「dam」など）

これらの機能を使用するには、AEM Assets の有効なライセンスが必要です。

## AEM Assets は個別のパッケージとして使用できますか。 {#is-aem-assets-available-as-a-separate-package}

いいえ。インストールとデプロイメントを簡単にするために、すべての AEM アプリケーションとアドオンは、機能がすべて含まれる 1 つのパッケージで配布されます。これは、パッケージに含まれるすべての機能の使用権がユーザーにあることを表すわけではありません。

## デジタルアセットのメタデータを編集したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

タイトル、説明およびタグ以外のメタデータを編集する場合は、AEM Assets のライセンスが必要です。

## Web サイトでカテゴリ述語を使用したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

はい。カテゴリ述語は、Geometrixx Press Center で使用されるその他すべてのコンポーネントと共に AEM Assets に含まれており、AEM Assets ライセンスが必要です。

## 画像を読み込むときに自動的にサイズ変更したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

はい。画像のサイズ変更、自動ワークフロー駆動変換およびレンディションの管理機能は AEM Assets に含まれており、AEM Assets ライセンスが必要です。

## カスタマイズされた画像コンポーネントを使用して画像をサイズ変更したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

画像コンポーネントは AEM WCM に含まれています。画像コンポーネントに（さらに AEM Assets にも）使用されているグラフィックライブラリは AEM プラットフォームに含まれており、AEM Assets ライセンスは必要ありません。

## 自分が AEM Assets のライセンスを所持していない場合、ユーザーが AEM Assets を使用しないようにする方法はありますか。 {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

すべての AEM Assets 固有ワークフロー、コンポーネント、分類、オプション、AEM Assets 管理機能を AEM から削除できます。これによって、ライセンスを所持していない AEM Assets の機能をユーザーが誤って使用することを防ぐことができます。

## ページに画像を追加し、その画像の切り抜きやサイズ変更を実行したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

このような使用法では、AEM Assets を購入する必要はありません。Web サイト上で画像を使用する目的では、Media Library も使用する必要はありません。画像コンポーネントを使用すると、ページに画像を直接アップロードできるからです。

## AEM Assets と Media Library で使用可能な機能の詳細な比較 {#listoffeatures}

**AEM Assets**

* コレクションと Lightbox
* 高度なメタデータプロパティと管理
* Adobe Asset Link（Creative Cloud エンタープライズ版への接続）
* AEM デスクトップアプリケーション
* 処理プロファイル
* InDesign Server との統合
* アセットテンプレートとカタログ作成フレームワーク
* Adobe Photoshop、Illustrator、InDesign にリンクしたアセット
* 多言語アセット管理
* PIM との統合
* Rights Management
* Camera Raw サポート
* 検索ファセットの管理と設定
* 事前定義済み DAM ワークフロー（写真撮影など）
* アセットのレポートと分析：アセットインサイト
* 3D アセット管理
* Connected Assets
* Brand Portal
* セルフサービスアクセス
* 閲覧、検索、ダウンロード
* コレクションとフォルダー共有
* 管理ツール
* スマートタグ
* ビジュアル検索
* アセット管理 UI

**Media Library**

* 基本的なメタデータプロパティ
* タグ管理
* バージョン管理
* 静的レンディション
* プロジェクト、タスク、ワークフローオーサリング
* アクティビティストリーム（タイムライン）
* クエリビルダー（API）
* Marketing Cloud との統合
* UI のカスタマイズと拡張
* コメントと注釈