---
title: Maven プロジェクトのバージョン処理
description: AEM as a Cloud Service のステージングデプロイメントと実稼動デプロイメントの場合は、Cloud Manager が一意の増分バージョンを生成します。
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 100%

---


# Maven プロジェクトのバージョン処理 {#maven-project-version-handling}

AEM as a Cloud Service のステージングデプロイメントと実稼動デプロイメントの場合は、Cloud Manager が一意の増分バージョンを生成します。

このバージョンは、[パイプライン実行の詳細ページ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)やアクティビティページに表示されます。ビルドを実行すると、Maven プロジェクトが更新されてこのバージョンを使用するようになります。また、タグが Git リポジトリーに作成され、そのバージョンを名前として使用します。

元のプロジェクトバージョンが特定の条件を満たす場合、更新された Maven プロジェクトバージョンは、元のプロジェクトバージョンと Cloud Manager で生成されたバージョンの両方を結合します。ただし、タグは常に生成されたバージョンを使用します。このマージが行われるためには、元のプロジェクトバージョンを 3 つのバージョンセグメントで構成する必要があり（例：`1.0` や `1` ではなく `1.0.0` や `1.2.3`）、元のバージョンの末尾に `-SNAPSHOT` を付けてはいけません。

>[!IMPORTANT]
>
>この元のプロジェクトバージョン値は、Git リポジトリブランチの最上位 `pom.xml` ファイルの `<version>` 要素で静的に設定する必要があります。

元のバージョンがこれらの条件を満たしている場合は、生成されたバージョンが新しいバージョンセグメントとして元のバージョンに追加されます。また、生成されたバージョンも、適切な並べ替えとバージョン処理を適用して若干変更されます。例えば、`2019.926.121356.0000020490` の生成されたバージョンの場合は、次の結果になると仮定します。

| バージョン | `pom.xml` 内のバージョン | コメント |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | 正しく作成されたオリジナルバージョン |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | スナップショットバージョン、上書き済み |
| `1` | `2019.926.121356.0000020490` | 不完全なバージョン、上書き済み |

>[!NOTE]
>
>Cloud Manager で初期化されたバージョンに元のバージョンが組み込まれたかどうかにかかわらず、元のバージョンは `cloudManagerOriginalVersion` という名前の Maven プロパティとして使用できます。
