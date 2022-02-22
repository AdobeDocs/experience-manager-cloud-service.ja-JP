---
title: 'サンドボックスプログラムの概要 '
description: サンドボックスプログラムと実稼動プログラムの違いについて説明します。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: b74a0dbb1c9fdb74941f7b71bed9215853b63666
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 14%

---


# サンドボックスプログラムの概要 {#sandbox-programs}

サンドボックスプログラムと実稼動プログラムの違いについて説明します。

## はじめに {#introduction}

サンドボックスプログラムは、通常、トレーニング、デモの実行、イネーブルメント、またはコンセプトの配達確認 (POC) の目的を満たすために作成されるので、ライブトラフィックを運ぶ目的ではありません。

サンドボックスプログラムは、AEM Cloud Serviceで使用可能な 2 種類のプログラムの 1 つで、もう 1 つは [実稼働プログラム。](introduction-production-programs.md) ドキュメントを参照してください [プログラムとプログラムの種類について](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) を参照してください。

## 自動作成 {#auto-creation}

サンドボックスプログラムは自動作成機能を備えています。 新しいサンドボックスプログラムを作成する場合、Cloud Manager は自動的に次の操作をおこないます。

* AEM SitesとAEM Assetsをプログラムのソリューションとして追加します。
* 次に基づくサンプルプロジェクトを使用してプロジェクト Git リポジトリを設定します。 [AEMプロジェクトアーキタイプ。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)
* 開発環境を作成します。
* 開発環境にデプロイする非実稼動パイプラインを作成します。

サンドボックスプログラムには 1 つの開発環境のみが含まれます。

## 制限事項 {#limitations}

ライブトラフィック向けのものではないので、サンドボックスプログラムは、使用に一定の制限と条件を持ち、実稼動プログラムと区別します。

### ライブトラフィックなし {#live-traffic}

サンドボックスプログラムは、ライブトラフィックを運ぶためのものではないので、対象となりません [AEMas a Cloud Serviceのコミットメント](https://www.adobe.com/jp/legal/service-commitments.html)

### 自動スケーリングなし {#auto-scaling}

サンドボックスプログラムで作成された環境は、自動スケーリング用に設定されていません。 したがって、パフォーマンスや負荷テストには適しません。

### カスタムドメインまたは IP許可リストがありません {#ip-allow}

カスタムドメインと IP許可リストは、サンドボックスプログラムでは使用できません。

### 手動更新のAEM {#updates}

AEMの更新は、サンドボックスプログラムに自動的にプッシュされるのではありませんが、サンドボックスプログラム内の環境に手動で適用することができます。

* 手動更新は、対象環境に適切に設定されたパイプラインがある場合にのみ実行できます。
* 実稼動環境またはステージング環境を手動で更新すると、もう一方が自動的に更新されます。 実稼働とステージングの環境セットは、同じ AEM リリースに存在する必要があります。

ドキュメントを参照してください [AEMバージョンの更新](/help/implementing/deploying/aem-version-updates.md) を参照してください。

ドキュメントを参照してください [環境の更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) 環境を更新する方法を学ぶには、以下を参照してください。

### 休止と削除 {#hibernation}

サンドボックスプログラム内の環境は、8 時間操作が実行されなかった場合、自動的に休止状態になります。 休止状態にしたら、手動で休止状態を解除できます。

サンドボックスプログラムは、6 ヶ月間連続休止モードになった後に削除され、その後、再作成できます。

詳しくは、 [サンドボックス環境の休止と休止解除](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) を参照してください。
