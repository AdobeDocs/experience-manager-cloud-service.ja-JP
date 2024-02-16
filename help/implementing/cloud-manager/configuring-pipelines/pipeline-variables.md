---
title: パイプライン変数の設定
description: Cloud Manager でパイプライン変数を使用して、ビルドの特定の設定変数を管理する方法について説明します。
source-git-commit: 7b98883d16893534387fa10665f5fa432d74470f
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 23%

---


# パイプライン変数の設定 {#configuring-pipeline-variables}

ビルドプロセスは、Git リポジトリに配置するのに適さない特定の設定変数によって異なる場合や、同じブランチを使用するパイプライン実行間で変更する必要が生じる場合があります。 Cloud Manager では、これらのデータをパイプライン変数として管理できます。

## パイプライン変数 {#pipeline-variables}

Cloud Manager を使用するには、複数の方法でパイプライン変数を設定できます。

* [Cloud Manager UI を使用](#ui)
* [Cloud Manager CLI の使用](#cli)
* [Cloud Manager API の使用](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

変数は、プレーンテキストとして保存することも、保存時に暗号化することもできます。どちらの場合も、変数はビルド環境内で環境変数として使用可能になり、変数は `pom.xml` ファイル内または他のビルドスクリプト内から参照できます。

### パイプライン変数の命名規則 {#naming-conventions}

変数名は、次の規則に従う必要があります。

* 変数には、英数字とアンダースコア（`_`）のみ使用できます。
* 名前はすべて大文字にします。
* 変数の数はパイプラインあたり最大 200 個までです。
* 名前は 100 文字以下にする必要があります。
* `string` 変数の値はそれぞれ、2048 文字未満にする必要があります。
* `secretString` 変数型の値はそれぞれ、500 文字以下にする必要があります。

## Cloud Manager UI を使用 {#ui}

パイプライン変数は、Cloud Manager UI を使用して設定および管理できます。 パイプライン変数を追加、編集および削除するには、パイプラインを編集する権限が必要です。

パイプラインが実行中の場合、変数管理はブロックされます。

### パイプライン変数の追加 {#add-ui}

1. 条件 [パイプラインの管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) パイプライン変数を作成するパイプラインの省略記号ボタンをタップまたはクリックし、「 」を選択します。 **変数を表示/編集** を選択します。

   ![パイプライン変数を表示/編集](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. The **変数設定** ウィンドウが開きます。 テーブルの 1 行目に変数の詳細を入力し、をタップまたはクリックします。 **追加**.

   * **設定名** は変数の一意の識別子で、先頭に配置する必要があります [パイプライン変数の命名規則。](#naming-conventions)
   * **値** は、変数に格納される値です。
   * **適用されたステップ** は、変数を適用するパイプライン内のステップです。 必須です。
      * **ビルド**
      * **機能テスト**
      * **UI テスト**
   * **タイプ** 変数がプレーンテキストか、シークレットとして暗号化かを定義します。

   ![変数を追加](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. がテーブルに追加されます。 必要に応じて変数を追加し、をタップまたはクリックします。 **保存** をクリックして、パイプラインに追加した変数を保存します。

### パイプライン変数の編集 {#edit-ui}

1. 条件 [パイプラインの管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) パイプライン変数を作成するパイプラインの省略記号ボタンをタップまたはクリックし、「 」を選択します。 **変数を表示/編集** を選択します。

   ![パイプライン変数を表示/編集](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. The **変数設定** ウィンドウが開きます。 編集する変数の省略記号ボタンをタップまたはクリックし、「 」を選択します。 **編集**.

   ![変数の編集](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. 必要に応じて変数の値を更新し、をタップまたはクリックします **適用** （行の最後のチェックマーク）変更を適用するか、 **破棄** （戻る矢印）を使用して、変更を元に戻します。

   * 変数の値のみを編集できます。

   ![変数の編集](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. タップまたはクリック **保存** をクリックして、変数に対する変更をパイプラインに保存します。

変数を削除する場合は、「 **削除** の代わりに **編集** を選択します。 **変数設定** ウィンドウ

## Cloud Manager CLI の使用 {#cli}

この CLI コマンドは変数を設定します。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

このコマンドは、変数を一覧表示します。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Maven `pom.xml` ファイル内で使用する場合は、通常、次のような構文を使用して、これらの変数を Maven プロパティにマッピングすると便利です。

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
