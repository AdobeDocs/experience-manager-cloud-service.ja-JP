---
title: '''[!DNL Experience Manager Assets] との  統合 [!DNL Adobe Workfront]'''
description: ' [!DNL Assets] と [!DNL Workfront]の統合の概要'
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: b6e108296d6786166e482cd8bbd20caa36795f44
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 96%

---

# [!DNL Adobe Workfront] との [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 統合 {#assets-integration-overview}

[!DNL Adobe Workfront] は作業管理アプリケーションで、作業のライフサイクル全体を一元的に管理するのに役立ちます。[!DNL Workfront] と [!DNL Adobe Experience Manager Assets] のネイティブ統合により、組織は、作業とデジタルアセット管理を本質的に関連付けることで、コンテンツベロシティを向上し、市場投入までの時間を短縮することができます。Workfront での作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

[!DNL Workfront for Experience Manager enhanced connector] により、エンドツーエンドのワークフローでビジネスプロセスが強化され、エンドツーエンドのクライアントエクスペリエンスと一元化されたストレージをパーソナライズできます。アドビは、標準コネクターと、これら 2 つのソリューションを統合する拡張コネクターを提供します。比較については、以下のサポートされる機能を参照し、[ [!DNL enhanced connector] の新機能](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)を確認してください。

[!DNL Workfront for Experience Manager enhanced connector] により、組織は以下の操作を実行できます。

* Workfront でリンクされた Experience Manager フォルダーを自動作成し、Workfront のポートフォリオ、プログラム、プロジェクトにもとづいてフォルダーを整理します。
* Workfront プロジェクトメタデータをリンクされた Experience Manager フォルダーと同期します。
* Experience Manager メタデータが新しいバージョンで更新されます。
* Experience Manager ワークフローを使用して、設定可能な条件にもとづいて Workfront オブジェクトのステータスを設定します。
* Experience Manager パブリッシュ環境または Brand Portal にアセットを公開します。

プラットフォームのサポートと [拡張コネクターの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience) を参照してください。

>[!IMPORTANT]
>
>アドビでは、[!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと設定を、認定パートナーまたは [!DNL Adobe Professional Services] を通じてのみ行うことを求めています。認定パートナーまたは [!DNL Adobe Professional Services] 以外がデプロイと設定を行った場合は、アドビのサポート対象外となります。
>
>アドビは、このコネクターを冗長にする[!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>詳しくは、 [Workfront for Experience Manager Assets拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 試験の詳細は、 [試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## [!DNL Assets] と [!DNL Workfront] の異なる統合の比較 {#feature-parity-matrix}

[!DNL Assets] と [!DNL Workfront] の間の様々なタイプの統合を通じて利用できる機能の詳細は、以下のとおりです。

| 機能 | 説明 | [!DNL Workfront] および [!DNL Assets Essentials] | [!DNL Experience Manager] コネクターの [!DNL Workfront] | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| デプロイメント方法 | 提供する [!DNL Assets] に適しています。 | Assets Essentials | Cloud Service、Adobe Managed Services、オンプレミス | Cloud Service、Adobe Managed Services、オンプレミス |
| [!DNL Workfront] から [!DNL Assets] へのデジタルファイルの送信 | AEM Assets に WF ドキュメントの最新バージョンをアップロードして、ドキュメントの新しいバージョンとしてリンクさせることができます。 | ✓ | ✓ | ✓ |
| AEM フォルダーの Workfront オブジェクトへの手動リンク | 既存の AEM フォルダーは Workfront フォルダーとしてリンクでき、その子アセットは新しい Workfront ドキュメントとしてリンクされます。 | ✓ | ✓ | ✓ |
| [!DNL Assets] の Workfront オブジェクトへのリンク | AEM 内の既存のアセットを新しい Workfront ドキュメントにリンクしたり、既存のドキュメントの新しいバージョンとしてリンクしたりできます。 | ✓ | ✓ | ✓ |
| リンクされたフォルダーに追加されたアセットの AEM への自動送信 | リンクされたフォルダーにドキュメントを追加すると、関連するアセットが新しいアセットとして AEM Assets に自動的にアップロードされます。 | ✓ | ✓ | ✓ |
| Workfront からのリンクされた AEM Assets のダウンロード | Workfront でアセットをリンクすると、ユーザーはアセット（バイト単位）をダウンロードできます。 | ✓ | ✓ | ✓ |
| Workfront 内での AEM Assets の検索 | Workfront の AEM Assets セレクターを使用すると、アセットのフルテキスト検索が可能になります。 | ✓ | ✓ | ✓ |
| Workfront 内からの AEM フォルダー階層の表示と移動 | Workfront の AEM Assets セレクターを使用すると、AEM で設定された関連するアクセス制御および権限によって制限される AEM Assets 階層を参照できます。 | ✓ | ✓ | ✓ |
| Workfront の AEM Assets からのアセットのリンク解除 | AEM の既存のリンクされたアセットのリンクを、関連する Workfront ドキュメントから解除できます。AEM 内の元のアセットは削除されません。 | ✓ | ✓ | ✓ |
| Workfront から AEM Assets への新しくバージョン管理されたアセットの追加 | Workfront のドキュメントに新しいバージョンが追加された場合、ユーザーは新しいバージョンを AEM に送信して、既存のバージョンに置き換えることができます。 | ✓ | ✓ | ✓ |
| ユーザーが AEM に移動した際の Workfront でのリンクされたアセットのプレビュー | ユーザーは、Workfront 内からリンクされたアセットをプレビューするように AEM に誘導されます。 | ✓ | ✓ | カスタム |
| Workfront でリンクされた AEM フォルダーの自動作成 | オブジェクトのステータスを使用して、Workfront 内にリンクされた AEM フォルダーを自動的に作成します。Workfront のポートフォリオ、プログラム、プロジェクトにもとづいて、AEM フォルダーを自動的に整理します。 | いいえ | いいえ | ✓ |
| コメントの同期 | アセットのコメントを [!DNL Workfront] から [!DNL Assets] に自動的に同期します。 | いいえ | ✓ | ✓ |
| Workfront のアセットメタデータの AEM Assets へのマッピング | Workfront のオブジェクトとカスタムフォームプロパティは、AEM のアセットメタデータプロパティにマッピングできます。値は、最初のアップロード／リンク時にプッシュされます。 | ✓ | ✓ | ✓ |
| Workfront でのドキュメントのカスタムフォームの自動作成 | AEM ワークフローを使用して、Workfront のドキュメント、タスクおよび問題にカスタムフォームを添付します。 | いいえ | カスタムフォームを手動で追加すると、自動的に同期されます | ✓ |
| AEM Assets と Workfront 間のメタデータの双方向での自動更新 | AEM Assets と Workfront の間でメタデータを自動的に更新します。 | いいえ | ✓ | ✓ |
| Workfront メタデータの AEM Assets フォルダーへのマッピング | Workfront プロジェクトメタデータをリンクされた AEM フォルダーと同期します。 | いいえ | いいえ | ✓ |
| 新しいバージョンでの AEM メタデータの更新 | AEM の設定を使用して、Workfront の新しくバージョン管理されたアセットも、そのメタデータに加えられた変更をプッシュするかどうかを指定できます。 | いいえ | いいえ | ✓ |
| Workfront のカスタムフォームに対する変更にもとづいた AEM メタデータの自動更新 | Workfront は、指定した AEM のアセットメタデータプロパティがドキュメントのカスタムフォームにマッピングされるように設定されます。アセットが最初にリンクされたとき、またはアセットが更新されたときに、これらのメタデータプロパティの値が、対応する Workfront ドキュメントのカスタムフォームフィールドにコピーされます。AEM からの変更が Workfront で発生した変更であるかのように、AEM に返送されないように注意する必要があります。 | いいえ | ✓ | ✓ |
| リンクされたアセットでの新しい配達確認バージョンの作成 | Workfront でアセットをリンクする際に、配達確認を自動的に生成できます。 | いいえ | ✓ | カスタム |
| Workfront オブジェクトでのステータスの設定 | AEM ワークフローを使用して、設定可能な条件にもとづいて Workfront オブジェクトのステータスを設定します。 | いいえ | いいえ | ✓ |
| AEM パブリッシュ環境または Brand Portal へのアセットの公開 | Workfront ユーザーに、リンクされたアセットを AEM パブリッシュ環境または Brand Portal に自動的に公開するオプションを提供します。 | いいえ | いいえ | ✓ |
