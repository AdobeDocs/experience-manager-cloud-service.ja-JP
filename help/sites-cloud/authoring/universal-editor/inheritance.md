---
title: ユニバーサルエディターでのコンテンツの継承
description: コンテンツの再利用とローカライゼーションをサポートするために、ユニバーサルエディターでマルチサイト管理とローンチのコンテンツの継承をサポートする方法について説明します。
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 2a1b87c2-29b9-4689-9a15-e17942439160
source-git-commit: 9941c652a1509934662cdaae6d187d1a28a1cc31
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 79%

---

# ユニバーサルエディターでのコンテンツの継承 {#inheritance}

コンテンツの再利用とローカライゼーションをサポートするために、ユニバーサルエディターでマルチサイト管理とローンチのコンテンツの継承をサポートする方法について説明します。

>[!NOTE]
>
>この機能は、AEM リポジトリに保存されているコンテンツに対してのみ使用できます。

## ユースケース {#use-case}

AEM の多くのユーザーにとって、ページの作成は単なる始まりに過ぎません。コンテンツを効果的に拡大・縮小するには、通常、ページの作成後に次の手順に従います。

1. 言語コピーと翻訳ワークフローを使用して、**ページを翻訳します**。
1. マルチサイト管理を使用して、翻訳済みページを様々な市場にロールアウトし、**ページをローカライズします**。
1. ローンチを使用して、ページの今後のイテレーションを準備し、それらの変更をライブで実行することによって、**新しいバージョンを作成します**。

これらの手順により、コンテンツの速度が向上し、コンテンツの一貫性が確保されます。ユニバーサルエディターは、言語コピー、マルチサイト管理およびローンチが依存するメカニズムであるコンテンツの継承をサポートしています。

## 継承 {#what-is-inheritance}

継承とは、一方を変更するともう一方も自動的に変更されるようにコンテンツをリンクできるメカニズムです。

MSM とローンチは、継承を使用してコンテンツを再利用するのに役立つ強力なツールです。ページを中央のソース（ブループリント）からコピーすると、作成者はそれらのコピーのコンテキストに固有の変更を行うことができますが、残りのコンテンツはブループリントから継承されたままになります。これは、サイトをローカライズする際に非常に役立ちます。

コピーの一部のコンテンツを変更するには、作成者は影響を受けるコンポーネントの継承を解除し、コピーをブループリントから同期した際にローカルの変更が上書きされないようにする必要があります。

## コンテンツの継承とユニバーサルエディター {#universal-editor}

ページが MSM またはローンチの一部であり、ユニバーサルエディターを使用してコンテンツを編集する場合、エディターでは、そのページの作成者が行ったすべての変更の継承を自動的に無効にし、ブループリントから更新を同期した際に変更済みのコンテンツが保持されるようにします。

作成者は、ローカル編集を行う前に、ボタンをクリックするなどの手順を実行して継承を無効にする必要はありません。変更を行うとすぐに、継承は暗黙的にキャンセルされます。このワークフローは、[ページエディター](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)とは対照的です。

ページ全体の継承は、次の方法で元に戻すことができます。

* [ライブコピーの概要コンソール](/help/sites-cloud/administering/msm/live-copy-overview.md)
* [ローンチコンソール](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* [ページプロパティウィンドウ](/help/sites-cloud/authoring/sites-console/page-properties.md)の「**ライブコピー**」タブにある「**リセット**」ボタンを使用する。

ユニバーサルエディターは、継承の基盤となるメカニズムには影響しません。継承の仕組みについて詳しくは、次のドキュメントを参照してください。

* [マルチサイト管理（MSM）](/help/sites-cloud/administering/msm/overview.md)
* [ローンチ](/help/sites-cloud/authoring/launches/overview.md)

### AEM Multi-Site-Management （MSM）拡張機能 {#msm-extension}

インストールされている場合、**AEM Multi-Site-Management （MSM）拡張では** 選択されたコンポーネントの現在の継承ステータスが表示され、コンポーネントレベルで継承を解除または復元することができます。

この拡張機能の使用方法について詳しくは、[ オーサリングのドキュメント ](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance) を参照してください。

この拡張機能を有効にする方法については、[Extension Managerのドキュメントを参照してください ](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)。

## 制限事項 {#limitations}

* 単一のコンポーネントの継承を元に戻すには、**AEM Multi-Site-Management （MSM）拡張機能** を有効にする必要があります。
* 視覚的なフィードバックによって、継承が無効になっているコンポーネントと保持されているコンポーネントを確認するには、**AEM Multi-Site-Management （MSM）拡張機能** を有効にする必要があります。
* これらの機能は現在、ページ内のコンポーネントに制限されており、MSM およびローンチの機能も備えているにもかかわらず、[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)にはまだ適用されていません。
