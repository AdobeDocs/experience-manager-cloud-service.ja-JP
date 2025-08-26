---
title: Experience Hubについて
description: Adobe Experience Hubのページについて説明します。
landing-page-description: すべてのAdobe機能にアクセスするための一元的な出発点である、AEM Experience Hubについて説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: a1b0eed7-b74c-4e72-8399-c473bbda9245
source-git-commit: 8bd6fd4a7abcfbf37ba8aa458a9d2a035cca050e
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 5%

---

# Experience Hubについて {#aem-experience-hub}

Experience Hubは、Adobe Experience Manager内のコンテンツ、アセット、サイトを一元的に管理するための出発点となります。 Experience Hubはパーソナライズされたエクスペリエンスを提供するように設計されており、ユーザーの役割と目標に応じてAEM エコシステムをシームレスに移動できます。 ガイドとして機能し、目的を効率的に達成するのに役立つ重要なインサイトと推奨されるアクションを提供します。明確なペルソナ駆動型のレイアウトにより、Experience Hubは重要なツールにすばやくアクセスでき、すべてのAEM機能で合理化された効果的なエクスペリエンスをサポートします。

再考されたAEM Experience Hub Workspace のクイックツアー（2 分 19 秒）をご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3470957?learn=on)

<!--
Available as a private beta, Experience Hub offers an optimized experience focused on improving workflows, prioritizing goals, and delivering results. Opting in lets you influence Experience Hub's development by providing feedback that helps shape its future and enhances its value for the entire AEM community. -->

## Experience Hubアップを閉じる {#aem-experience-hub-about}

1. 開始するには、[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) をクリックしてホームページを開きます。

   ![Adobe Experience Cloudのホームページ ](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. **クイックアクセス** グループ化で、[**Experience Manager**](https://experience.adobe.com) をクリックします。
1. 初めてアクセスするときは、「**操作を教えてください** ページで目的のオプションをクリックして、Adobeがエクスペリエンスをカスタマイズできるようにします。

   この環境設定はいつでも変更できます。

   ![ 何をしたいか教えてくださいページ ](/help/implementing/cloud-manager/assets/experience-cloud-tellus.png)

Adobe Experience Managerページが更新され、ナビゲーションが強化され、インタラクティブウィジェットが追加されました。 以前のソリューションカードのコレクションでは、次のようなツールへのアクセスが可能でした。

* ユニバーサルエディター
* Cloud Manager
* Cloud Acceleration Manager
* ソフトウェア配布
* Extension Manager
* Brand Portal

>[!IMPORTANT]
>
>表示されるウィジェット、ツールおよびアーティファクトは、ユーザーのペルソナ、使用権限およびAEM デプロイメントタイプ（AEM as a Cloud ServiceまたはManaged Services 6.5/6.5 LTS）によって異なります。

これらのソリューションは、**ツール** または **サービス** の下のメインナビゲーションに移動しました。 さらに、新しいナビゲーション要素を使用すると、有効になっているソリューション（Assets、Sites、Forms、コンテンツフラグメント、ローンチなど）に固有の主なAdobe Experience Manager機能にすばやくアクセスできます。

![Experience Hub環境 ](/help/implementing/cloud-manager/assets/experience-hub-author-environments.png)

これらの機能は、アクセス権のあるプライマリ実稼動環境で使用できます。または、複数のAEM インスタンスにアクセスできる場合は、ターゲットにする特定の環境を選択できます。

![ 実稼動環境とステージ環境 ](/help/implementing/cloud-manager/assets/experience-hub-prod-stage.png)

Adobe Experience Managerの中央ハブとして機能するExperience Hub ページには、各ユーザーロールに合わせた追加のウィジェットとアクションが拡張されています。 ページは完全にカスタマイズ可能で、画面に最適なレイアウトを選択できます。 ウィジェットをフィルタリングして、選択したウィジェットのみをメインページに表示し、パーソナライズされたエクスペリエンスを提供できます。

![ カスタマイズされたExperience Hub](/help/implementing/cloud-manager/assets/experience-hub-custom.png)

ウィジェットは、ニーズや環境設定に合わせてサイズを変更したり、ページ上で再配置したりすることもできます。

![Experience Hub ウィジェット ](/help/implementing/cloud-manager/assets/experience-hub-widgets.png)

「**オーサリング環境**」セクションには、アクセス可能なすべてのAEM環境が表示され、使用可能なソリューションやページへの特定のショートカットも含まれています。また、リストの上部に表示する特定の環境をピン留めすることもできます。

次の図に示す **最近** セクションには、AEMで最近アクセスしたページが一覧表示されます。 テナントのライセンスに応じて、プログラム、パイプライン実行、Assets、ページエディター、フォームエディターなどがウィジェットに含まれる場合があります。

ページの左上隅付近にある **クイックショートカット** には、日々のタスクの開始に役立つ、設定可能なショートカットのリストが用意されています。 このリストはカスタマイズ可能で、各アクションは選択したAEM環境をターゲットにします。

![ オーサリング環境 ](/help/implementing/cloud-manager/assets/experience-hub-recents.png)

![Experience Hubのクイックショートカット ](/help/implementing/cloud-manager/assets/experience-hub-quick-shortcuts.png)

AEM Cloud Service またはManaged Servicesの実稼動環境が存在しない場合は、選択オプションがグレー表示され選択できません。

![Experience Hub実稼動環境がありません ](/help/implementing/cloud-manager/assets/experience-hub-no-prod-environs.png)

## AEMの AI アシスタント

[ 前提条件を完了している ](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access) お客様は、AEMの AI アシスタントを組織内のユーザーが利用できます。 [AEMの AI アシスタント ](/help/implementing/cloud-manager/ai-assistant-in-aem.md) を参照してください。
