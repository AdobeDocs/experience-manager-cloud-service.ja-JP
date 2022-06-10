---
title: ''' [!DNL Adobe Workfront] との [!DNL Experience Manager Assets] 統合'''
description: ' [!DNL Assets]  と  [!DNL Workfront] の統合の概要'
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 8dd16d0ef18cba90417fe97bc51a1d3de899296f
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 96%

---

# [!DNL Adobe Workfront] との [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 統合 {#assets-integration-overview}

[!DNL Adobe Workfront] は作業管理アプリケーションで、作業のライフサイクル全体を一元的に管理するのに役立ちます。[!DNL Workfront] と [!DNL Adobe Experience Manager Assets] の統合により、組織は、作業とデジタルアセット管理を本質的に関連付けることで、コンテンツベロシティを向上させ市場投入までの時間を短縮することができます。Workfront での作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

[!DNL Workfront for Experience Manager enhanced connector] により、エンドツーエンドのワークフローでビジネスプロセスが強化され、エンドツーエンドのクライアントエクスペリエンスと一元化されたストレージをパーソナライズできます。アドビでは、標準コネクタと、これら 2 つのソリューションを統合する拡張コネクタを提供します。 比較については、以下のサポートされる機能を参照し、[ [!DNL enhanced connector]の新機能を参照してください](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)。

[!DNL Workfront for Experience Manager enhanced connector] を使用すると、組織で次のことが可能です。

* Workfront でリンクされた Experience Manager フォルダーを自動作成し、Workfront のポートフォリオ、プログラム、プロジェクトに基づいてフォルダーを整理します。
* Workfront プロジェクトメタデータをリンクされた Experience Manager フォルダーと同期してください。
* Experience Manager メタデータを新しいバージョンで更新します。
* Experience Manager ワークフローを使用して、設定可能な条件に基づいて Workfront オブジェクトのステータスを設定してください。
* アセットを Experience Manager パブリッシュ環境または Brand Portal に公開します。

プラットフォームのサポートと[拡張コネクターの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)を参照してください。

>[!IMPORTANT]
>
>* アドビでは、[!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと設定を、認定パートナーまたは [!DNL Adobe Professional Services] を通じてのみ行うことを求めています。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* Adobeは、拡張コネクタバージョン 1.7.4 以降をサポートしています。 以前のプレリリースおよびカスタムバージョンはサポートされていません。 拡張コネクタのバージョンを確認するには、次の手順 5(a) を参照してください： [コネクタのインストール手順の強化](workfront-connector-install.md).
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、 [試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## [!DNL Assets] と [!DNL Workfront] の間の異なる統合の比較  {#feature-parity-matrix}

[!DNL Assets] と [!DNL Workfront] の間の様々なタイプの統合を通じて利用できる機能の詳細は、以下のとおりです。

| 機能 | 説明 | [!DNL Workfront] および [!DNL Assets Essentials] | [!DNL Experience Manager] コネクターの [!DNL Workfront] | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| デプロイメント方法 | どの [!DNL Assets] の提供に適切か。 | Assets Essentials | Cloud Service、Adobe Managed Services、オンプレミス | Cloud Service、Adobe Managed Services、オンプレミス |
| [!DNL Workfront] から [!DNL Assets] へのデジタルファイルの送信  | WF ドキュメントの最新バージョンを AEM Assets にアップロードして、ドキュメントの新しいバージョンとしてリンクさせることができます。 | ✓ | ✓ | ✓ |
| AEM フォルダーの Workfront オブジェクトへの手動リンク | 既存の AEM フォルダーは Workfront フォルダーとしてリンクでき、その子アセットは新しい Workfront ドキュメントとしてリンクされます。 | ✓ | ✓ | ✓ |
| [!DNL Assets] を Workfront オブジェクトにリンク | AEM 内の既存のアセットを新しい Workfront ドキュメントにリンクしたり、既存のドキュメントの新しいバージョンとしてリンクしたりできます。 | ✓ | ✓ | ✓ |
| リンクされたフォルダーに追加されたアセットは、AEM に自動的に送信されます | リンクされたフォルダーにドキュメントを追加すると、関連するアセットが新しいアセットとして AEM Assets に自動的にアップロードされます。 | ✓ | ✓ | ✓ |
| Workfront 内からリンクされた AEM Assets をダウンロード | Workfront 内でアセットをリンクすると、ユーザーはアセットのバイトをダウンロードできます。 | ✓ | ✓ | ✓ |
| Workfront 内から AEM Assets を検索 | Workfront の AEM Assets セレクターを使用すると、アセットのフルテキスト検索が可能になります。 | ✓ | ✓ | ✓ |
| Workfront 内から AEM フォルダー階層を表示し、階層内を移動する | Workfront の AEM Assets セレクターを使用すると、AEM で設定されたユーザーの関連するアクセス制御および権限によって制限される AEM Assets 階層を参照できます。 | ✓ | ✓ | ✓ |
| Workfront の AEM Assets からアセットのリンクを解除 | AEM の既存のリンクされたアセットのリンクを、関連する Workfront ドキュメントから解除できます。 AEM 内の元のアセットは削除されません。 | ✓ | ✓ | ✓ |
| Workfront から AEM Assets に新しくバージョン管理されたアセットを追加 | Workfront のドキュメントに新しく追加されたバージョンが追加された場合、ユーザーは新しいバージョンを AEM に送信して、既存のバージョンに置き換えることができます。 | ✓ | ✓ | ✓ |
| 「ユーザーを AEM に誘導」をクリックしたときに Workfront でリンクされたアセット | ユーザーは、Workfront 内からリンクされたアセットをプレビューするように AEM に誘導されます。 | ✓ | ✓ | カスタム |
| Workfront 内のリンクされた AEM フォルダーを自動的に作成 | オブジェクトのステータスを使用して、Workfront 内にリンクされた AEM フォルダーを自動的に作成します。 Workfront のポートフォリオ、プログラム、プロジェクトに基づいて、AEM フォルダーを自動的に整理します。 | いいえ | 不可 | ✓ |
| コメントの同期 | アセットのコメントを [!DNL Workfront] から [!DNL Assets] への自動的に同期 | 不可 | ✓ | ✓ |
| Workfront のアセットメタデータの AEM Assets へのマッピング | Workfront オブジェクトおよびカスタムフォームプロパティは、AEM のアセットメタデータプロパティにマッピングできます。値は、最初のアップロード／リンク時にプッシュされます。 | ✓ | ✓ | ✓ |
| Workfront でドキュメントのカスタムフォームを自動的に作成 | AEM ワークフローを使用して、Workfront のドキュメント、タスク、問題にカスタムフォームを添付します。 | 不可 | 手動でカスタムフォームを追加すると、自動同期が機能します | ✓ |
| AEM Assets と Workfront の間でメタデータを双方向に自動更新 | AEM Assets と Workfront の間でメタデータを自動的に更新します。 | 不可 | ✓ | ✓ |
| Workfront メタデータ を AEM Assets フォルダーへマッピング | Workfront プロジェクトのメタデータを、リンクされた AEM フォルダーと同期します。 | いいえ | 不可 | ✓ |
| 新しいバージョンで AEM メタデータを更新 | AEM の設定を行うことにより、Workfront のアセットのバージョンが新しくなった場合にも、メタデータに加えられた変更をプッシュするかどうかを指定できます。 | いいえ | 不可 | ✓ |
| Workfront のカスタムフォームが変更されると AEM メタデータを自動的に更新 | 指定した AEM のアセットのメタデータプロパティが、ドキュメントのカスタムフォームにマッピングされるように Workfront を設定します。アセットが最初にリンクされる際、またはアセットが更新される際に、メタデータプロパティの値が、対応する Workfront のドキュメントのカスタムフォームフィールドにコピーされます。AEM からの変更が、あたかも Workfront から起こった変更かのように、AEM に送り返されないように注意する必要があります。 | 不可 | ✓ | ✓ |
| リンクされたアセットに新しい配達確認バージョンを作成 | Workfront でアセットをリンクすると、配達確認を自動的に生成できます。 | 不可 | ✓ | カスタム |
| Workfront オブジェクトのステータスを設定 | AEM ワークフローを使用して、設定可能な条件に基づく Workfront オブジェクトのステータスを設定します。 | いいえ | 不可 | ✓ |
| AEM パブリッシュ環境または Brand Portal にアセットを公開 | リンクされたアセットを AEM パブリッシュ環境または Brand Portal に自動的に公開するオプションをWorkfront ユーザーに与えます。 | いいえ | 不可 | ✓ |
