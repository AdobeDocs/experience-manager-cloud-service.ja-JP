---
title: ヘッドレスセットアップ
description: このクイックスタートガイドでは、コンテンツモデル、コンテンツフラグメント、GraphQL API など、Cloud Service の強力なヘッドレス機能としての AEM の基本事項について説明します。
exl-id: 26c05122-5930-4b4e-91dd-287b7cc865ee
feature: Headless
role: Admin, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '278'
ht-degree: 100%

---

# ヘッドレスセットアップ {#introduction}

以下では、AEM およびヘッドレステクノロジーについて既に熟知しているユーザー向けに、AEM as a Cloud Service を使用したエクスペリエンスの作成、管理、配信の簡単な道筋を 5 つの手順に分けて示します。各ガイドは前のガイドに基づいているので、じっくり順番に検討することをお勧めします。

1. [設定の作成](create-configuration.md)
1. [コンテンツフラグメントモデルの作成](create-content-model.md)
1. [アセットフォルダーの作成](create-assets-folder.md)
1. [コンテンツフラグメントの作成](create-content-fragment.md)
1. [API リクエストの作成](create-api-request.md)

>[!TIP]
>
>この入門ガイドでは、AEM とヘッドレステクノロジーの両方に関する知識を前提としています。
>
>AEM またはヘッドレスのいずれかを初めて使用する場合は、アドビのヘッドレスドキュメントジャーニーを参照して、ヘッドレスと AEM によるヘッドレスのサポートについて概要を理解してください。
>
>* [ヘッドレスデベロッパージャーニー](/help/journey-headless/developer/overview.md)
>* [ヘッドレスコンテンツアーキテクトジャーニー](/help/journey-headless/architect/overview.md)
>* [ヘッドレスコンテンツ作成者ジャーニー](/help/journey-headless/author/overview.md)
>* [ヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md).

## 対象読者 {#audience}

説明されているタスクは、AEM のヘッドレス機能の基本的な包括的デモに必要です。テスト用 AEM インスタンスへの管理者アクセス権を持つユーザーは誰でも、これらのガイドに従って AEM でのヘッドレスな配信を理解できますが、開発者の経験を持つユーザーが最適です。

ただし、実稼動状況では、これらのタスクは様々なペルソナによって実行され、実行回数も様々です。次に例を示します。

* **管理者**：コンテンツの初期設定とフォルダー構造を、通常は 1 回のみまたは散発的にセットアップする必要があります。
* **情報アーキテクト**：通常、組織のニーズの変化に応じて新しいモデルを追加します。
* **コンテンツ作成者**：アーキテクトが定義したモデルに基づいて、新しいコンテンツをコンテンツフラグメントとして継続的に作成します。

## 次の手順 {#next-step}

詳細に入る準備ができましたか？それでは、まず、ヘッドレスセットアップの第 1 部である[設定の作成](create-configuration.md)に目を通しましょう。
