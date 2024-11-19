---
title: Edge Delivery Servicesの作業中のサイト機能
description: 作業中のAEM Sitesの機能とユースケースを確認し、Edge Delivery Servicesを使用する際に代替ソリューションを見つけます。
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: 92da26452438f2b56cdec1aecc76587d4982f00e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Edge Delivery Servicesの作業中のサイト機能 {#wip-sites-features}

作業中のAEM Sitesの機能とユースケースを確認し、Edge Delivery Servicesを使用する際に代替ソリューションを見つけます。

>[!TIP]
>
>仕掛品は、道端という意味ではありません。 このドキュメントで処理中としてリストされている機能やユースケースが必要な場合は、Adobe担当者にお問い合わせください。 お客様とAdobeが連携して特定のニーズを把握し、代替ソリューションを見つけることができます。

## 作業中の機能 {#wip-features}

AEM SitesでEdge Delivery Servicesを使用する場合、ほとんどの Sites 機能を使用できます。 例えば、[Sites コンソール ](/help/sites-cloud/authoring/sites-console/introduction.md) で使用できるほぼすべてのアクションがEdge Delivery Servicesに適用できます。

ただし、一部の機能は作業中（WIP）です。 WIP 機能は、Sites コンソールの機能であり、AEM SitesとのEdge Delivery Servicesでまだ使用できないか、部分的にのみ使用できます。 このため、WIP 機能の表示方法が Sites の同等機能とは異なる場合や、ユースケースに応じた別のソリューションが存在する場合があります。

次のリストは、このような WIP 機能と代替ソリューションを示しています。 プロジェクトで WIP 機能が必要な場合は、以下に示す代替手段を確認し、Adobeに連絡して協力しユースケースを把握してください。

| Sites 機能 | Edgeのステータス | 備考 | Edge ドキュメント |
|---|---|---|---|
| [ ページの継承 ](/help/sites-cloud/administering/msm-and-translation.md) | 使用可 |  | [ ユニバーサルエディターでのコンテンツの継承 ](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [ コンポーネントの継承 ](/help/sites-cloud/administering/msm-and-translation.md) | 一部利用可能 | コンポーネントはコンテンツを継承しますが、継承を元に戻すことができるのはページレベルのみです | [ ユニバーサルエディターでのコンテンツの継承 ](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [ 言語コピー ](/help/sites-cloud/administering/translation/overview.md) | 部分的に使用可能 | コンポーネントはコンテンツを継承しますが、継承を元に戻すことができるのはページレベルのみです | [ ユニバーサルエディターでのコンテンツの継承 ](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [ マルチサイト管理 ](/help/sites-cloud/administering/msm/overview.md) | 部分的に使用可能 | コンポーネントはコンテンツを継承しますが、継承を元に戻すことができるのはページレベルのみです | [ ユニバーサルエディターでのコンテンツの継承 ](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [ローンチ](/help/sites-cloud/authoring/launches/overview.md) | 一部利用可能 | コンポーネントはコンテンツを継承しますが、継承を元に戻すことができるのはページレベルのみです | [ ユニバーサルエディターでのコンテンツの継承 ](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [ページテンプレート](/help/sites-cloud/authoring/page-editor/templates.md) | 部分的に使用可能 | テンプレートから作成されたページは、元のテンプレートから独立したコピーです。 | [ ユニバーサルエディターでのページテンプレートの使用 ](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Context Hub とターゲティング ](/help/sites-cloud/authoring/personalization/overview.md) | 使用不可 |  |  |
| [タイムワープ](/help/sites-cloud/authoring/launches/preview.md) | 使用不可 |  |  |
| [関連コンテンツ](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | 使用不可 |  |  |
| [エクスペリエンスフラグメント](/help/sites-cloud/authoring/fragments/experience-fragments.md) | 代替 | ページを作成し、フラグメントコンポーネントを使用します |  |

## 作業中のユースケース {#wip-use-cases}

Edge Delivery Servicesは、まったく新しい最新のテクノロジースタックに基づいて構築されているので、次のAEM Sitesのユースケースはまだ完全にはカバーされておらず、作業中です。 プロジェクトで WIP のユースケースが必要な場合は、Adobeに問い合わせて、連携しプロジェクトのニーズを理解してください。

| Sites のユースケース | 詳細 |
|---|---|
| ページをレンダリングするサーバーサイドロジック | アプリサーバーとしてのAEM Runtime の使用 |
| 動的ページ | SSI または任意の動的インクルード技術 |
| ユーザー管理 | AEMを IdP として使用 |
| 認証 | AEMを使用したコンテンツのセキュリティ保護 |
| コンテンツ権限 | 安全なエクストラネットとしてのAEM |
