---
title: 既存の AEM プロジェクトでの Edge Delivery Services の使用
description: 既存の AEM プロジェクトで Edge Delivery Services のメリットを活用する方法を学ぶ
feature: Edge Delivery Services
exl-id: f54aac3a-1d0c-4be0-9aa6-616217e0e458
source-git-commit: 05548d56d791584781606b02839c5602b4469f7b
workflow-type: ht
source-wordcount: '339'
ht-degree: 100%

---

# 既存の AEM プロジェクトでの Edge Delivery Services の使用 {#existing-projects}

新しい AEM プロジェクトで Edge 配信サービスのメリットを活用できるようになるまで待つ必要はありません。Edge 配信サービスは既存の AEM プロジェクトに統合できるので、パフォーマンスの向上をすぐに活用できます。

## AEM ページエディターの制限事項 {#page-editor}

Edge Delivery Services が登場する前は、AEM で管理されるコンテンツは、AEM ページエディターを使用して編集されていました。Edge Delivery Services の導入前にプロジェクトが開始されていた場合、ページエディターを使用していることはほぼ確実です。

AEM ページエディターは、[コアコンポーネントなどの [AEM コンポーネント](/help/implementing/developing/components/overview.md)でのみ機能します。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)これらのコンポーネントは、Edge Delivery Services とは互換性がありません。このため、既存の AEM プロジェクトに Edge Delivery Services を導入するには、次の 2 つの段階が必要です。

* [フェーズ 1 - フロントエンドの置換](#replace-front-end)
* [フェーズ 2 - ユニバーサルエディターに切り替える](#switch-ue)

## フェーズ 1 - フロントエンドの置換 {#replace-front-end}

フェーズ 1 では、既存の AEM サイト構造、コンポーネント、オーサリングツールを引き続き使用できます。Web サイトのレンダリングは、JavaScript と CSS のブロックを使用して再構築され、Edge Delivery Services 経由で配信されます。

ブロックの詳細と、Edge Delivery Services 向けの開発方法について詳しくは、Edge Delivery Services に関するドキュメントの[ビルドセクション](/help/edge/developer/block-collection.md)を参照してください。

AEM でレンダリングされた HTML 出力を変換して Edge Delivery Services に送信するには、App Builder 上のコンバーターが必要です。

![公開フローのコンテンツコンバーター](assets/content-converter.png)

フェーズ 2 では、AEM オーサー環境での HTL と Java を備えた AEM コアコンポーネント、Edge 配信環境での JS ベースのブロック、NodeJS ベースのコンバーターというテクノロジーの重複を排除して、プロセスを完了します。

## フェーズ 2 - ユニバーサルエディターに切り替える {#switch-ue}

このフェーズでは、AEM ページエディターがユニバーサルエディターに置き換えられます。ユニバーサルエディターではブロックを直接操作できるので、AEM コアコンポーネントとコンバーターは不要になりました。

## 使い始める方法 {#how-to-get-started}

この機能にアクセスするには、アドビ担当者にお問い合わせください。
