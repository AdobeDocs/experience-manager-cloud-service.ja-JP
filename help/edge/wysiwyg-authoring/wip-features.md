---
title: Edge Delivery Services 向けの作成中の Sites の機能
description: 作成中の AEM Sites の機能とユースケースと、Edge Delivery Services を使用した代替ソリューションについて説明します。
solution: Experience Manager Sites
feature: Edge Delivery Services
role: User
exl-id: 21745f53-a7ef-4eec-9170-b267c2f4314e
source-git-commit: 92da26452438f2b56cdec1aecc76587d4982f00e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 100%

---

# Edge Delivery Services 向けの作成中の Sites の機能 {#wip-sites-features}

作成中の AEM Sites の機能とユースケースと、Edge Delivery Services を使用した代替ソリューションについて説明します。

>[!TIP]
>
>作成中とは、終わりを意味するものではありません。このドキュメントで作成中と記載される機能またはユースケースが必要な場合は、アドビ担当者にお問い合わせください。お客様とアドビは協力して、お客様の特定のニーズを理解し、代替ソリューションを見つけることができます。

## 作成中の機能 {#wip-features}

AEM Sites で Edge Delivery Services を使用する場合、ほとんどの Sites 機能が使用できます。例えば、[Sites コンソール](/help/sites-cloud/authoring/sites-console/introduction.md)で使用できるほとんどすべてのアクションは、Edge Delivery Services に適用できます。

ただし、一部の機能は作成中（WIP）です。WIP 機能は、AEM Sites の Edge Delivery Services ではまだ使用できない、または部分的にしか使用できない Sites コンソールの機能です。このため、WIP 機能は Sites の機能とは異なる方法で提示される場合があり、ユースケースに代替ソリューションが存在する場合もあります。

次のリストに、このような WIP 機能と代替ソリューションを示します。プロジェクトに WIP 機能が必要な場合は、以下に示す代替手段を確認し、アドビに連絡して、協力してユースケースを理解してください。

| Sites 機能 | Edge のステータス | メモ | Edge のドキュメント |
|---|---|---|---|
| [ページの継承](/help/sites-cloud/administering/msm-and-translation.md) | 使用可 |  | [ユニバーサルエディターでのコンテンツの継承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [コンポーネントの継承](/help/sites-cloud/administering/msm-and-translation.md) | 部分的に使用可 | コンポーネントはコンテンツを継承しますが、継承はページレベルでのみ元に戻すことができます。 | [ユニバーサルエディターでのコンテンツの継承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [言語コピー](/help/sites-cloud/administering/translation/overview.md) | 部分的に使用可 | コンポーネントはコンテンツを継承しますが、継承はページレベルでのみ元に戻すことができます。 | [ユニバーサルエディターでのコンテンツの継承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [マルチサイト管理](/help/sites-cloud/administering/msm/overview.md) | 部分的に使用可 | コンポーネントはコンテンツを継承しますが、継承はページレベルでのみ元に戻すことができます。 | [ユニバーサルエディターでのコンテンツの継承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [ローンチ](/help/sites-cloud/authoring/launches/overview.md) | 部分的に使用可 | コンポーネントはコンテンツを継承しますが、継承はページレベルでのみ元に戻すことができます。 | [ユニバーサルエディターでのコンテンツの継承](/help/sites-cloud/authoring/universal-editor/inheritance.md) |
| [ページテンプレート](/help/sites-cloud/authoring/page-editor/templates.md) | 部分的に使用可 | テンプレートから作成されたページは、元のテンプレートから独立したコピーです。 | [ユニバーサルエディターを使用したページテンプレートの使用](/help/sites-cloud/authoring/universal-editor/templates.md) |
| [Context Hub とターゲティング](/help/sites-cloud/authoring/personalization/overview.md) | 使用不可 |  |  |
| [タイムワープ](/help/sites-cloud/authoring/launches/preview.md) | 使用不可 |  |  |
| [関連コンテンツ](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#associated-content-browser) | 使用不可 |  |  |
| [エクスペリエンスフラグメント](/help/sites-cloud/authoring/fragments/experience-fragments.md) | 代替 | ページの作成およびフラグメントコンポーネントの使用 |  |

## 作成中のユースケース {#wip-use-cases}

Edge Delivery Services は、まったく新しい最新のテクノロジースタックに基づいて作成されているので、AEM Site の次のユースケースは作成中でまだ完全には対象となっていません。プロジェクトに WIP のユースケースが必要な場合は、アドビに連絡して、協力してプロジェクトのニーズを把握ことをお勧めします。

| Sites のユースケース | 詳細 |
|---|---|
| ページをレンダリングするサーバーサイドロジック | アプリサーバーとしての AEM のランタイムの使用 |
| 動的ページ | SSI または任意の動的インクルード技術 |
| ユーザー管理 | AEM の IdP としての使用 |
| 認証 | セキュリティ保護されたコンテンツの AEM の使用 |
| コンテンツ権限 | セキュリティ保護されたエクストラネットとしての AEM |
