---
title: Adobe Experience Manager Assets as a Cloud Service の主な変更点
description: Adobe Experience Manager 6.5 と比較した、AEM Cloud Service の Adobe Experience Manager Assets の主な変更点.
translation-type: tm+mt
source-git-commit: 37ff6912837ba78c90526e8f8322b9002e9a4304
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 100%

---


# Experience Manager Assets as a Cloud Service の主な変更点 {#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。ただし、Adobe Experience Manager as a Cloud Service と、On-Premise や Adobe Managed Services の Adobe Experience Manager Assets を比較すると、両者には多くの違いがあります。このドキュメントでは、Assets 機能の重要な違いについて説明します。その他の変更点については、[Experience Manager as a Cloud Service の主な変更点](/help/release-notes/aem-cloud-changes.md)を参照してください。

Adobe Experience Manager 6.5 との主な違いは次の点です。

* [アセットの取り込みとアップロード](#asset-ingestion)。
* [クラウド処理用のアセットマイクロサービス](#asset-microservices)。
* [クラシック UI の削除](#classic-ui).

## アセットの取り込みとアップロード {#asset-ingestion}

アセットのアップロードが効率化のために最適化され、アセット取り込みの規模をより適切に拡大／縮小できるようになったほか、アップロードが高速化されました。製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されました。ただし、これによって、一部の既存カスタマイズが影響を受ける可能性があります。

* Adobe Experience Manager では、アップロードとダウンロードに直接バイナリアクセスの原則を使用し、アセットの処理にアセットマイクロサービスを使用します。[アセットの取り込みの概要](/help/assets/asset-microservices-overview.md)を参照してください。
   * [直接バイナリアクセスを使用した](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)アセットのアップロード。
   * 技術的な詳細については、[直接バイナリアップロードのプロトコルと API](/help/assets/developer-reference-material-apis.md#overview-binary-upload) を参照してください.
* 以前のバージョンの AEM に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。代わりに、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどに対応できる、拡張性と可用性の高いサービスをアセットマイクロサービスが提供します。
   * [アセットマイクロサービスの設定および使用方法](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。
* パッケージマネージャーで取り込まれたアセットについては、Assets インターフェイスの「**[!UICONTROL アセットを再処理]**」アクションを使用して、手動で再処理する必要があります。

アセットマイクロサービスで生成された標準レンディションは、後方互換性のある方法でアセットリポジトリノードに保存されます（同じ命名規則が使用されます）。

## アセットマイクロサービスの開発とテスト {#asset-microservices}

アセットマイクロサービスは、クラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。アドビは、様々なアセットタイプや処理オプションを最適に処理するための Cloud Services を管理します。アセットマイクロサービスを利用すると、サードパーティ製のレンダリングツールやメソッド（ImageMagick など）が不要になり、システムの設定が簡単になると同時に、一般的なファイルタイプにそのまま使用できる機能が提供されます。以前のバージョンの Experience Manager で可能だったよりも幅広く、[様々なファイルタイプ](/help/assets/file-format-support.md)の形式を追加設定なしで処理できるようになりました。例えば、以前は ImageMagick などのサードパーティソリューションが必要だった PSD 形式と PSB 形式を、サムネール抽出できるようになりました。ImageMagick の複雑な設定は、[!UICONTROL 処理プロファイル]の設定に使用できません。また、ビデオの Fmpeg トランスコードには [!DNL Dynamic Media] を使用します。

アセットマイクロサービスは、Cloud Manager で管理されるユーザープログラムと環境にある Adobe Experience Manager に自動的にプロビジョニングして接続される、クラウドネイティブなサービスです。Adobe Experience Manager の拡張やカスタマイズをおこなう場合、開発者は、既存のコンテンツまたはクラウド環境で生成されたレンディションを含んだアセットを使用して、アセットの使用、表示、ダウンロードをおこなうコードをテストし検証できます。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証をおこなうには、コードの変更を[パイプライン](/help/implementing/cloud-manager/configure-pipeline.md)を使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## クラシック UI の削除 {#classic-ui}

Adobe Experience Manager as a Cloud Service ではクラシック UI が使用できなくなりました。標準のインターフェイスは、タッチ対応 UI です。
