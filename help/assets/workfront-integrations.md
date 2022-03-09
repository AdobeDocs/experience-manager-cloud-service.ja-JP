---
title: '''[!DNL Experience Manager Assets] ～との統合 [!DNL Adobe Workfront]'''
description: A と B の統合の概要 [!DNL Assets] および [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: b6e108296d6786166e482cd8bbd20caa36795f44
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] ～との統合 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] は、作業のライフサイクル全体を 1 か所で管理するのに役立つ作業管理アプリケーションです。 次の間の統合： [!DNL Workfront] および [!DNL Adobe Experience Manager Assets] 企業は、業務とデジタルアセット管理を本質的に結び付けることで、コンテンツの速度と市場投入までの時間を改善できます。 Workfrontでの作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

この [!DNL Workfront for Experience Manager enhanced connector] エンドツーエンドのワークフローにより、ビジネスプロセスが強化され、エンドツーエンドのクライアントエクスペリエンスと一元化されたストレージをパーソナライズできます。 Adobeは、標準コネクタと、これら 2 つのソリューションを統合する拡張コネクタを提供します。 比較については、以下のサポートされる機能を参照し、 [の新機能 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manager enhanced connector] 組織では、次のことが可能です。

* WorkfrontでリンクされたExperience Managerフォルダーを自動作成し、WorkfrontのPortfolio、プログラム、プロジェクトに基づいてフォルダーを整理します。
* WorkfrontプロジェクトメタデータをリンクされたExperience Managerフォルダーと同期します。
* Experience Managerメタデータが新しいバージョンで更新されました。
* Experience Managerワークフローを使用して、設定可能な条件に基づいてWorkfrontオブジェクトのステータスを設定します。
* アセットをExperience Managerパブリッシュ環境またはBrand Portalに公開します。

プラットフォームのサポートを参照し、 [拡張コネクタの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobeには、 [!DNL Adobe Workfront for Experience Manager enhanced connector] 認定パートナーまたは [!DNL Adobe Professional Services]. 認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobeではサポートされません。
>
>Adobeが次の更新をリリースする可能性がある： [!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] このコネクタを冗長にするこの場合、お客様はこのコネクタの使用から移行する必要が生じる場合があります。
>
>詳しくは、 [Workfront for Experience Manager Assets拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 試験の詳細は、 [試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## A と B の間の異なる統合の比較 [!DNL Assets] および [!DNL Workfront] {#feature-parity-matrix}

次に、 [!DNL Assets] および [!DNL Workfront].

| 機能 | 説明 | [!DNL Workfront] および [!DNL Assets Essentials] | [!DNL Workfront] 対象 [!DNL Experience Manager] コネクタ | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| デプロイメント方法 | 適切な対象 [!DNL Assets] 提供 | Assets Essentials | Cloud Service、Adobe Managed Services、オンプレミス | Cloud Service、Adobe Managed Services、オンプレミス |
| からのデジタルファイルの送信 [!DNL Workfront] から [!DNL Assets] | WF ドキュメントの最新バージョンをAEM Assetsにアップロードして、ドキュメントの新しいバージョンとしてリンクさせることができます。 | ✓ | ✓ | ✓ |
| AEMフォルダーのWorkfrontオブジェクトへの手動リンク | 既存のAEMフォルダーはWorkfrontフォルダーとしてリンクでき、その子アセットは新しいWorkfrontドキュメントとしてリンクされます。 | ✓ | ✓ | ✓ |
| リンク [!DNL Assets] Workfront Objects | AEM内の既存のアセットを新しいWorkfrontドキュメントにリンクしたり、既存のドキュメントの新しいバージョンとしてリンクしたりできます。 | ✓ | ✓ | ✓ |
| リンクされたフォルダーに追加されたアセットは、AEMに自動的に送信されます | ドキュメントがリンクされたフォルダーに追加されている場合、関連するアセットが新しいアセットとしてAEM Assetsに自動的にアップロードされます。 | ✓ | ✓ | ✓ |
| Workfront内から Linked AEM Assetsをダウンロード | Workfrontでアセットをリンクすると、ユーザーはアセットのバイトをダウンロードできます。 | ✓ | ✓ | ✓ |
| Workfront内からAEM Assetsを検索 | WorkfrontのAEM Assetsセレクターを使用すると、アセットのフルテキスト検索が可能になります。 | ✓ | ✓ | ✓ |
| Workfront内からAEMフォルダー階層を表示および移動する | WorkfrontのAEM Assetsセレクターを使用すると、AEMで設定されたユーザーの関連するアクセス制御および権限によって制限されるAEM Assets階層を参照できます。 | ✓ | ✓ | ✓ |
| WorkfrontのAEM Assetsからアセットのリンクを解除 | AEMの既存のリンクされたアセットのリンクを、関連するWorkfrontドキュメントから解除できます。 AEM内の元のアセットは削除されません。 | ✓ | ✓ | ✓ |
| WorkfrontからAEM Assetsに新しくバージョン管理されたアセットを追加 | Workfrontのドキュメントに新しく追加されたバージョンが追加された場合、ユーザーは新しいバージョンをAEMに送信して、既存のバージョンに置き換えることができます。 | ✓ | ✓ | ✓ |
| 「直接ユーザー」をクリックしてAEMにリンクされたアセット | Workfront内から、リンクされたアセットをプレビューするためのAEMへのユーザー向けの画面です。 | ✓ | ✓ | カスタム |
| WorkfrontでリンクされたAEMフォルダーを自動的に作成 | オブジェクトのステータスを使用して、Workfront内にリンクされたAEMフォルダーを自動的に作成します。 WorkfrontのPortfolio、プログラム、プロジェクトに基づいて、AEMフォルダーを自動的に整理します。 | 不可 | いいえ | ✓ |
| コメントの同期 | からのアセットのコメントを自動的に同期 [!DNL Workfront] から [!DNL Assets] | いいえ | ✓ | ✓ |
| WorkfrontのアセットメタデータのAEM Assetsへのマッピング | Workfrontオブジェクトおよびカスタムフォームプロパティは、AEMのアセットメタデータプロパティにマッピングできます。 値は、最初のアップロード/リンク時にプッシュされます。 | ✓ | ✓ | ✓ |
| WorkfrontでドキュメントのカスタムFormsを自動的に作成 | AEMワークフローを使用して、Workfrontのドキュメント、タスクおよび問題にカスタムフォームを添付します。 | いいえ | カスタムフォームを手動で追加し、自動同期が機能する | ✓ |
| AEM AssetsとWorkfrontの間でのメタデータの双方向の自動更新 | AEM AssetsとWorkfrontの間でメタデータを自動的に更新します。 | いいえ | ✓ | ✓ |
| WorkfrontメタデータのAEM Assetsフォルダーへのマッピング | WorkfrontプロジェクトメタデータをリンクされたAEMフォルダーと同期します。 | 不可 | いいえ | ✓ |
| 新しいバージョンでのAEMメタデータの更新 | AEMの設定を使用して、Workfrontの新しくバージョン管理されたアセットも、そのメタデータに加えられた変更をプッシュするかどうかを指定できます。 | 不可 | いいえ | ✓ |
| WorkfrontのカスタムFormsに対する変更に基づいて、AEMメタデータを自動的に更新 | Workfrontは、指定したAEMのアセットメタデータプロパティがドキュメントのカスタムフォームにマッピングされるように設定されます。 アセットが最初にリンクされたとき、またはアセットが更新されたときに、これらのメタデータプロパティの値が、対応するWorkfrontドキュメントのカスタムフォームフィールドにコピーされます。 変更がAEMからAEMに送り返されるのを防ぐために、Workfrontに起因する変更と同じように、注意が必要です。 | いいえ | ✓ | ✓ |
| リンクされたアセットに新しい配達確認バージョンを作成 | Workfrontでアセットをリンクする際に、配達確認を自動的に生成できます。 | いいえ | ✓ | カスタム |
| Workfrontオブジェクトでのステータスの設定 | AEMワークフローを使用した、Workfrontオブジェクトのステータスに基づく設定可能な条件の設定 | 不可 | いいえ | ✓ |
| AEM パブリッシュ環境またはBrand Portalにアセットを公開する | Workfrontユーザーに、リンクされたアセットを AEM パブリッシュ環境またはBrand Portalに自動的に公開するオプションを与えます。 | 不可 | いいえ | ✓ |
