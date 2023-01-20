---
title: ' [!DNL Adobe Workfront] との [!DNL Experience Manager Assets] 統合'
description: ' [!DNL Assets]  と  [!DNL Workfront] の統合の概要'
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 269dff32b41dba86fb048418da3f3b3ef8a6781e
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 63%

---

# [!DNL Adobe Workfront] との [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 統合 {#assets-integration-overview}

[!DNL Adobe Workfront] は作業管理アプリケーションで、作業のライフサイクル全体を一元的に管理するのに役立ちます。[!DNL Workfront] と [!DNL Adobe Experience Manager Assets] の統合により、組織は、作業とデジタルアセット管理を本質的に関連付けることで、コンテンツベロシティを向上させ市場投入までの時間を短縮することができます。Workfront での作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

Adobe [統合 [!DNL Workfront] および [!DNL Adobe Experience Manager Assets] ネイティブ (Assets Essentialsと Assetsas a Cloud Serviceをサポート )、またはWorkfront for Assets 拡張コネクタの使用](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). ネイティブ統合の場合、2 つのソリューションを統合するためのコネクタは必要ありません。

>[!NOTE]
>
>Adobeは、Experience Manager強化コネクタとExperience Managerの統合に対するWorkfrontの並行使用をサポートしていません。

ネイティブExperience Manager統合と [!DNL Workfront for Experience Manager enhanced connector]を使用すると、次のことができます。

| ネイティブ [!DNL Adobe Experience Manager Assets] 機能 | [!DNL Workfront for Experience Manager enhanced connector] features |
|---|---|
| <ul><li>Workfront内で統合をすばやく設定します。</li><li>Workfrontとフォルダーの間にリンクされたExperience Managerーを自動的に作成します。</li><li>既存のリンクされたアセットのメタデータを簡単に同期できます。</li><li>Workfrontで変更された場合に、プロジェクトメタデータを自動的に更新します。</li><li>複数のExperience Manager Assetsリポジトリを 1 つのWorkfront環境に、または複数のWorkfront環境を組織 ID をまたいで 1 つのExperience Manager Assetsリポジトリにスムーズに接続できます。</li> | <ul><li>Workfront でリンクされた Experience Manager フォルダーを自動作成し、Workfront のポートフォリオ、プログラム、プロジェクトに基づいてフォルダーを整理します。</li><li>Workfront プロジェクトメタデータをリンクされた Experience Manager フォルダーと同期してください。</li><li>Experience Manager メタデータを新しいバージョンで更新します。</li><li>Experience Manager ワークフローを使用して、設定可能な条件に基づいて Workfront オブジェクトのステータスを設定してください。</li><li>アセットを Experience Manager パブリッシュ環境または Brand Portal に公開します。</li> |

詳しくは、 [比較のために以下でサポートされている機能](#feature-parity-matrix) ネイティブ統合または統合間で、2 つのソリューション間のコネクタを使用する場合。



プラットフォームのサポートと[拡張コネクターの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)を参照してください。

>[!IMPORTANT]
>
>* アドビでは、[!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと設定を、認定パートナーまたは [!DNL Adobe Professional Services] を通じてのみ行うことを求めています。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* アドビでは、拡張コネクタバージョン 1.7.4 以降をサポートしています。以前のプレリリースバージョンやカスタムバージョンはサポートされていません。拡張コネクタのバージョンを確認するには、[拡張コネクタのインストール手順](workfront-connector-install.md)の手順 5(a) を参照してください。
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、[試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)を参照してください。


## [!DNL Assets] と [!DNL Workfront] の間の異なる統合の比較  {#feature-parity-matrix}

[!DNL Assets] と [!DNL Workfront] の間の様々なタイプの統合を通じて利用できる機能の詳細は、以下のとおりです。

| 機能 | 説明 | [!DNL Workfront] および [!DNL Assets Essentials] *コネクタなし (OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *コネクタが必要* | Workfrontと [!DNL Experience Manager as a Cloud Service] *コネクタなし (OOTB)* |
|----|----|----|-----|-----|
| デプロイメント方法 | どの [!DNL Assets] の提供に適切か。 | Assets Essentials | Cloud Service、Adobe Managed Services、オンプレミス | Cloud Service |
| **一般** |
| [!DNL Workfront] から [!DNL Assets] へのデジタルファイルの送信  | WF ドキュメントの最新バージョンを AEM Assets にアップロードして、ドキュメントの新しいバージョンとしてリンクさせることができます。 | ✓ | ✓ | ✓ |
| AEM フォルダーの Workfront オブジェクトへの手動リンク | 既存の AEM フォルダーは Workfront フォルダーとしてリンクでき、その子アセットは新しい Workfront ドキュメントとしてリンクされます。 | ✓ | ✓ | ✓ |
| [!DNL Assets] を Workfront オブジェクトにリンク | AEM 内の既存のアセットを新しい Workfront ドキュメントにリンクしたり、既存のドキュメントの新しいバージョンとしてリンクしたりできます。 | ✓ | ✓ | ✓ |
| リンクされたフォルダーに追加されたアセットは、AEM に自動的に送信されます | リンクされたフォルダーにドキュメントを追加すると、関連するアセットが新しいアセットとして AEM Assets に自動的にアップロードされます。 | ✓ | ✓ | ✓ |
| Workfront 内からリンクされた AEM Assets をダウンロード | Workfront 内でアセットをリンクすると、ユーザーはアセットのバイトをダウンロードできます。 | ✓ | ✓ | ✓ |
| Workfront 内から AEM Assets を検索 | Workfront の AEM Assets セレクターを使用すると、アセットのフルテキスト検索が可能になります。 | ✓ | ✓ | ✓ |
| Workfront内からAEMフォルダーを検索 | WorkfrontのAEM Assetsセレクターを使用すると、フォルダーのフルテキスト検索が可能になります。 | ✓ | ✓ | ✓ |
| Workfront 内から AEM フォルダー階層を表示し、階層内を移動する | WorkfrontのAEM Assetsセレクターを使用すると、AEMで設定されたユーザーの関連するアクセス制御および権限によって制限されるAEM Assets階層を参照できます。 | ✓ | ✓ | ✓ |
| AEMタイムラインでのアセットバージョンの追跡 | WorkfrontとAEMの間でドキュメントのバージョン履歴を管理します。 | ✓ | ✓ | ✓ |
| Workfront の AEM Assets からアセットのリンクを解除 | AEM の既存のリンクされたアセットのリンクを、関連する Workfront ドキュメントから解除できます。AEM 内の元のアセットは削除されません。 | ✓ | ✓ | ✓ |
| Workfront から AEM Assets に新しくバージョン管理されたアセットを追加 | Workfront のドキュメントに新しく追加されたバージョンが追加された場合、ユーザーは新しいバージョンを AEM に送信して、既存のバージョンに置き換えることができます。 | ✓ | ✓ | ✓ |
| 「ユーザーを AEM に誘導」をクリックしたときに Workfront でリンクされたアセット | ユーザーは、Workfront 内からリンクされたアセットをプレビューするように AEM に誘導されます。 | ✓ | ✓ | 今後 |
| Workfront 内のリンクされた AEM フォルダーを自動的に作成 | プロジェクトのステータスを使用して、Workfront内にリンクされたAEMフォルダーを自動的に作成します。 WorkfrontのPortfolio、プログラム、プロジェクトに基づいて、AEMフォルダーを自動的に構成します。 | 不可 | ✓ | いいえ |
| WorkfrontからAEMリポジトリーに直接移動する | ユーザーがWorkfront内で設定された使用可能なAEMリポジトリに移動できるようになります。 | ✓ | 不可 | ✓ |
| WorkfrontでのリンクされたAEMフォルダーの作成 | 「ドキュメント」タブのオプションを使用して、WorkfrontでリンクされたAEMフォルダーを手動で作成します。 | ✓ | 不可 | ✓ |
| コメントの同期 | アセットのコメントを [!DNL Workfront] から [!DNL Assets] への自動的に同期 | 不可 | ✓ | いいえ |
| 1 つのAEM環境に接続する複数のWorkfront環境をサポート | 複数のWorkfront環境のユーザーは、1 つのAEM環境に接続できます。 | ✓ | 不可 | ✓ |
| 1 つのWorkfront環境に接続する複数のAEM環境をサポート | 単一のWorkfront環境内のユーザーは、複数のAEM環境間でアセットを送信またはリンクできます。 | ✓ | ✓ | ✓ |
| **メタデータ** |
| Workfront のアセットメタデータの AEM Assets へのマッピング | Workfront オブジェクトおよびカスタムフォームプロパティは、AEM のアセットメタデータプロパティにマッピングできます。値は、最初のアップロード／リンク時にプッシュされます。 | ✓ | ✓ | ✓ |
| Workfront でドキュメントのカスタムフォームを自動的に作成 | AEM ワークフローを使用して、Workfront のドキュメント、タスク、問題にカスタムフォームを添付します。 | 不可 | ✓ | いいえ |
| AEM Assets と Workfront の間でメタデータを双方向に自動更新 | AEM Assets と Workfront の間でメタデータを自動的に更新します。双方向のメタデータ更新が適切に機能するには、最初にアセットをWorkfrontからAEMにプッシュし、WorkfrontのアセットメタデータをAEMのアセットにマッピングする必要があります。 | 不可 | ✓ | いいえ |
| AEMにマッピングされたメタデータのWorkfrontでのリアルタイム表示 | Workfrontドキュメントの詳細パネルおよびドキュメントの概要パネル内で、更新後にマッピングされたメタデータをAEMに表示します。 | ✓ | 不可 | ✓ |
| 更新されたWorkfrontメタデータのAEMへのリアルタイムプッシュ | アセットや新しいバージョンのアセットを置き換えることなく、マッピングされたWorkfrontメタデータをAEMに自動的に更新します。 | ✓ | 不可 | ✓ |
| Workfront メタデータ を AEM Assets フォルダーへマッピング | Workfront プロジェクトのメタデータを、リンクされた AEM フォルダーと同期します。 | 不可 | ✓ | ✓ |
| 新しいバージョンで AEM メタデータを更新 | AEM の設定を行うことにより、Workfront のアセットのバージョンが新しくなった場合にも、メタデータに加えられた変更をプッシュするかどうかを指定できます。 | 不可 | ✓ | いいえ |
| Workfront のカスタムフォームが変更されると AEM メタデータを自動的に更新 | AEMでは、Workfrontでドキュメントフォームの更新情報を購読できます。 その結果、Workfrontドキュメントのカスタムフォームメタデータを更新すると、マッピングされたAEMメタデータフィールドの値が変更されます。 | 不可 | ✓ | いいえ |
| **ワークフロー（標準）** |
| リンクされたアセットに新しい配達確認バージョンを作成 | Workfront でアセットをリンクすると、配達確認を自動的に生成できます。 | 不可 | カスタム | いいえ |
| Workfront オブジェクトのステータスを設定 | AEM ワークフローを使用して、設定可能な条件に基づく Workfront オブジェクトのステータスを設定します。 | 不可 | ✓ | 今後 |
| AEM パブリッシュ環境または Brand Portal にアセットを公開 | リンクされたアセットを AEM パブリッシュ環境または Brand Portal に自動的に公開するオプションをWorkfront ユーザーに与えます。 | 不可 | ✓ | 今後 |
