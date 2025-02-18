---
title: 多言語サイトのコンテンツの翻訳
description: 多言語サイトのコンテンツを翻訳する方法の概要を説明します。
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '288'
ht-degree: 100%

---

# 多言語サイトのコンテンツの翻訳 {#translating-content-for-multilingual-sites}

ページコンテンツおよびアセットの翻訳を自動化して多言語の Web サイトを作成および管理する方法を説明します。翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、コンテンツを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

* **人間による翻訳：**&#x200B;コンテンツが翻訳プロバイダーに送信され、専門の翻訳者によって翻訳されます。翻訳が完了すると、翻訳済みコンテンツが返されて、AEM に読み込まれます。翻訳プロバイダーが AEM と統合されると、AEM と翻訳プロバイダーとの間でコンテンツが自動的に送信されます。
* **機械翻訳：**&#x200B;機械翻訳サービスでは、コンテンツがすぐに翻訳されます。

>[!TIP]
>
>コンテンツの翻訳を初めて行う場合は、[AEM Sites 翻訳ジャーニー](/help/journey-sites/translation/overview.md)を参照してください。これは、AEM の強力な翻訳ツールを使用して AEM Sites コンテンツを翻訳する手順を示すガイドです。AEM や翻訳の経験がないユーザーに最適です。

コンテンツの翻訳には次の手順が含まれます。

1. [AEM を翻訳プロバイダーサービスに接続](integration-framework.md#connecting-to-a-translation-service-provider)して、[翻訳統合フレームワーク設定を作成](integration-framework.md)します。
1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](integration-framework.md#configuring-pages-for-translation)ます。
1. 翻訳する[コンテンツのタイプを特定](rules.md)します。
1. [翻訳するコンテンツを準備](preparation.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。
1. [翻訳プロジェクトを作成](managing-projects.md)して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。
1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](managing-projects.md)します。

AEM との統合のためのコネクタが翻訳サービスプロバイダーに用意されていない場合、AEM では翻訳コンテンツ（XML 形式）の手動による抽出と再挿入がサポートされます。

>[!NOTE]
>
>言語コピー機能を使用するには、ユーザーが `project-administrators` グループのメンバーである必要があります。

## ベストプラクティス {#best-practices}

[翻訳のベストプラクティス](best-practices.md)には、実装に関する重要な情報が記載されています。
