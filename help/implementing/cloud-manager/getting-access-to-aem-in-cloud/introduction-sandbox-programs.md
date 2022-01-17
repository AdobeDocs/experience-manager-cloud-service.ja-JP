---
title: 'サンドボックスプログラムの概要 '
description: サンドボックスプログラムの概要
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 1892900ea3f365e1b5f7d31ffae64d45256d2a3a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 100%

---

# サンドボックスプログラムの概要 {#sandbox-programs}

## はじめに {#introduction}

サンドボックスプログラムは、AEM Cloud Service で使用できる 2 種類のプログラムの 1 つで、もう 1 つは実稼動プログラムです。

サンドボックスは、通常、トレーニング、デモの実行、使用可能性、またはコンセプトの配達確認（POC）といった目的を満たすために作成され、ライブトラフィックを運ぶためのものではありません。サンドボックスは、[AEM as a Cloud Service のコミットメント](https://www.adobe.com/jp/legal/service-commitments.html)には従いません。

サンドボックスで作成された環境は、自動スケール用に設定されません。したがって、パフォーマンスや負荷テストには適しません。

サンドボックスプログラムには [!DNL Sites] と [!DNL Assets] が含まれ、Git リポジトリー、開発環境、実稼働以外のパイプラインが自動入力されます。Git リポジトリーには、AEM プロジェクトのアーキタイプに基づくサンプルプロジェクトが入力されます。

>[!IMPORTANT]
>サンドボックスプログラムには、開発環境が 1 つだけあります。

>[!NOTE]
>カスタムドメインと IP 許可リストは、サンドボックスプログラムでは使用できません。

プログラムタイプの詳細については、[プログラムとプログラムタイプについて](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html?lang=ja)を参照してください。

### サンドボックスプログラムの属性 {#attributes-sandbox}

サンドボックスプログラムには次の属性があります。

1. **プログラムの作成：**&#x200B;サンドボックスプログラムの作成には、次の自動機能が含まれます。
   * サンプルコードとコンテンツを使用したプロジェクトのセットアップ
   * 開発環境の作成
   * 開発環境にデプロイされる、実稼働以外のパイプラインの作成（開発環境へのメインブランチのデプロイ）

1. **ソリューション：**&#x200B;サンドボックスプログラムには、AEM [!DNL Sites] および [!DNL Assets] が含まれます。

1. **AEM アップデート：** AEM のアップデートは、サンドボックスプログラム内の環境に手動で適用します。自動でプッシュされることはありません。詳しくは、[サンドボックス環境への AEM アップデートの適用](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox)を参照してください。

1. **休止状態：**&#x200B;サンドボックスプログラム内の環境は、特定の期間、アクティビティが検出されなかった場合、自動的に休止状態になります。サンドボックスは、8 時間操作が実行されなかった後に休止ノードになり、その後、休止解除できます。休止状態の環境は、手動で休止を解除できます。詳しくは、[サンドボックス環境の休止と休止解除](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md)を参照してください。

1. **削除**：サンドボックスは、連続休止モードになってから 6 か月が経過すると削除され、その後再作成できます。
