---
title: インタラクティブなコミュニケーションの作成
description: パーソナライズされたデータ主導のコミュニケーションを実現。 主な機能、オンボーディングステップ、実際のユースケースについて、ガイドとチュートリアルでご確認ください。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: c23145c9-078d-4b03-a8f4-2d835cdd1592
source-git-commit: 53ff71c82d35b9ec9b20b521ef469d3f0abd79df
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---


# インタラクティブなコミュニケーションの作成


インタラクティブなコミュニケーションを活用すれば、カスタマーサービス、請求、オンボーディングドキュメント、オファーレター、アカウントの更新など、パーソナライズされたインタラクティブなコミュニケーションを作成、管理、提供できます。 動的なユーザー固有のコンテンツが、業界全体のコミュニケーション体験を向上させるあらゆるシナリオをサポートするように設計されています。

何千もの顧客に銀行取引明細書、保険契約、光熱費を送信する必要がある場合を想像してみてください。 それぞれ同じレイアウトですが、パーソナライズされたデータがあります。 インタラクティブ・コミュニケーション（IC）は、それを効率的に可能にします。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/introduction.png)

特に、パーソナライゼーションとデータの統合が必要な場合、これらのドキュメントを手作業で作成するのは時間がかかり、多くの場合、不整合が生じます。 インタラクティブ通信エディターを使用すると、インタラクティブ通信の作成プロセスを効率化できます。

## 前提条件

* [作成者がforms-users グループのメンバーであることを確認します](/help/forms/setup-forms-cloud-service.md#configure-users)

## インタラクティブなコミュニケーションの作成

必要な再利用とデータ統合のレベルに基づいて、様々なシナリオからインタラクティブ通信を作成できます。

+++ 空のインタラクティブ通信の作成

空白のインタラクティブ通信を作成すると、レイアウト、構造、ロジックを完全に制御したい場合に最適な、ゼロから開始できます。
次の手順に従います。

1. **Adobe Experience Manager （AEM） Forms as a Cloud Service インスタンス**&#x200B;を開きます。
1. **Forms/Forms &amp; Documents**&#x200B;に移動します。
1. **作成/ インタラクティブ通信**&#x200B;をクリックします。

   ![IC ドキュメントを検索](/help/forms/interactive-communication/assets/comm.png)

1. 作成画面で、「**テンプレート**」フィールドを空白のままにします。

   ![IC ドキュメントを検索](/help/forms/interactive-communication/assets/create-ic-document.png)

1. タイトル、名前、作成者など、その他の詳細を入力します。
1. **作成**&#x200B;をクリックして、インタラクティブ通信エディターUIに入り、デザインを開始します。
1. IC エディターが開き、コミュニケーションのデザインを開始できます。
+++

+++ テンプレートベースのインタラクティブ通信の作成

テンプレートを使用すると、ヘッダー、フッター、ロゴ、標準フォーマットなどの一貫したレイアウト要素を再利用して、デザインをスピードアップできます。
テンプレートにより、ブランドの一貫性を確保し、一般的なコミュニケーションの種類に応じた時間を節約できます。次の手順を実行します。

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **Forms/Forms &amp; Documents**&#x200B;に移動し、**作成/インタラクティブ通信**&#x200B;をクリックします。
1. 作成フォームで、ピッカーから有効なテンプレートを&#x200B;**select**&#x200B;します。
1. タイトル、名前、作成者など、その他の詳細を入力します。
1. **作成**&#x200B;をクリックして、選択したテンプレート構造を使用したコミュニケーションをデザインします。
1. IC エディターが開き、コミュニケーションのデザインを開始できます。
+++

+++ データを操作したインタラクティブ通信の作成

データを活用したコミュニケーション バックエンドのデータを使用してコンテンツを自動的にパーソナライズできます。
明細書、請求書、または通知に最適です。構造は一定のままですが、データは受信者ごとに異なります。次の手順に従います。

1. AEM Forms as a Cloud Service インスタンスを開きます。
1. **Forms/Forms &amp; Documents**&#x200B;に移動し、**作成/インタラクティブ通信**&#x200B;をクリックします。
1. **フォームデータモデル** フィールドで、定義済みの&#x200B;**FDM （フォームデータモデル）**&#x200B;をリンクします。
1. タイトル、名前、作成者など、その他の詳細を入力します。
1. エディター内で&#x200B;**データモデル**&#x200B;を使用して、フィールドを動的データ（顧客名、残高、アカウント番号など）にバインドします。
1. **コンテンツ領域、サブフォーム**&#x200B;および&#x200B;**フラグメント**&#x200B;を使用して、必要に応じてデータを構造化し、繰り返します。
1. **PDF Preview**&#x200B;を使用してプレビューし、配信のためのコミュニケーションを確定します。
1. IC エディターが開き、コミュニケーションのデザインを開始できます。

![IC ドキュメントを検索](/help/forms/interactive-communication/assets/ic-ui.png)
+++

インタラクティブなコミュニケーションの構築を始め、ワークフローを合理化し、ユーザーごとに最適な体験を提供できます。

## 次の手順

[ インタラクティブ通信テンプレートの作成](/help/forms/interactive-communication/create-interactive-communication-template.md)
[ インタラクティブ通信フラグメントの作成](/help/forms/interactive-communication/create-interactive-communication-fragment.md)

## 関連トピック

* [ インタラクティブ通信のレビューと注釈](/help/forms/interactive-communication/howto/review-and-annotate-interactive-communication.md) — IC キャンバス上に配置された注釈ピンを使用して、レビュー担当者と共同作業を行います。
* [ インタラクティブ通信バージョンの比較](/help/forms/interactive-communication/howto/compare-interactive-communication-versions.md) — 2つのバージョン間のレイアウトとコンテンツの違いを並べて調べます。
* [ テーブル セルの結合と分割](/help/forms/interactive-communication/howto/merge-and-split-table-cells.md) — セルの結合または分割によって柔軟なテーブル レイアウトを作成します。
* [ コンポーネントをマスターページに移動](/help/forms/interactive-communication/howto/move-component-to-master-page.md) – 一貫したクロスページコンポーネントの配置を確保します。

