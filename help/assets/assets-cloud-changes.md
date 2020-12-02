---
title: Adobe Experience Manager Assets as a の主な変更点 [!DNL Cloud Service]
description: AEM [!DNL Cloud Service] のAdobe Experience Manager資産に対する顕著な変更点は、Adobe Experience Manager6.5と比較してa0/>です。
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 80%

---


# Experience Manager Assets as a の主な変更点 [!DNL Cloud Service] {#notable-changes}

[!DNL Cloud Service]としてのAdobe Experience Managerは、AEMプロジェクトを管理するための新機能と可能性を数多く提供します。 ただし、Experience ManagerアセットのオンプレミスとAdobe管理サービスの間には、[!DNL Cloud Service]としてのExperience Managerと比べて多くの違いがあります。 このドキュメントでは、Assets 機能の重要な違いについて説明します。

Adobe Experience Manager 6.5 との主な違いは次の点です。

* [アセットの取り込みとアップロード](#asset-ingestion)。
* [クラウドネイティブ処理用のアセットマイクロサービス](#asset-microservices)。
* [クラシック UI の削除](#classic-ui)。

>[!NOTE]
>
>このドキュメントでは、AEM Assets の主な変更点について重点的に説明します。[!DNL Cloud Service]や他のモジュールとしてのExperience Managerに関する一般的な変更点については、以下を参照してください。
>
>* [Adobe Experience Manager as a の概要 [!DNL Cloud Service]](/help/overview/introduction.md)
>* [AEMの概要 [!DNL Cloud Service]  — 新機能と違い](/help/overview/what-is-new-and-different.md)
>* [Adobe Experience Manager as a のアーキテクチャ](/help/core-concepts/architecture.md)[!DNL Cloud Service]
>* [AEMに対する主な変更点 [!DNL Cloud Service] （リリースノート）](/help/release-notes/aem-cloud-changes.md)
>* [～としてのAEM Sitesの顕著な変化 [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [チュートリアル [!DNL Cloud Service] としてのAdobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


## アセットの取り込みとアップロード {#asset-ingestion}

アセットのアップロードが効率化のために最適化され、アセット取り込みの規模をより適切に拡大／縮小できるようになったほか、アップロードが高速化されました。製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されました。ただし、これによって、一部の既存カスタマイズが影響を受ける可能性があります。

* Adobe Experience Manager では、アップロードとダウンロードに直接バイナリアクセスの原則を使用し、アセットの処理にアセットマイクロサービスを使用します。[アセットの取り込みの概要](/help/assets/asset-microservices-overview.md)を参照してください。
   * [直接バイナリアクセスを使用した](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)アセットのアップロード。
   * 技術的な詳細については、[直接バイナリアップロードのプロトコルと API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください.
* 以前のバージョンの AEM に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。代わりに、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどに対応できる、拡張性と可用性の高いサービスをアセットマイクロサービスが提供します。
   * [アセットマイクロサービスの設定および使用方法](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。
* パッケージマネージャーで取り込まれたアセットについては、Assets インターフェイスの「**[!UICONTROL アセットを再処理]**」アクションを使用して、手動で再処理する必要があります。

アセットマイクロサービスで生成された標準レンディションは、後方互換性のある方法でアセットリポジトリノードに保存されます（同じ命名規則が使用されます）。

## アセットマイクロサービスの開発とテスト {#asset-microservices}

アセットマイクロサービスは、クラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。アドビは、様々なアセットタイプや処理オプションを最適に処理するための Cloud Services を管理します。アセットマイクロサービスを利用すると、サードパーティ製のレンダリングツールやメソッド（ImageMagick など）が不要になり、システムの設定が簡単になると同時に、一般的なファイルタイプにそのまま使用できる機能が提供されます。以前のバージョンの Experience Manager で可能だったよりも幅広く、[様々なファイルタイプ](/help/assets/file-format-support.md)の形式を追加設定なしで処理できるようになりました。例えば、以前は ImageMagick などのサードパーティソリューションが必要だった PSD 形式と PSB 形式を、サムネール抽出できるようになりました。ImageMagick の複雑な設定は、[!UICONTROL 処理プロファイル]の設定に使用できません。ビデオの FFmpeg トランスコードに [!DNL Dynamic Media] を使用し、[MP4 ビデオの基本的なトランスコード](/help/assets/manage-video-assets.md#transcode-video)に処理プロファイルを使用します。

アセットマイクロサービスは、Cloud Manager で管理されるユーザープログラムと環境にある Adobe Experience Manager に自動的にプロビジョニングして接続される、クラウドネイティブなサービスです。Adobe Experience Manager の拡張やカスタマイズをおこなう場合、開発者は、既存のコンテンツまたはクラウド環境で生成されたレンディションを含んだアセットを使用して、アセットの使用、表示、ダウンロードをおこなうコードをテストし検証できます。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証をおこなうには、コードの変更を[パイプライン](/help/implementing/cloud-manager/configure-pipeline.md)を使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## クラシック UI の削除 {#classic-ui}

Classic UIは、Experience Managerでは[!DNL Cloud Service]として使用できなくなりました。 標準のインターフェイスは、タッチ対応 UI です。
