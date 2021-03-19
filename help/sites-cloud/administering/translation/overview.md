---
title: 多言語サイトのコンテンツの翻訳
description: 多言語サイトのコンテンツを翻訳する方法の概要を説明します。
feature: 言語コピー
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 50%

---


# 多言語サイトのコンテンツの翻訳 {#translating-content-for-multilingual-sites}

ページコンテンツやアセットの翻訳を自動化し、多言語Webサイトを作成および管理します。 翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、コンテンツを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

* **人による翻訳：** コンテンツは翻訳プロバイダーに送信され、専門の翻訳者が翻訳します。翻訳が完了すると、翻訳済みのコンテンツが返送され、AEMに読み込まれます。翻訳プロバイダーがAEMに統合されている場合、コンテンツはAEMと翻訳プロバイダーの間で自動的に送信されます。
* **機械翻訳：機械翻訳サ** ービスは、コンテンツを即座に翻訳します。

コンテンツの翻訳には次の手順が含まれます。

1. [AEM を翻訳プロバイダーサービスに接続](integration-framework.md#connecting-to-a-translation-service-provider)して、[翻訳統合フレームワーク設定を作成](integration-framework.md)します。
1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](integration-framework.md#configuring-pages-for-translation)ます。
1. [翻訳する](rules.md) コンテンツのタイプを指定します。
1. [翻訳するコンテンツを準備](preparation.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。
1. [翻訳](managing-projects.md) プロジェクトを作成して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。
1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](managing-projects.md)します。

AEM との統合のためのコネクターが翻訳サービスプロバイダーに用意されていない場合、AEM では翻訳コンテンツ（XML 形式）の手動による抽出と再挿入がサポートされます。

>[!NOTE]
>
>言語コピー機能を使用するには、ユーザーが`project-administrators`グループのメンバーである必要があります。

## ベストプラクティス {#best-practices}

[翻訳のベストプラクティス](best-practices.md)ページには、導入に関する重要な情報が記載されています。
