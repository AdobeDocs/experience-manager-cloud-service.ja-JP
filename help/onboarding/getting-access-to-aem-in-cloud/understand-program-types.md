---
title: プログラムとプログラムのタイプについて
description: プログラムとプログラムのタイプについて —Cloud Services
translation-type: tm+mt
source-git-commit: e1d805e1e5b5850ecf3154cd69a3955c4dbe1e65
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 3%

---


# プログラムとプログラムの種類について {#understanding-programs}

Cloud Managerでは、最上部にテナントエンティティがあり、このエンティティ内に複数のプログラムを含めることができます。 各プログラムには、1つの実稼働環境と複数の非実稼働環境を含めることができます。

次の図に、Cloud Managerのエンティティの階層を示します。

![画像](assets/program-types1.png)

## プログラムタイプ{#program-types}

ユーザーは、**Sandbox**&#x200B;または&#x200B;**Production**&#x200B;プログラムを作成できます。

* *本番プログラム*が作成され、将来の適切なタイミングでライブトラフィックを利用できるようになります。
詳しくは、[実稼働プログラムの紹介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。


* *Sandboxプログラム*は、通常、トレーニング、デモ、有効化、POC、ドキュメントの実行の目的で作成されます。 ライブトラフィックを運ぶことを目的としたものではなく、通常のプログラムでは行われないという制限を受けます。 サイトとアセットが含まれ、サンプルコード、開発環境、非実稼働パイプラインを含むGitブランチが自動入力されて配信されます。
詳しくは、[Sandboxプログラムの紹介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)を参照してください。

