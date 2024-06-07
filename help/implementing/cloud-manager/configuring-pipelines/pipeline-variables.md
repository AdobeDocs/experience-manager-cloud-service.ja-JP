---
title: パイプライン変数の設定
description: Cloud Manager でパイプライン変数を使用して、お使いのビルドに特有の設定変数を管理する方法について説明します。
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '571'
ht-degree: 100%

---

# パイプライン変数の設定 {#configuring-pipeline-variables}

お使いのビルドプロセスが、Git リポジトリに配置するのに適さない特定の設定変数に基づいている場合や、同じブランチを使用するパイプライン実行間で環境変数を変えることが必要になる場合があります。Cloud Manager では、これらのデータをパイプライン変数として管理できます。

## パイプライン変数 {#pipeline-variables}

Cloud Manager を使用すると、複数の方法でパイプライン変数を設定できます。

* [Cloud Manager UI の使用](#ui)
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

## Cloud Manager UI の使用 {#ui}

パイプライン変数は、Cloud Manager UI を使用して設定および管理できます。パイプライン変数を追加、編集、削除するには、パイプラインを編集する権限が必要です。

パイプラインが実行中の場合、変数管理はブロックされます。

### パイプライン変数の追加 {#add-ui}

1. [パイプラインを管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)する際、パイプライン変数を作成するパイプラインの省略記号ボタンをタップまたはクリックし、コンテキストメニューから「**変数を表示／編集**」を選択します。

   ![パイプライン変数の表示／編集](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. **変数設定**&#x200B;ウィンドウが開きます。テーブルの 1 行目に変数の詳細を入力し、「**追加**」をタップまたはクリックします。

   * **設定名**&#x200B;は変数の一意の ID で、[パイプライン変数の命名規則](#naming-conventions)に従う必要があります。
   * **値**&#x200B;は、変数が保持する値です。
   * **適用された手順**&#x200B;は、変数を適用するパイプライン内の手順です。これは必須です。
      * **ビルド**
      * **機能テスト**
      * **UI テスト**
   * **タイプ**&#x200B;は、変数がプレーンテキストか、シークレットとして暗号化されているかを定義します。

   ![変数の追加](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. がテーブルに追加されます。必要に応じて変数を追加し、「**保存**」をタップまたはクリックして、パイプラインに追加した変数を保存します。

### パイプライン変数の編集 {#edit-ui}

1. [パイプラインを管理](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)する際、パイプライン変数を作成するパイプラインの省略記号ボタンをタップまたはクリックし、コンテキストメニューから「**変数を表示／編集**」を選択します。

   ![パイプライン変数の表示／編集](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. **変数設定**&#x200B;ウィンドウが開きます。編集する変数の省略記号ボタンをタップまたはクリックし、「**編集**」を選択します。

   ![変数の編集](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. 必要に応じて変数の値を更新し、「**適用**」（行の最後のチェックマーク）をタップまたはクリックして変更を適用するか、「**破棄**」（戻る矢印）をタップまたはクリックして、変更を元に戻します。

   * 変数の値のみを編集できます。

   ![変数の編集](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. 「**保存**」をタップまたはクリックして、変数に対する変更をパイプラインに保存します。

変数を削除する場合は、**変数設定**&#x200B;ウィンドウのパイプライン変数の省略記号メニューから「**編集**」ではなく「**削除**」を選択します。

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
