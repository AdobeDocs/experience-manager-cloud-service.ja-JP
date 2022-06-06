---
title: 'サンドボックスプログラムの概要 '
description: サンドボックスプログラムの概要と実稼動プログラムとの違いについて説明します。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: b74a0dbb1c9fdb74941f7b71bed9215853b63666
workflow-type: ht
source-wordcount: '413'
ht-degree: 100%

---


# サンドボックスプログラムの概要 {#sandbox-programs}

サンドボックスプログラムの概要と実稼動プログラムとの違いについて説明します。

## はじめに {#introduction}

サンドボックスプログラムは、通常、トレーニング、デモの実行、イネーブルメントまたは概念実証（POC）の目的にかなうように作成されるので、ライブトラフィックを実行するためのものではありません。

サンドボックスプログラムは、AEM Cloud Service で使用できる 2 種類のプログラムの 1 つで、もう 1 つは[実稼動プログラム](introduction-production-programs.md)です。プログラムタイプについて詳しくは、[プログラムとプログラムタイプについて](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)のドキュメントを参照してください。

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

### AEM の手動更新 {#updates}

AEM のアップデートは、サンドボックスプログラムに自動的にはプッシュされませんが、サンドボックスプログラム内の環境に手動で適用することができます。

* 手動更新は、対象環境に適切に設定されたパイプラインがある場合にのみ実行できます。
* 実稼働環境またはステージング環境のどちらか一方を手動で更新すると、もう一方が自動的に更新されます。実稼働とステージングの環境セットは、同じ AEM リリースに存在する必要があります。

詳しくは、[AEM バージョンのアップデート](/help/implementing/deploying/aem-version-updates.md)のドキュメントを参照してください。

環境を更新する方法については、[環境の更新](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)のドキュメントを参照してください。

### 休止と削除 {#hibernation}

サンドボックスプログラム内の環境は、8 時間操作が行われなかった場合、自動的に休止状態になります。休止状態になったら、手動で休止状態を解除できます。

サンドボックスプログラムは、連続休止モードになってから 6 か月が経過すると削除され、その後、再作成できます。

詳しくは、[サンドボックス環境の休止と休止解除](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md)を参照してください。
