---
title: 'Sandboxプログラムの概要 '
description: 'Sandboxプログラムの概要 '
translation-type: tm+mt
source-git-commit: d98e3ba930690627bfbe9b90ce5cb93328c30503
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 79%

---


# Sandboxプログラムの紹介{#sandbox-programs}

## 概要 {#introduction}

Sandboxプログラムは、AEMCloud Serviceで使用できる2種類のプログラムの1つで、もう1つは実稼働プログラムです。

サンドボックスは、通常、トレーニング、デモの実行、使用可能性、またはコンセプトの配達確認（POC）といった目的を満たすために作成され、ライブトラフィックを運ぶためのものではありません。サンドボックスは、[AEM as a Cloud Service のコミットメント](https://www.adobe.com/jp/legal/service-commitments.html)には従いません。

サンドボックスで作成された環境は、自動スケール用に設定されません。したがって、これらの環境は、パフォーマンスや読み込みテストには適していません。

サンドボックスプログラムには Sites と Assets が含まれ、Git リポジトリー、開発環境、実稼働以外のパイプラインが自動入力されます。Git リポジトリーには、AEM プロジェクトのアーキタイプに基づくサンプルプロジェクトが入力されます。

プログラムタイプの詳細については、[プログラムとプログラムタイプについて](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)を参照してください。

### サンドボックスプログラムの属性 {#attributes-sandbox}

サンドボックスプログラムには次の属性があります。

1. **プログラムの作成：**&#x200B;サンドボックスプログラムの作成には、次の自動機能が含まれます。
   * サンプルコードとコンテンツを使用したプロジェクトのセットアップ
   * 開発環境の作成
   * 開発環境にデプロイされる、実稼働以外のパイプラインの作成（開発環境へのメインブランチのデプロイ）

1. **ソリューション：**&#x200B;サンドボックスプログラムには、AEM Sites と Assets が含まれます。

1. **AEM アップデート：** AEM のアップデートは、サンドボックスプログラム内の環境に手動で適用します。自動でプッシュされることはありません。詳しくは、[Sandbox環境へのAEMの更新](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox)を参照してください。

1. **休止状態：**&#x200B;サンドボックスプログラム内の環境は、特定の期間、アクティビティが検出されなかった場合、自動的に休止状態になります。休止状態の環境は、手動で休止を解除できます。詳しくは、[サンドボックス環境の休止と休止解除](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md)を参照してください。