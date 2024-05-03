---
title: フォームデータモデル（FDM）の作成方法
description: フォームデータモデル (FDM) を作成し、アダプティブフォームまたはAEMワークフローを使用して、データソースにデータを送信または取得する方法を説明します。
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 63%

---

# フォームデータモデル（FDM）の作成 {#create-form-data-model}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


![データ統合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] のデータ統合機能には、フォームデータモデルを作成して使用するための直感的なユーザーインターフェイスが用意されています。フォームデータモデル（FDM）は、データの交換にデータソースを使用しますが、データソースを使用せずにフォームデータモデル（FDM）を作成することもできます。 フォームデータモデルを作成する方法には、以下の 2 つがあります。データソースが既に設定されているかどうかに応じて、いずれかの方法を選択してください。

* **事前設定済みのデータソースの使用**：の説明に従ってデータソースが設定されている場合 [データソースの設定](configure-data-sources.md)を参照します。これらは、フォームデータモデル（FDM）の作成時に選択できます。 選択したデータソースのすべてのデータモデルオブジェクト、プロパティ、サービスを、フォームデータモデル（FDM）内で使用できるようになります。

* **データソースなし**：フォームデータモデル（FDM）のデータソースを設定していない場合でも、データソースを使用せずに作成できます。 フォームデータモデル（FDM）を使用して、アダプティブFormsを作成できます <!--and interactive communication--> そして、サンプルデータを使用してテストします。 データソースが使用可能な状態になっている場合は、フォームデータモデル（FDM）をデータソースに連結すると、関連するアダプティブForms内でその連結内容が自動的に反映されます<!--and interactive communications-->.

>[!NOTE]
>
>両方のメンバーでなければなりません **fdm-author** および **forms-user** フォームデータモデル（FDM）を作成して操作できるグループ。 これらのグループのメンバーになるには、[!DNL Experience Manager] の管理者に依頼してください。

## フォームデータモデル（FDM）の作成 {#data-sources}

フォームデータモデル（FDM）で使用するデータソースが、の説明に従って設定されていることを確認してください [データソースの設定](configure-data-sources.md). 設定されたデータソースに基づいてフォームデータモデル（FDM）を作成するには、以下の手順を実行します。

1. [!DNL Experience Manager] オーサーインスタンスで、**[!UICONTROL フォーム／データ統合]**&#x200B;に移動します。
1. **[!UICONTROL 作成／フォームデータモデル]**&#x200B;を選択します。
1. フォームデータモデルの作成ダイアログで、以下の操作を実行します。

   * フォームデータモデル（FDM）の名前を指定します。
   * （**オプション**） フォームデータモデル（FDM）のタイトル、説明、タグを指定します。
   * （**オプション、データソースが既に設定されている場合のみ**）「**[!UICONTROL データソース設定]**」フィールドの横にあるチェックマークアイコンを選択し、使用するデータソース用のクラウドサービスが存在する設定ノードを選択します。この操作により、選択した設定ノード内の有効なデータソースだけが、以下のページに選択可能なデータソースとして表示されます。ただし、どの [!DNL Experience Manager] ユーザープロファイルのデータソースも、デフォルトで表示されます。設定ノードを選択しない場合は、すべての設定ノードのデータソースが表示されます。

1. 「**[!UICONTROL 次へ]**」を選択します。

1. （**データソースが既に設定されている場合のみ**）**[!UICONTROL データソースを選択]**&#x200B;画面に、使用可能なデータソースが表示されます（有効なデータソースが存在する場合）。フォームデータモデルで使用するデータソースを選択します。
1. 「**[!UICONTROL 作成]**」を選択し、確認ダイアログで「**[!UICONTROL 開く]**」をクリックして、フォームデータモデルエディターを開きます。

   ここで、フォームデータモデルエディターの UI に表示される各種コンポーネントを確認します。

   ![RESTful サービス、[!DNL Experience Manager] ユーザープロファイル、RDBMS の 3 つのデータソースが含まれているフォームデータモデル](assets/fdm-ui.png)

   A. **[!UICONTROL データソース]** フォームデータモデルのデータソースをリストします。データソースを展開すると、データモデルオブジェクトとサービスが表示されます。

   B. **[!UICONTROL データソース定義を更新]** データソース定義内の変更内容が設定済みデータソースから取得され、フォームデータモデルエディターの「データソース」タブでその変更内容が反映されます。

   C. **[!UICONTROL モデル]** 追加されたデータモデルオブジェクトのコンテンツ領域が表示されます。

   D. **[!UICONTROL サービス]** 追加したデータソースの操作やサービスのコンテンツ領域が表示されます。

   E. **[!UICONTROL ツールバー]** フォームデータモデル（FDM）を操作するためのツールです。 フォームデータモデル（FDM）で選択したオブジェクトに応じて、追加のオプションがツールバーに表示されます。

   F. **[!UICONTROL 選択]** 選択したデータモデルオブジェクトとサービスをフォームデータモデルに追加します。

フォームデータモデルエディターの詳細と、フォームデータモデルエディターを使用してフォームデータモデル（FDM）の編集と設定を行う方法については、以下を参照してください。 [フォームデータモデルの操作](work-with-form-data-model.md).

## データソースの更新 {#update}

既存のフォームデータモデル（FDM）のデータソースを追加または更新するには、以下の手順を実行します。

1. に移動 **[!UICONTROL Forms/データ統合]**&#x200B;を選択し、データソースを追加または更新するフォームデータモデル（FDM）を選択して、 **[!UICONTROL プロパティ]**.
1. フォームデータモデルのプロパティで、「**[!UICONTROL ソースを更新]**」タブに移動します。

   「**[!UICONTROL ソースを更新]**」タブで、以下の操作を実行します。

   * 「**[!UICONTROL コンテキスト対応設定]**」フィールドで参照アイコンを選択し、追加するデータソースのクラウド設定が存在する設定ノードを指定します。ノードを選択しなかった場合、「**[!UICONTROL ソースを追加]**」を選択すると、`global` ノード内のクラウド設定だけが表示されます。

   * 新しいデータソースを追加するには、以下を選択します。 **[!UICONTROL ソースを追加]** フォームデータモデル（FDM）に追加するデータソースを選択します。 `global` ノード内で設定されているデータソースと、選択した設定ノード内で構成されているデータソースが、すべて表示されます。

   * 既存のデータソースを、同じタイプの別のデータソースで置き換える場合は、置き換え前のデータソースの「**[!UICONTROL 編集]**」アイコンを選択し、有効なデータソースのリストで、置き換え後のデータソースを選択します。
   * 既存のデータソースを削除する場合は、目的のデータソースの「**[!UICONTROL 削除]**」アイコンを選択します。データソースのデータモデルオブジェクトがフォームデータモデル（FDM）に追加されている場合、「削除」アイコンは無効になります。

     ![fdm-properties](assets/fdm-properties.png)

1. 「**[!UICONTROL 保存して閉じる]**」を選択して、変更内容を保存します。

>[!NOTE]
>
>フォームデータモデル（FDM）に新しいデータソースを追加したら（または、既存のデータソースを更新したら）、アダプティブFormsで連結参照を適切に更新する必要があります<!--and interactive communications--> 更新されたフォームデータモデル（FDM）を使用します。

## 特定の実行モードのコンテキスト対応設定 {#runmode-specific-context-aware-config}

[!UICONTROL フォームデータモデル（FDM）] 使用する [Sling のコンテキスト対応設定](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html?lang=ja) 異なるデータ ソース パラメータをサポートして、異なるデータ ソースに接続するには [!DNL Experience Manager] 実行モード。

条件 [!UICONTROL フォームデータモデル（FDM）] では、クラウド設定を使用してパラメーターを保存します。この設定をチェックインしてソース管理（Cloud-Manager GIT リポジトリー）を通じてデプロイすると、すべての実行モード（開発、ステージ、実稼動）で同じパラメーターを持つクラウド設定が作成されます。 ただし、テスト環境と実稼動環境で異なるデータセットを使用する必要があるユースケースの場合は、異なる [!DNL Experience Manager] 実行モード用のデータソースパラメーター（データソース URL など）を使用します。

これを行うには、データソースのパラメーターと値のペアを含む OSGi 設定を作成する必要があります。これは、次の場合に同じペアを上書きします [!UICONTROL フォームデータモデル（FDM）] 実行時のクラウド設定。 OSGi 設定はデフォルトでこれらの実行モードをサポートしているので、実行モードに基づいてデータソースパラメーターを異なる値に上書きできます。

でデプロイメント固有のクラウド設定を有効にする方法 [!UICONTROL フォームデータモデル（FDM）]:

1. 開発用ローカルインスタンスにクラウド設定を作成します。詳細な手順については、[データソースの設定方法](/help/forms/configure-data-sources.md)を参照してください。

1. クラウド設定をファイルシステムに保存します。
   1. フィルター `/conf/{foldername}/settings/cloudconfigs/fdm` を使用してパッケージを作成します。手順 1 と同じ `{foldername}` を使用します。Azure ストレージ設定用に、`fdm` を `azurestorage` で置き換えます。
   1. パッケージを構築してダウンロードします。詳しくは、[パッケージのアクション](/help/implementing/developing/tools/package-manager.md)を参照してください。

1. クラウド設定を [!DNL Experience Manager] アーキタイププロジェクトに統合します。
   1. ダウンロードしたパッケージを解凍します。
   1. `jcr_root` フォルダーをコピーして、`ui.content`／`src`／`main`／`content` に置きます。
   1. `ui.content`／`src`／`main`／`content`／`META-INF`／`vault`／`filter.xml` を更新して、フィルター `/conf/{foldername}/settings/cloudconfigs/fdm` を含めます。詳しくは、[AEM プロジェクトアーキタイプの ui.content モジュール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html?lang=ja)を参照してください。このアーキタイププロジェクトを CM パイプラインを通じてデプロイする場合、同じクラウド設定がすべての環境（または実行モード）にインストールされます。環境に基づいてクラウド設定のフィールド（URL など）の値を変更するには、次の手順で説明する OSGi 設定を使用します。

1. Apache Sling のコンテキスト対応設定を作成します。OSGI 設定の作成手順は次のとおりです。
   1. アーキタイププロジェクトの **OSGi 設定ファイルをセットアップ[!DNL Experience Manager]します。**
PID `org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider` を使用して OSGi ファクトリー設定ファイルを作成します。実行モードごとに値を変更する必要がある各実行モードフォルダーの下に、同じ名前のファイルを作成します。詳しくは、[ [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations) の OSGi の設定を参照してください。

   1. **OSGI 設定 json を設定します。** Apache Sling Context-Aware Configuration Override Provider の使用手順は次のとおりです。
      1. ローカル開発インスタンス `/system/console/configMgr` で、**[!UICONTROL Apache Sling Context-Aware Configuration Override Provider: SGi configuration]** という名前のファクトリー OSGi 設定を選択します。
      1. 説明を入力します。
      1. 「**[!UICONTROL 有効]**」を選択します。
      1. オーバーライドで、Sling オーバーライド構文の環境に基づいて変更する必要があるフィールドを指定します。詳しくは、[Apache Sling Context-Aware Configuration - Override](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax) を参照してください。例：`cloudconfigs/fdm/{configName}/url="newURL"`。複数のオーバーライドを追加するには、「**[!UICONTROL +]**」を選択します。
      1. 「**[!UICONTROL 保存]**」を選択します。
      1. OSGi 設定 JSON を取得するには、[AEM SDK Quickstart を使用した OSGi 設定の生成](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)の手順に従ってください。
      1. 前の手順で作成した OSGi Factory Configuration ファイルに JSON を配置します。
      1. 環境（または実行モード）に基づいて `newURL` の値を変更します。
      1. 実行モードに応じてシークレット値を変更するには、[Cloud Manager API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) を使用してシークレット変数を作成し、後で [OSGi 設定](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values)から参照することができます。
このアーキタイププロジェクトが CM パイプラインを通じてデプロイされる場合、オーバーライドは異なる環境（または実行モード）で異なる値を提供します。
      >[!NOTE]
      >
      >[サービスパック 6.5.13.0 でコンテキスト対応設定が利用可能](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config?lang=ja)になった後、[!DNL Adobe Managed Service] ユーザーは暗号化サポートを使用してシークレットの値を暗号化し（詳細は、[設定プロパティの暗号化サポート](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support?lang=ja)を参照）、値に暗号化テキストを配置できるようになりました。

1. [フォームデータモデルエディター](#data-sources)のデータソース定義を更新するオプションを使用してデータソース定義を更新し、FDM UI を通じて FDM キャッシュを更新し、最新の設定を取得します。

## 次の手順 {#next-steps}

これで、データソースが追加されたフォームデータモデル（FDM）が作成されました。 次に、フォームデータモデル（FDM）を編集して、データモデルオブジェクトとサービスの追加と設定、データモデルオブジェクト間の関連付けの追加、プロパティの編集、カスタムデータモデルオブジェクトとプロパティの追加、サンプルデータの生成などを行うことができます。

詳しくは、「[フォームデータモデルの操作](work-with-form-data-model.md)」を参照してください。


>[!MORELIKETHIS]
>
>* [フォームデータモデル（FDM）の使用](/help/forms/using-form-data-model.md)