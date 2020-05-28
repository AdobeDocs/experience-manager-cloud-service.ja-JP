---
title: 計画段階
description: 計画段階
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 10%

---


# 計画 {#planning-phase}

クラウドサービスへのトランジションの遍歴を始める前に、クラウドサービスとしてのAEMの知識を深め、AEMに対して行われた注目すべき変更を確認し、置き換えられた機能や非推奨の機能を確認する必要があります。

## 主要な変更点 {#notable-changes}

クラウドサービスとしてのAEMは、AEMプロジェクトを管理するための多くの新機能と可能性を提供します。

ただし、AEMオンプレミスとAdobe Managed Servicesの違いは、AEMをクラウドサービスとして使用する場合とでは多くの違いがあります。

重要な違いについては、「AEMクラウドサービスに関する [重要な変更点](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/release-notes/aem-cloud-changes.html) 」を参照してください。

## 廃止される機能 {#deprecated-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

クラウドサービスとしてExperience Managerで非推奨としてマークされた機能について詳しくは、 [非推奨の機能](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) （英語）を参照してください。

## 計画段階について {#introduction}

次の図は、計画段階で必要となる主な手順を示しています。

![画像](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### クラウドサービスの準備状況の評価 {#access-cloud-readiness}

計画段階の最初の手順は、既存のAEMバージョンからクラウドサービスに移行する準備ができているかを評価し、クラウドサービスとしてのAEMとの互換性を維持するためにリファクタリングが必要な領域を決定することです。

トランジションの遍歴で期待される作業のレベルを決定するには、現在のAEMソースコードを注目すべき変更点および非推奨の機能に対して包括的な評価を行う必要があります。

>[!NOTE]
>既にCloud Managerとクラウドサービスの環境にアクセスできる場合は、現在のコードをCloud Managerのコード品質パイプラインで実行し、クラウドサービスと互換性があるように必要なコード変更を評価することをお勧めします。

### 生産資源計画の検討 {#review-resource-planning}

クラウドサービスへの移行に必要な作業レベルを見積もったら、リソースを特定し、チームを作成し、トランジションプロセスのロールと責任をマッピングする必要があります。

### KPIの設定 {#establish-kpis}

主要業績評価指標(KPI)を以前に確立していない場合は、チームが最も重要な点に焦点を当てるのに役立つように、Adobe Experience Manager(AEM)の実装に関するKPIを確立することをお勧めします。

ビジネス目標に合った適切なKPIを選択する方法については、 [「KPIの](https://guided.adobe.com/welcome/aem/part6.html) 開発」を参照してください。

