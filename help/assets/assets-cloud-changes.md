---
title: Adobe Experience Manager Assets as a の主な変更点 [!DNL Cloud Service]
description: Experience Manager [!DNL Cloud Service] のAdobe Experience Manager資産に対する顕著な変更は、Adobe Experience Manager6.5に比べて<a0/>です。
translation-type: tm+mt
source-git-commit: 0838f384b31c59fe95087e1a71741656eedcd13b
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 63%

---


# Experience Manager Assets as a の主な変更点 [!DNL Cloud Service] {#notable-changes}

[!DNL Cloud Service]としてのAdobe Experience Managerは、Experience Managerプロジェクトを管理するための新機能と可能性を数多く提供します。 Experience Managerアセットは、オンプレミスまたはAdobe管理サービスとしてホストされるものと、[!DNL Experience Manager]は[!DNL Cloud Service]としてホストされるものとで多くの違いがあります。 この記事では、[!DNL Assets]機能の重要な違いについて説明します。

[Experience Manager] 6.5との主な違いは次のとおりです。

* [アセットの取り込み、アップロードおよび処理](#asset-ingestion)。
* [クラウドネイティブ処理用のアセットマイクロサービス](#asset-microservices)。
* [クラシック UI の削除](#classic-ui)。

## アセットの取り込みと処理{#asset-ingestion}

アセットの取り込みの拡大・縮小、アップロードの高速化、マイクロサービスを使用した処理の高速化、一括取り込みを可能にすることで、アセットのアップロードが効率化されました。 製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されました。ただし、これによって、一部の既存カスタマイズが影響を受ける可能性があります。

* Adobe Experience Manager では、アップロードとダウンロードに直接バイナリアクセスの原則を使用し、アセットの処理にアセットマイクロサービスを使用します。[アセットの取り込みの概要](/help/assets/asset-microservices-overview.md)を参照してください。
   * [直接バイナリアクセスを使用した](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)アセットのアップロード。
   * 技術的な詳細については、[直接バイナリアップロードのプロトコルと API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください.
   * 基本的なCRUD操作に使用できるAPIメソッドの比較については、[APIとアセット操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)を参照してください。
* 以前のバージョンの に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。[!DNL Experience Manager]代わりに、アセットマイクロサービスは、デフォルトのアセット処理(レンディション、メタデータ抽出、インデックス作成用のテキスト抽出)のほとんどをカバーする、スケーラブルで、容易に利用できるサービスを提供します。
   * [アセットマイクロサービスの設定および使用方法](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。
* パッケージマネージャーで取り込まれたアセットについては、Assets インターフェイスの「**[!UICONTROL アセットを再処理]**」アクションを使用して、手動で再処理する必要があります。

アセットマイクロサービスで生成された標準レンディションは、後方互換性のある方法でアセットリポジトリノードに保存されます（同じ命名規則が使用されます）。

## アセットマイクロサービスの開発とテスト {#asset-microservices}

アセットマイクロサービスは、クラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。アドビは、様々なアセットタイプや処理オプションを最適に処理するための Cloud Services を管理します。アセットマイクロサービスを利用すると、サードパーティ製のレンダリングツールやメソッド（ImageMagick など）が不要になり、システムの設定が簡単になると同時に、一般的なファイルタイプにそのまま使用できる機能が提供されます。以前のバージョンの Experience Manager で可能だったよりも幅広く、[様々なファイルタイプ](/help/assets/file-format-support.md)の形式を追加設定なしで処理できるようになりました。例えば、以前は ImageMagick などのサードパーティソリューションが必要だった PSD 形式と PSB 形式を、サムネール抽出できるようになりました。ImageMagick の複雑な設定は、[!UICONTROL 処理プロファイル]の設定に使用できません。ビデオの高度なFmpegトランスコードには[!DNL Dynamic Media]を、MP4ビデオの基本的なトランスコードには[処理プロファイルを使用します](/help/assets/manage-video-assets.md#transcode-video)。

アセットマイクロサービスは、Cloud Manager で管理されるユーザープログラムと環境にある Adobe Experience Manager に自動的にプロビジョニングして接続される、クラウドネイティブなサービスです。Adobe Experience Manager の拡張やカスタマイズをおこなう場合、開発者は、既存のコンテンツまたはクラウド環境で生成されたレンディションを含んだアセットを使用して、アセットの使用、表示、ダウンロードをおこなうコードをテストし検証できます。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証をおこなうには、コードの変更を[パイプライン](/help/implementing/cloud-manager/configure-pipeline.md)を使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## クラシック UI の削除 {#classic-ui}

Classic UIは、Experience Managerでは[!DNL Cloud Service]として使用できなくなりました。 標準のインターフェイスは、タッチ対応 UI です。

>[!MORELIKETHIS]
>
>* [の [!DNL Adobe Experience Manager] 紹介 [!DNL Cloud Service]](/help/overview/introduction.md)
>* [ [!DNL Experience Manager] as a [!DNL Cloud Service] の概要 — 新機能と異なる機能](/help/overview/what-is-new-and-different.md)
>* [!DNL Experience Manager]の[アーキテクチャ](/help/core-concepts/architecture.md)は[!DNL Cloud Service]として
>* [の主な変更点 [!DNL Experience Manager] は、 [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md)
>* [の主な変更点 [!DNL Experience Manager Sites] は、 [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

