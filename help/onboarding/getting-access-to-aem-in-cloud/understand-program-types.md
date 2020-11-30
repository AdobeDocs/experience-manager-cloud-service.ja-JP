---
title: プログラムとプログラムのタイプについて
description: プログラムとプログラムのタイプについて —Cloud Services
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---


# プログラムとプログラムの種類について {#understanding-programs}

Cloud Managerでは、最上部にテナントエンティティがあり、このエンティティ内に複数のプログラムを含めることができます。  各プログラムには、1つの実稼働環境と複数の非実稼働環境を含めることができます。

次の図に、Cloud Managerのエンティティの階層を示します。

![画像](assets/program-types1.png)

## プログラムタイプ {#program-types}

ユーザーは **Sandbox** または **** 正規プログラムを作成できます。

通常、 *Sandbox* は、トレーニング、デモ、有効化、POC、またはドキュメントの実施を目的として作成されます。 ライブトラフィックを運ぶことを目的としたものではなく、通常のプログラムでは行われないという制限を受けます。 サイトとアセットが含まれ、サンプルコード、開発環境、非実稼働パイプラインを含むGitブランチが自動入力されて配信されます。

正規プログラム *は* 、将来の適切なタイミングでライブトラフィックを有効にするために作成されます。