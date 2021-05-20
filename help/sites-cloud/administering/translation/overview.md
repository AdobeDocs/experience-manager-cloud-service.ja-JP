---
title: 多言語サイトのコンテンツの翻訳
description: 多言語サイトのコンテンツの翻訳方法の概要を説明します。
feature: 言語コピー
role: Administrator
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 50%

---

# 多言語サイトのコンテンツの翻訳 {#translating-content-for-multilingual-sites}

多言語のWebサイトを作成および管理するために、ページコンテンツとアセットの翻訳を自動化します。 翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、コンテンツを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

* **人間による翻訳：** コンテンツは翻訳プロバイダーに送信され、専門の翻訳者によって翻訳されます。完了すると、翻訳されたコンテンツが返され、AEMに読み込まれます。翻訳プロバイダーがAEMと統合されると、AEMと翻訳プロバイダーの間でコンテンツが自動的に送信されます。
* **機械翻訳：** 機械翻訳サービスは、コンテンツを直ちに翻訳します。

コンテンツの翻訳には次の手順が含まれます。

1. [AEM を翻訳プロバイダーサービスに接続](integration-framework.md#connecting-to-a-translation-service-provider)して、[翻訳統合フレームワーク設定を作成](integration-framework.md)します。
1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](integration-framework.md#configuring-pages-for-translation)ます。
1. [翻訳するコンテンツのタ](rules.md) イプを指定します。
1. [翻訳するコンテンツを準備](preparation.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。
1. [翻訳プロジェ](managing-projects.md) クトを作成して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。
1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](managing-projects.md)します。

AEM との統合のためのコネクターが翻訳サービスプロバイダーに用意されていない場合、AEM では翻訳コンテンツ（XML 形式）の手動による抽出と再挿入がサポートされます。

>[!NOTE]
>
>言語コピー機能を使用するには、ユーザーが`project-administrators`グループのメンバーである必要があります。

## ベストプラクティス {#best-practices}

[翻訳のベストプラクティス](best-practices.md)ページには、実装に関する重要な情報が含まれています。
