---
title: ' [!DNL Adobe Experience Manager Assets] を [!DNL Cloud Service]として主に変更'
description: '[!DNLAdobe Experience Manager6.5と比較した [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] の顕著な変更。'
translation-type: tm+mt
source-git-commit: 6dc6445e4019664525629fe2204d255cfee37a81
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 28%

---


# [!DNL Experience Manager Assets]を[!DNL Cloud Service] {#notable-changes}として注目すべき変更

[!DNL Adobe Experience Manager] は、Experience Managerプロジェクトを管理するための多くの新機能と可能性を [!DNL Cloud Service] 提供します。[!DNL Experience Manager Assets]社内またはAdobe管理サービスとしてホストされる[!DNL Experience Manager]と[!DNL Cloud Service]社との間には多くの違いがあります。 この記事では、[!DNL Assets]機能の重要な違いについて説明します。

[Experience Manager] 6.5との主な違いは次のとおりです。

* [アセットの取り込み、アップロードおよび処理](#asset-ingestion)。
* [クラウドネイティブ処理用のアセットマイクロサービス](#asset-microservices)。
* [クラシック UI の削除](#classic-ui)。

## アセットの取り込みと処理{#asset-ingestion}

アセットのアップロードは、取り込みの拡大・縮小、アップロードの高速化、マイクロサービスを使用した処理の高速化、一括取り込みを可能にすることで、効率を向上させるために最適化されています。 製品機能（Webユーザーインターフェイス、デスクトップクライアント）が更新されます。 また、これは既存のカスタマイズの一部に影響を与える場合があります。

* [!DNL Experience Manager] 直接バイナリアクセスの原則を使用してアセットをアップロードおよびダウンロードし、アセットの処理にasset microservicesを使用します。[マイクロサービスの概要](/help/assets/asset-microservices-overview.md)を参照してください。
   * [直接バイナリアクセスを使用した](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)アセットのアップロード。
   * 技術的な詳細については、[直接バイナリアップロードプロトコルとAPI](/help/assets/developer-reference-material-apis.md#upload-binary)を参照してください。
   * 基本的なCRUD操作に使用できるAPIメソッドの比較については、[APIとアセット操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)を参照してください。
* 以前のバージョンの に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。[!DNL Experience Manager]代わりに、アセットマイクロサービスは、デフォルトのアセット処理(レンディション、メタデータ抽出、インデックス作成用のテキスト抽出)のほとんどをカバーする、スケーラブルで、容易に利用できるサービスを提供します。
   * [アセットのマイクロサービスの設定と使用](/help/assets/asset-microservices-configure-and-use.md)を参照
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます.
* メタデータの書き戻しはサポートされていません。  [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html)の[メタデータの書き戻しを参照してください。
* Package Managerを使用してアップロードされるアセットは、[!DNL Assets]ユーザーインターフェイスの&#x200B;**[!UICONTROL アセットを再処理]**&#x200B;アクションを使用して手動で再処理する必要があります。
* [!DNL Assets] は、アップロードされたアセットのMIMEタイプを自動的に検出しません。拡張子のないデジタルアセットや、誤った拡張子のデジタルアセットは、必要に応じて処理されません。 例えば、そのようなアセットをアップロードする場合、何も発生しないか、アセットに誤った処理プロファイルが適用される場合があります。 ユーザーは、DAMに拡張子を付けずにバイナリファイルを保存できます。  [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)の[MIMEタイプ検出を参照してください。
* [!DNL Experience Manager] 」は、複合アセットのサブアセットを生成し [!DNL Cloud Service] ません。 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)の[サブアセットの作成を参照してください。
* [!DNL Assets] ホームページエクスペリエンスを使用できません。[[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html)を参照してください。
* 重複資産の検出は、[ [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)での動作とは異なる動作をします。
* 配置専用(FPO)レンディションの生成方法は、以前の[!DNL Experience Manager]バージョンとは異なります。 [ [!DNL Cloud Service]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html)として [!DNL Experience Manager] のFPOレンディションを参照してください。
* ZIPアーカイブをアップロードする場合、[!DNL Experience Manager]は[!DNL Cloud Service]としてアーカイブにバンドルされているアセットは抽出されません。  [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.htmln#extractzip)の[ZIP抽出を参照してください。

アセットマイクロサービスで生成された標準レンディションは、同じ命名規則を使用して、アセットリポジトリノードに下位互換性のある方法で保存されます。

## アセットマイクロサービスの開発とテスト {#asset-microservices}

アセットマイクロサービスは、クラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。アドビは、様々なアセットタイプや処理オプションを最適に処理するための Cloud Services を管理します。アセットマイクロサービスを利用すると、サードパーティ製のレンダリングツールやメソッド（ImageMagick など）が不要になり、システムの設定が簡単になると同時に、一般的なファイルタイプにそのまま使用できる機能が提供されます。以前のバージョンの Experience Manager で可能だったよりも幅広く、[様々なファイルタイプ](/help/assets/file-format-support.md)の形式を追加設定なしで処理できるようになりました。例えば、以前は ImageMagick などのサードパーティソリューションが必要だった PSD 形式と PSB 形式を、サムネール抽出できるようになりました。ImageMagick の複雑な設定は、[!UICONTROL 処理プロファイル]の設定に使用できません。ビデオの高度なFmpegトランスコードには[!DNL Dynamic Media]を、MP4ビデオの基本的なトランスコードには[処理プロファイルを使用します](/help/assets/manage-video-assets.md#transcode-video)。

Asset Microservicesは、Cloud Managerで管理されるお客様のプログラムーや環境ーで、自動的に[!DNL Experience Manager]にプロビジョニングされ、配線されるクラウドネイティブのサービスです。 [!DNL Experience Manager]を拡張またはカスタマイズするには、開発者は、クラウド環境で生成されたレンディションを含む既存のコンテンツまたはアセットを使用し、アセットの使用、表示、ダウンロードを使用したコードのテストと検証を行います。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証をおこなうには、コードの変更を[パイプライン](/help/implementing/cloud-manager/configure-pipeline.md)を使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## クラシック UI の削除 {#classic-ui}

クラシックUIは、[!DNL Experience Manager]では[!DNL Cloud Service]として使用できなくなりました。 タッチ対応UIのみを使用できます。

>[!MORELIKETHIS]
>
>[!DNL Experience Manager]の[!DNL Cloud Service]には次のリソースがあります。
>
>* [紹介](/help/overview/introduction.md)
>* [新機能と相違点](/help/overview/what-is-new-and-different.md)
>* [建築](/help/core-concepts/architecture.md)
>* [主要な変更点](/help/release-notes/aem-cloud-changes.md)
>* [主要な変更点 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [ビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=ja)

