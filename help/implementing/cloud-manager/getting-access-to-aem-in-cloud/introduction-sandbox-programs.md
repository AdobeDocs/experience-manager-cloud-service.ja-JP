---
title: サンドボックスプログラムの概要
description: サンドボックスプログラムの概要と実稼動プログラムとの違いについて説明します。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 100%

---


# サンドボックスプログラムの概要 {#sandbox-programs}

サンドボックスプログラムの概要と実稼動プログラムとの違いについて説明します。

## はじめに {#introduction}

サンドボックスプログラムは、通常、トレーニング、デモの実行、イネーブルメントまたは概念実証（POC）の目的にかなうように作成されるので、ライブトラフィックを実行するためのものではありません。

サンドボックスプログラムは、AEM Cloud Service で使用できる 2 種類のプログラムの 1 つで、もう 1 つは[実稼動プログラム](introduction-production-programs.md) プログラムタイプについて詳しくは、[プログラムとプログラムタイプについて](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)を参照してください。

## 自動作成 {#auto-creation}

サンドボックスプログラムは自動作成機能を備えています。新しいサンドボックスプログラムを作成するたびに、Cloud Manager は自動的に以下を行います。

* AEM Sites と AEM Assets をソリューションとしてプログラムに追加します。
* プロジェクト Git リポジトリと、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)に基づくサンプルプロジェクトをセットアップします。
* 開発環境を作成します。
* その開発環境へのデプロイメントを行う実稼動以外のパイプラインを作成します。

サンドボックスプログラムには、開発環境が 1 つだけあります。

## 制限事項と条件 {#limitations}

サンドボックスプログラムはライブトラフィック向けのものではないので、使用に関して一定の制限事項と条件があります。これが、実稼動プログラムとの違いです。

### ライブトラフィックなし {#live-traffic}

サンドボックスプログラムは、ライブトラフィックを実行するためのものではないので、[AEM as a Cloud Service のコミットメント](https://www.adobe.com/jp/legal/service-commitments.html)には従いません。

### 自動スケーリングなし {#auto-scaling}

サンドボックスプログラムに作成された環境は、自動スケール用に設定されません。したがって、パフォーマンスや負荷テストには適しません。

### カスタムドメインまたは IP許可リストなし {#ip-allow}

カスタムドメインと IP 許可リストは、サンドボックスプログラムでは使用できません。

### 高度なネットワークなし {#advanced-networking}

[高度なネットワーク機能](/help/security/configuring-advanced-networking.md)（例えば、VPN のセルフサービスプロビジョニング、非標準ポート、専用のエグレス IP アドレスなど）は、サンドボックスプログラムでは使用できません。

### AEM の手動更新 {#updates}

AEM のアップデートは、サンドボックスプログラムに自動的にはプッシュされませんが、サンドボックスプログラム内の環境に手動で適用することができます。

* 手動更新は、対象環境に適切に設定されたパイプラインがある場合にのみ実行できます。
* 実稼働環境またはステージング環境のどちらか一方を手動で更新すると、もう一方が自動的に更新されます。実稼働とステージングの環境セットは、同じ AEM リリースに存在する必要があります。

詳しくは、[AEM バージョンのアップデート](/help/implementing/deploying/aem-version-updates.md)を参照してください。

環境を更新する方法については、[環境の更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)を参照してください。

### 休止と削除 {#hibernation}

サンドボックスプログラム内の環境は、非アクティブな状態が 8 時間を超えると、自動的に休止状態になります。サンドボックス環境は、6 か月連続の休止状態が続いた後に削除されます。

環境の休止状態を解除する方法とサンドボックスの自動削除について詳しくは、[サンドボックス環境の休止と休止解除](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md)を参照してください。

### テクニカルサポートなし {#no-support}

サンドボックスプログラムは通常、トレーニング、デモの実行、有効化または概念実証（POC）の目的で作成されるので、サンドボックスプログラムで発生する問題に対してはテクニカルサポートを利用できません。

サンドボックスプログラムの作成と管理で問題が発生する場合でも、これはテクニカルサポートの範囲内です。
