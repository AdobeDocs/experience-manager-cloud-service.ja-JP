---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: A と B の統合の概要 [!DNL Assets] および [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: d75d9ac16f64b6770fcf35d58474c47c52b1585b
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] ～との統合 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] は、作業のライフサイクル全体を 1 か所で管理するのに役立つ作業管理アプリケーションです。 次の間の統合： [!DNL Workfront] および [!DNL Adobe Experience Manager Assets] 企業は、業務とデジタルアセット管理を本質的に結び付けることで、コンテンツの速度と市場投入までの時間を改善できます。 Workfrontでの作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

Adobeは、両方のソリューションを統合するための 2 種類のコネクタを提供します。 コネクタにより、複雑な企業の自動化、設定、拡張可能なワークフローを実現 [!DNL Assets] および [!DNL Workfront]. さらに、 [!DNL Assets Essentials] は、新しい [!DNL Workfront] 顧客は個別に購入できます。 詳しくは、 [[!DNL Workfront] and [!DNL Assets Essentials] 統合](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/integration.html).

[!DNL Workfront for Experience Manage enhanced connector] 組織では、次のことが可能です。

* 簡単に共同作業できます。 クリエイティブチームは、1 つ少ないことについて心配することができます。 作業が完了すると、ボタンをクリックしてAEM Assetsに送信できます。
* 各手順でアセットをエンリッチメントします。 アセットライフサイクルの各段階で新しいデータを収集します。 アイディエーションから配信に至るまで、組織は主要指標をキャプチャし、情報に基づいて将来のアセット開発に関するビジネス上の意思決定をおこなうことができます。
* 既存のアセットを参照します。 実稼動環境で既存のアセットを簡単に検索して再利用し、参照アイテムとして新しいプロジェクトに追加できます。
* すべてのメタデータを同期します。 メタデータをできるだけ簡単に追加できるようにして、メタデータを拡張します。 コネクタを使用すると、メタデータはWorkfrontとAEM Assetsの間で双方向的に同期されます
* 活用 [!DNL Experience Manager Assets] デジタル管理機能。 お気に入り内ですべてのデジタルアセットに直接アクセス [!DNL Creative Cloud] アプリケーション。 AI 対応のスマートタグ付けと切り抜き、検索ツール、動的配信 [!DNL Dynamic Media]そして、その他多くを。

プラットフォームのサポートとその他の情報を見る [拡張コネクタの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobeには、 [!DNL Adobe Workfront for Experience Manager enhanced connector] 認定パートナーまたは [!DNL Adobe Professional Services]. 認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobeではサポートされません。
>
>Adobeが次の更新をリリースする可能性がある： [!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] これにより、このコネクタは冗長になります。この場合、お客様はこのコネクタの使用から移行する必要が生じる場合があります。

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
| WorkfrontでリンクされたAEMフォルダーを自動的に作成 | オブジェクトのステータスを使用して、Workfront内にリンクされたAEMフォルダーを自動的に作成します。 WorkfrontのPortfolio、プログラム、プロジェクトに基づいて、AEMフォルダーを自動的に整理します。 | 不可 | 不可 | ✓ |
| コメントの同期 | からのアセットのコメントを自動的に同期 [!DNL Workfront] から [!DNL Assets] | 不可 | ✓ | ✓ |
| WorkfrontのアセットメタデータのAEM Assetsへのマッピング | Workfrontオブジェクトおよびカスタムフォームプロパティは、AEMのアセットメタデータプロパティにマッピングできます。 値は、最初のアップロード/リンク時にプッシュされます。 | ✓ | ✓ | ✓ |
| WorkfrontでドキュメントのカスタムFormsを自動的に作成 | AEMワークフローを使用して、Workfrontのドキュメント、タスクおよび問題にカスタムフォームを添付します。 | 不可 | カスタムフォームを手動で追加し、自動同期が機能する | ✓ |
| AEM AssetsとWorkfrontの間でのメタデータの双方向の自動更新 | AEM AssetsとWorkfrontの間でメタデータを自動的に更新します。 | 不可 | ✓ | ✓ |
| WorkfrontメタデータのAEM Assetsフォルダーへのマッピング | WorkfrontプロジェクトメタデータをリンクされたAEMフォルダーと同期します。 | 不可 | 不可 | ✓ |
| 新しいバージョンでのAEMメタデータの更新 | AEMの設定を使用して、Workfrontの新しくバージョン管理されたアセットも、そのメタデータに加えられた変更をプッシュするかどうかを指定できます。 | 不可 | 不可 | ✓ |
| WorkfrontのカスタムFormsに対する変更に基づいて、AEMメタデータを自動的に更新 | Workfrontは、指定したAEMのアセットメタデータプロパティがドキュメントのカスタムフォームにマッピングされるように設定されます。 アセットが最初にリンクされたとき、またはアセットが更新されたときに、これらのメタデータプロパティの値が、対応するWorkfrontドキュメントのカスタムフォームフィールドにコピーされます。 変更がAEMからAEMに送り返されるのを防ぐために、Workfrontに起因する変更と同じように、注意が必要です。 | 不可 | ✓ | ✓ |
| リンクされたアセットに新しい配達確認バージョンを作成 | Workfrontでアセットをリンクする際に、配達確認を自動的に生成できます。 | 不可 | ✓ | カスタム |
| Workfrontオブジェクトでのステータスの設定 | AEMワークフローを使用した、Workfrontオブジェクトのステータスに基づく設定可能な条件の設定 | 不可 | 不可 | ✓ |
| AEM パブリッシュ環境またはBrand Portalにアセットを公開する | Workfrontユーザーに、リンクされたアセットを AEM パブリッシュ環境またはBrand Portalに自動的に公開するオプションを与えます。 | 不可 | 不可 | ✓ |
