---
title: フォームデータモデルの作成方法
description: Experience Manager Forms のデータ統合機能には、フォームデータモデルを作成して使用するための直感的なユーザーインターフェイスが用意されています。ここでは、データソースを使用せずにフォームデータモデルを作成する方法と、既に設定されているデータソースを使用してフォームデータモデルを作成する方法について説明します。
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 1f3104d4a986018675f751afa04fe0ed3b7f5c26
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 61%

---

# フォームデータモデルの作成 {#create-form-data-model}

![データ統合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] のデータ統合機能には、フォームデータモデルを作成して使用するための直感的なユーザーインターフェイスが用意されています。フォームデータモデルでは、データソースを使用してデータが交換されますが、データソースを使用せずにフォームデータモデルを作成することも、設定済みのデータソースを使用してフォームデータモデルを作成することもできます。フォームデータモデルを作成する方法には、以下の 2 つがあります。データソースが既に設定されているかどうかに応じて、いずれかの方法を選択してください。

* **事前に設定されたデータソースを使用する場合**：「[データソースの設定](configure-data-sources.md)」の説明に従ってデータソースが既に設定されている場合は、フォームデータモデルを作成する際に、それらのデータソースを選択できます。この方法の場合、選択したデータソースのすべてのデータモデルオブジェクト、プロパティ、サービスをフォームデータモデル内で使用することができます。

* **データソースが設定されていない場合**：フォームデータモデル用のデータソースが設定されていない場合であっても、データソースを使用することなくフォームデータモデルを作成することができます。フォームデータモデルを使用して、アダプティブフォーム<!--and interactive communication-->を作成し、サンプルデータを使用してテストを行うことができます。データソースが使用可能な状態になっている場合は、フォームデータモデルをそのデータソースに連結すると、関連するアダプティブフォーム<!--and interactive communications-->内でその連結内容が自動的に反映されます。

>[!NOTE]
>
>フォームデータモデルの作成と操作を行うには、**fdm-author** グループと **forms-user** グループのメンバーである必要があります。これらのグループのメンバーになるには、[!DNL Experience Manager] の管理者に依頼してください。

## フォームデータモデルの作成 {#data-sources}

フォームデータモデル内で使用するデータソースが、「[データソースの設定](configure-data-sources.md)」の説明に従って正しく設定されていることを確認してください。設定されているデータソースに基づいてフォームデータモデルを作成するには、以下の手順を実行します。

1. [!DNL Experience Manager] オーサーインスタンスで、**[!UICONTROL フォーム／データ統合]**&#x200B;に移動します。
1. **[!UICONTROL 作成／フォームデータモデル]**&#x200B;の順にタップします。
1. フォームデータモデルの作成ダイアログで、以下の操作を実行します。

   * フォームデータモデルの名前を指定します。
   * （**任意**）フォームデータモデルのタイトル、説明、タグを指定します。
   * （**任意、データソースが既に設定されている場合のみ**）「**[!UICONTROL データソース設定]**」の横にあるチェックマークアイコンをタップし、使用するデータソース用のクラウドサービスが存在する設定ノードを選択します。この操作により、選択した設定ノード内の有効なデータソースだけが、以下のページに選択可能なデータソースとして表示されます。ただし、 [!DNL Experience Manager] ユーザープロファイルデータソースは、デフォルトで一覧表示されます。 設定ノードを選択しなかった場合、すべての設定ノード内のデータソースが表示されます。

1. 「**[!UICONTROL 次へ]**」をタップします。

1. （**データソースが既に設定されている場合のみ**）「**[!UICONTROL データソースを選択]**」画面に、使用可能なデータソースが表示されます（有効なデータソースが存在する場合）。フォームデータモデルで使用するデータソースを選択します。
1. 「**[!UICONTROL 作成]**」をタップし、確認ダイアログで「**[!UICONTROL 開く]**」をタップして、フォームデータモデルエディターを開きます。

   ここで、フォームデータモデルエディターの UI に表示される各種コンポーネントを確認します。

   ![RESTful サービス、[!DNL Experience Manager] ユーザープロファイル、RDBMS の 3 つのデータソースが含まれているフォームデータモデル](assets/fdm-ui.png)

   A. **[!UICONTROL データソース]** フォームデータモデルのデータソースをリストします。データソースを展開すると、データモデルオブジェクトとサービスが表示されます。

   B. **[!UICONTROL データソース定義を更新]** データソース定義内の変更内容が設定済みデータソースから取得され、フォームデータモデルエディターの「データソース」タブでその変更内容が反映されます。

   C. **[!UICONTROL モデル]** 追加されたデータモデルオブジェクトのコンテンツ領域が表示されます。

   D. **[!UICONTROL サービス]** 追加したデータソースの操作やサービスのコンテンツ領域が表示されます。

   E. **[!UICONTROL ツールバー]** フォームデータモデルを操作するためのツールです。選択したフォームデータモデルのオブジェクトに応じて、追加のオプションがツールバーに表示されます。

   F. **[!UICONTROL 選択]** 選択したデータモデルオブジェクトとサービスをフォームデータモデルに追加します。

フォームデータモデルエディターの詳細と、フォームデータモデルエディターを使用してフォームデータモデルの編集と設定を行う方法については、「[フォームデータモデルの操作](work-with-form-data-model.md)」を参照してください。

## データソースの更新 {#update}

既存のフォームデータモデルにデータソースを追加するには（または、既存のフォームデータモデルのデータソースを更新するには）、以下の手順を実行します。

1. **[!UICONTROL フォーム／データ統合]**&#x200B;に移動し、データソースを追加または更新するフォームデータモデルを選択して、「**[!UICONTROL プロパティ]**」をタップします。
1. フォームデータモデルのプロパティで、「**[!UICONTROL ソースを更新]**」タブに移動します。

   「**[!UICONTROL ソースを更新]**」タブで、以下の操作を実行します。

   * 「**[!UICONTROL コンテキスト対応設定]**」フィールドで参照アイコンをタップし、追加するデータソースのクラウド設定が存在する設定ノードを選択します。ノードを選択しなかった場合、「**[!UICONTROL ソースを追加]**」をタップすると、`global` ノード内のクラウド設定だけが表示されます。

   * 新しいデータソースを追加する場合は、「**[!UICONTROL ソースを追加]**」をタップし、フォームデータモデルに追加するデータソースを選択します。`global` ノード内で設定されているデータソースと、選択した設定ノード内で構成されているデータソースが、すべて表示されます。

   * 既存のデータソースを、同じタイプの別のデータソースで置き換える場合は、置き換え前のデータソースの「**[!UICONTROL 編集]**」アイコンをタップし、有効なデータソースのリストで、置き換え後のデータソースを選択します。
   * 既存のデータソースを削除する場合は、目的のデータソースの「**[!UICONTROL 削除]**」アイコンをタップします。データソース内のデータモデルオブジェクトがフォームデータモデルに追加されている場合、「削除」アイコンは無効になります。

      ![fdm-properties](assets/fdm-properties.png)

1. 「**[!UICONTROL 保存して閉じる]**」をタップして、変更内容を保存します。

>[!NOTE]
>
>フォームデータモデルに新しいデータソースを追加したら（または、フォームデータモデル内の既存のデータソースを更新したら）、更新後のフォームデータモデルが使用されるアダプティブフォーム<!--and interactive communications-->で、連結参照を適切に更新する必要があります。

## 特定の実行モードのコンテキスト対応設定 {#runmode-specific-context-aware-config}

[!UICONTROL フォームデータモデル] 利用する [Sling のコンテキスト対応設定](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html?lang=ja) 異なるデータソースのパラメータをサポートし、異なるデータソースに接続するには [!DNL Experience Manager] 実行モード

条件 [!UICONTROL フォームデータモデル] はクラウド設定を使用してパラメーターを保存します。この設定をチェックインしてソース管理（Cloud-Manager GIT リポジトリ）を通じてデプロイすると、すべての実行モード（開発、ステージ、実稼動）で同じパラメーターを持つクラウド設定が作成されます。 ただし、テスト環境と実稼動環境で異なるデータセットを使用する必要がある使用例の場合は、異なる用途にデータソースパラメーター（データソース URL など）を使用します [!DNL Experience Manager] 実行モード

これをおこなうには、データソースのパラメーターと値のペアを含む OSGi 設定を作成する必要があります。 これは、 [!UICONTROL フォームデータモデル] 実行時のクラウド設定 OSGi 設定はデフォルトでこれらの実行モードをサポートしているので、実行モードに基づいてデータソースパラメーターを異なる値に上書きできます。

でデプロイメント固有のクラウド設定を有効にするには [!UICONTROL フォームデータモデル]:

1. クラウドインスタンスでローカル開発設定を作成します。 詳細な手順については、 [データソースの設定方法](/help/forms/configure-data-sources.md).

1. クラウド設定をファイルシステムに保存します。
   1. フィルターを使用してパッケージを作成 `/conf/{foldername}/settings/cloudconfigs/fdm`. 同じ `{foldername}` 手順 1 に示すように。 および `fdm` と `azurestorage` （Azure ストレージ設定用）
   1. パッケージをビルドしてダウンロードします。 詳しくは、 [パッケージアクション](/help/implementing/developing/tools/package-manager.md).

1. クラウド設定を [!DNL Experience Manager] アーキタイププロジェクト。
   1. ダウンロードしたパッケージを解凍します。
   1. コピー `jcr_root` フォルダーを `ui.content` > `src` > `main` > `content`.
   1. 更新 `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` フィルターを含める `/conf/{foldername}/settings/cloudconfigs/fdm`. 詳しくは、 [AEM Project Archetype の ui.content モジュール](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). このアーキタイププロジェクトを CM パイプラインを通じてデプロイする場合、同じクラウド設定がすべての環境（または実行モード）にインストールされます。 環境に基づいてクラウド設定のフィールド（URL など）の値を変更するには、次の手順で説明する OSGi 設定を使用します。

1. Apache Sling のコンテキスト対応設定を作成します。 OSGi 設定を作成するには：
   1. **での OSGi 設定ファイルのセットアップ [!DNL Experience Manager] アーキタイププロジェクト。**
PID を使用した OSGi Factory Configuration ファイルの作成 
`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider` で使用される様々なキャッシュに配分されます。実行モードごとに値を変更する必要がある各実行モードフォルダーの下に、同じ名前のファイルを作成します。 詳しくは、 [の OSGi の設定 [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **OSGI 設定 json を設定します。** Apache Sling Context-Aware Configuration Override Provider を使用するには：
      1. ローカル開発インスタンス `/system/console/configMgr`、という名前でファクトリ OSGi 設定を選択します。 **[!UICONTROL Apache Sling Context-Aware Configuration Override Provider:OSGi 設定]**.
      1. 説明を入力します。
      1. 選択 **[!UICONTROL 有効]**.
      1. オーバーライドの下で、sling オーバーライド構文の環境に基づいて変更する必要があるフィールドを指定します。 詳しくは、 [Apache Sling Context-Aware Configuration - Override](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). 例えば、`cloudconfigs/fdm/{configName}/url="newURL"` のようになります。複数の上書きを追加するには、「 **[!UICONTROL +]**.
      1. 「**[!UICONTROL 保存]**」を選択します。
      1. OSGi 設定 JSON を取得するには、 [AEM SDK Quickstart を使用した OSGi 設定の生成](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. 前の手順で作成した OSGi Factory Configuration Files に JSON を配置します。
      1. の値を変更 `newURL` 環境（または実行モード）に基づく。
      1. 実行モードに基づいてシークレット値を変更するには、 [cloud manager API](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 後で [OSGi 設定](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
このアーキタイププロジェクトが CM パイプラインを通じてデプロイされる場合、オーバーライドは異なる環境（または実行モード）で異なる値を提供します。

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] ユーザーは、暗号化サポートを使用して秘密鍵の値を暗号化できます ( 詳しくは、 [設定プロパティの暗号化のサポート](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) 暗号化されたテキストを [コンテキスト対応設定は、service pack 6.5.13.0で利用できます](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. データソース定義を更新するには、 [フォームデータモデルエディター](#data-sources) FDM UI を使用して FDM キャッシュをリフレッシュし、最新の構成を取得します。

## 次の手順 {#next-steps}

これで、データソースが追加されたフォームデータモデルが作成されました。この状態で、フォームデータモデルを編集してデータモデルオブジェクトとサービスの作成と設定を行ったり、データモデルオブジェクト間の関連付けを行ったり、プロパティを編集したり、カスタムのデータモデルオブジェクトとプロパティを追加したり、サンプルデータを生成したりできます。

詳しくは、「[フォームデータモデルの操作](work-with-form-data-model.md)」を参照してください。
