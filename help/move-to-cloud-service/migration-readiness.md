---
title: 準備段階
description: 準備段階
exl-id: 987cb929-7871-4fec-8ef5-4d2f5f2f2186
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 97%

---

# 準備 {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="移行の計画"
>abstract="Cloud Service への移行プロセスを開始する前に、AEM as a Cloud Service に習熟し、AEM as a Cloud Service に対する主要な変更点を確認すると共に、置換または廃止された機能も確認する必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=ja" text="ベストプラクティスアナライザー"

Cloud Service への移行プロセスを開始する前に、AEM as a Cloud Service に習熟し、AEM as a Cloud Service に対する主要な変更点を確認すると共に、置換または廃止された機能も確認する必要があります。

## 主要な変更点 {#notable-changes}

AEM as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。

ただし、AEM as a Cloud Service とオンプレミスまたは Adobe Managed Services の AEM を比較すると、両者には数々の違いがあります。

重要な違いについては、[Adobe Experience Manager（AEM）as a Cloud Service の主要な変更点](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=ja)を参照してください。

## 非推奨（廃止予定）の機能 {#deprecated-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

Adobe Experience Manager as a Cloud Service で廃止される特長や機能については、[廃止される機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features)を参照してください。

## 計画段階について {#introduction}

計画段階で必要になる主なステップを次の図に示します。

![画像](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### Cloud Service への対応準備状況の評価 {#access-cloud-readiness}

計画段階の最初のステップは、既存の AEM バージョンから Cloud Service に移行する準備ができているかどうかを評価し、AEM as a Cloud Service に対応するためにリファクタリングが必要な領域を決定することです。

移行プロセスで予想される作業レベルを決定するには、主要な変更点および廃止される機能に照らした現在の AEM ソースコードの包括的な評価を行う必要があります。

現在の AEM バージョンでベストプラクティスアナライザーを実行すると、評価ステップを高速化できます。詳しくは、[ベストプラクティスアナライザー](/help/move-to-cloud-service/best-practices-analyzer/overview-best-practices-analyzer.md)を参照してください。

>[!NOTE]
>既に Cloud Manager と Cloud Service 環境にアクセスできる場合は、現在のコードを Cloud Manager のコード品質パイプラインで実行して、Cloud Service に対応するために必要なコード変更を評価することをお勧めします。

### リソース計画のレビュー {#review-resource-planning}

Cloud Service への移行に必要な作業レベルを推定したら、リソースを特定し、チームを作成し、移行プロセスに関連する役割と責務を綿密に計画する必要があります。

### KPI の設定 {#establish-kpis}

主要業績評価指標（KPI）をまだ設定していない場合は、最も重要なことにチームが専念できるように、Adobe Experience Manager（AEM）の実装に関する KPI を設定することをお勧めします。

ビジネス目標に合った適切な KPI を選択する方法については、[KPI の策定に関するドキュメント](https://guided.adobe.com/welcome/aem/part6.html)を参照してください。
