---
title: Cloud Manager のパイプライン変数
description: Cloud Manager でパイプライン変数を使用して、お使いのビルドに特有の設定変数を管理する方法について説明します。
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ea85deb74f759f8e74d314df0ba081ea23cb5aab
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 96%

---

# Cloud Manager のパイプライン変数 {#configuring-pipeline-variables}

ビルドプロセスが、Git リポジトリに保存すべきではない特定の設定変数に依存している可能性があります。または、同じブランチでのパイプライン実行間で調整が必要になる場合があります。Cloud Manager では、これらの設定をパイプライン変数として管理できます。

## パイプライン変数について {#pipeline-variables}

Cloud Manager を使用すると、複数の方法でパイプライン変数を設定できます。

* [Cloud Manager ユーザーインターフェイスの使用](#ui)
* [Cloud Manager CLI の使用](#cli)
* [Cloud Manager API の使用](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

変数は、プレーンテキストとして保存することも、保存時に暗号化することもできます。どちらの場合も、変数はビルド環境内で環境変数として使用可能になり、変数は `pom.xml` ファイル内または他のビルドスクリプト内から参照できます。

## Cloud Manager を使用したパイプライン変数の追加 {#ui}

パイプライン変数は、Cloud Manager ユーザーインターフェイスを使用して設定および管理できます。これは、特に様々なステップで異なる設定が必要な場合に、パイプライン管理を効率化するのに役立ちます。

パイプライン変数を追加、編集、削除するには、パイプラインを編集する権限が必要です。

パイプラインが実行中の場合、変数管理はブロックされます。

**Cloud Manager を使用してパイプライン変数を追加するには：**

1. [パイプラインを管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)する際、パイプライン変数を作成するパイプラインの![省略記号 - その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックします。

1. ドロップダウンメニューから、「**変数を表示／編集**」をクリックします。

   ![パイプライン変数を表示／編集](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. **変数設定**&#x200B;ダイアログボックスで、テーブルの最初の行に詳細を入力します。

   | フィールド | 説明 |
   | --- | --- |
   | 名前 | 設定変数の一意の名前です。パイプラインで使用される特定の変数を識別します。次の命名規則に従う必要があります。<ul><li>変数には、英数字とアンダースコア（`_`）のみ使用できます。</li><li>名前はすべて大文字にします。</li><li>変数の数はパイプラインあたり最大 200 個までです。</li><li>名前は 100 文字以下にする必要があります。</li><li>`string` 変数の値はそれぞれ、2048 文字未満にする必要があります。</li><li>`secretString` 変数型の値はそれぞれ、500 文字以下にする必要があります。</li></ul> |
   | 値 | 変数が保持する値です。 |
   | 適用されたステップ | 必須。変数が適用されるパイプラインのステップ：<ul><li>**ビルド** - 変数は、ビルドプロセス中に適用されます。</li><li>**機能テスト** - 変数は、機能テストステップで使用されます。</li><li>**UI テスト** - 変数は、UI テスト段階で使用されます。</li>&lt;li&lt;**Deploy** – 変数は、デプロイステップで使用されます。 例えば、Edge Delivery Services パイプラインには、この変数を使用します。</li></ul> |
   | タイプ | 変数がプレーンテキストか、シークレットとして暗号化されているかを選択します。 |

   ![変数の追加](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. 「**追加**」をクリックします。

   必要に応じて、変数を追加します。

1. 「**保存**」をクリックします。

## パイプライン変数の編集 {#edit-ui}

1. [パイプラインを管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)する際、パイプライン変数を編集するパイプラインの ![省略記号 - その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**変数を表示／編集**」をクリックします。

   ![パイプライン変数の表示／編集](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. **変数設定**&#x200B;ダイアログボックスで、変更する変数の ![省略記号 - その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**編集**」をクリックします。

   ![変数の編集](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. 必要に応じて、変数の値を更新します。

   変更できるのは変数の値のみです。

1. 次のいずれかの操作を行います。

   * ![適用 – チェックマークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) をクリックして、変更を適用します。
   * ![取り消しアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg)をクリックして、変更を元に戻します。

1. 「**保存**」をクリックします。


## パイプライン変数の削除 {#delete-ui}

1. [パイプラインを管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)する際、パイプライン変数を削除するパイプラインの ![省略記号 - その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**変数を表示／編集**」をクリックします。

   ![パイプライン変数の表示／編集](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. **変数設定**&#x200B;ダイアログボックスで、削除する変数の ![省略記号 - その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、「**削除**」をクリックします。

## Cloud Manager CLI を使用したパイプライン変数の設定 {#cli}

CLI（コマンドラインインターフェイス）のこのコマンドで、変数を設定します。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

このコマンドは、変数を一覧表示します。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Maven `pom.xml` ファイル内で使用する場合は、多くの場合、次のような構文を使用して、これらの変数を Maven プロパティにリンクすると便利です。

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```
