---
title: AEM Forms のフォームデータモデル（FDM）を操作するプロセスとは
description: データモデルオブジェクト、サービス、データモデルオブジェクトおよび子プロパティの追加、サービスの設定、OData サービスのナビゲーションプロパティの操作を行います。
feature: Adaptive Forms, Form Data Model
role: Admin, User
level: Beginner, Intermediate
exl-id: c17c0443-d4dc-41f8-9315-6cc49e6c471f
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '4146'
ht-degree: 100%

---

# フォームデータモデル（FDM）の操作 {#work-with-form-data-model}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/work-with-form-data-model.html?lang=ja) |
| AEM as a Cloud Service | この記事 |


![data-integration](do-not-localize/data-integeration.png)

フォームデータモデル（FDM）エディターには、フォームデータモデル（FDM）の編集と設定を行うための直感的なユーザーインターフェイスが用意されています。このエディターを使用すると、フォームデータモデル（FDM）内の関連データソースからデータモデルのオブジェクト、プロパティ、サービスの追加と設定を行うことができます。また、データソースを持っていないデータモデルオブジェクトとプロパティを作成し、後でそれらのオブジェクトとプロパティにデータソースを連結することもできます。さらに、データモデルオブジェクトのプロパティ用にサンプルデータを生成して編集し、これらのプロパティを使用してアダプティブフォーム<!--and interactive communications-->にデータを取り込み、プレビュー表示することもできます。フォームデータモデル（FDM）内で設定したデータモデルのオブジェクトとサービスをテストすることにより、そのフォームデータモデル（FDM）がデータソースと正しく統合されているかどうかを確認できます。

Forms のデータ統合機能を初めて使用する場合や、これまでにデータソースの設定やフォームデータモデル（FDM）の作成を行ったことがない場合は、以下のトピックを参照してください。

* [[!DNL Experience Manager Forms] データ統合](data-integration.md)
* [データソースの設定](configure-data-sources.md)
* [フォームデータモデル（FDM）の作成](create-form-data-models.md)

ここからは、フォームデータモデルエディターを使用して実行できる様々なタスクや設定について説明します。

>[!NOTE]
>
>フォームデータモデル（FDM）の作成と操作を行うには、**fdm-author** グループと **forms-user** グループにメンバーとして属している必要があります。これらのグループのメンバーになるには、[!DNL Experience Manager] の管理者に依頼してください。

## データモデルオブジェクトとサービスの追加 {#add-data-model-objects-and-services}

データソースを持つフォームデータモデル（FDM）が既に作成されている場合は、フォームデータモデルエディターを使用して、データモデルオブジェクトとサービスの追加、各種プロパティの設定、データモデルオブジェクト間の関連付けの定義、フォームデータモデル（FDM）とサービスのテストを行うことができます。

フォームデータモデル（FDM）内の使用可能なデータソースから、データモデルのオブジェクトとサービスを追加できます。追加したデータモデルオブジェクトは「モデル」タブに表示され、追加したサービスは「サービス」タブに表示されます。

データモデルオブジェクトとサービスを追加するには、以下の手順を実行します。

1. [!DNL Experience Manager] オーサーインスタンスにログインして **[!UICONTROL Forms／データ統合]**&#x200B;に移動し、データモデルオブジェクトを追加するフォームデータモデル（FDM）を開きます。
1. データソースペインでデータソースを展開して、使用可能なデータモデルオブジェクトとサービスを表示します。
1. フォームデータモデル（FDM）に追加するデータモデルオブジェクトとサービスを選択して、「**[!UICONTROL 選択項目を追加]**」を選択します。

   ![selected-objects](assets/selected-objects.png)

   選択されたデータモデルオブジェクトとサービス

   「**[!UICONTROL モデル]**」タブには、フォームデータモデル（FDM）に追加されたすべてのデータモデルオブジェクトのグラフィカル表現と、それらのオブジェクトのプロパティが表示されます。フォームデータモデル内の各データモデルオブジェクト（FDM）は、ボックスを使用して表現されます。

   ![model-tab](assets/model-tab.png)

   追加したデータモデルオブジェクトが表示された「**[!UICONTROL モデル]**」タブ

   >[!NOTE]
   >
   >データモデルオブジェクトのボックスを選択してドラッグすると、コンテンツ領域内にデータモデルオブジェクトを配置できます。フォームデータモデル（FDM）に追加されたデータモデルオブジェクトは、データソースペイン内ではすべてグレーアウトされます。

   「**[!UICONTROL サービス]**」タブには、追加されたサービスが一覧表示されます。

   ![services-tab](assets/services-tab.png)

   データモデルサービスが表示された「**[!UICONTROL サービス]**」タブ

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。詳しくは、[OData サービスのナビゲーションプロパティの操作](#work-with-navigation-properties-of-odata-services)を参照してください。

1. 「**[!UICONTROL 保存]**」を選択して、フォームモデルオブジェクトを保存します。

   >[!NOTE]
   >
   >アダプティブフォームのルールを使用すると、フォームデータモデル（FDM）の「サービス」タブで設定したサービスを呼び出せます。設定したサービスは、ルールエディターの「サービスを起動」アクションで使用できます。設定したサービスをアダプティブフォームルールで使用する方法については、「[ルールエディター](rule-editor.md)」で、「サービスを起動」ルールと「指定値」ルールに関する説明を参照してください。

## データモデルオブジェクトと子プロパティの作成 {#create-data-model-objects-and-child-properties}

### データモデルオブジェクトの作成 {#create-data-model-objects}

設定済みのデータソースからデータモデルオブジェクトを追加できますが、データソースのないデータモデルオブジェクトやデータモデルエンティティを作成することもできます。フォームデータモデル（FDM）でデータソースを設定していない場合は特に便利です。

データソースを使用せずにデータモデルオブジェクトを作成するには：

1. [!DNL Experience Manager] オーサーインスタンスにログインして **[!UICONTROL Forms／データ統合]**&#x200B;に移動し、データモデルオブジェクトまたはデータモデルエンティティを作成するフォームデータモデル（FDM）を開きます。
1. 「**[!UICONTROL エンティティを作成]**」を選択します。
1. [!UICONTROL データモデルを作成]ダイアログで、データモデルオブジェクトの名前を指定して「**[!UICONTROL 追加]**」を選択します。データモデルオブジェクトがフォームデータモデル（FDM）に追加されます。以下の図に示すように、新しく追加されたデータモデルオブジェクトは、データソースには連結されません。また、プロパティも設定されません。

   ![new-entity](assets/new-entity.png)

次に、バインドされていないデータモデルオブジェクトに子プロパティを追加できます。

### 子プロパティの追加 {#child-properties}

フォームデータモデルエディターを使用すると、データモデルオブジェクトで子プロパティを作成できます。作成時のプロパティは、データソース内のどのプロパティにもバインドされません。後で、データモデルオブジェクトを含む別のプロパティにこの子プロパティをバインドできます。

子プロパティを作成するには、以下の手順を実行します。

1. フォームデータモデルでデータモデルオブジェクトを選択して「**[!UICONTROL 子プロパティを作成]**」を選択します。
1. **[!UICONTROL 子プロパティを作成]**&#x200B;ダイアログで、 プロパティの名前とデータタイプをそれぞれ&#x200B;**[!UICONTROL 名前]**&#x200B;フィールドと&#x200B;**[!UICONTROL タイプ]**&#x200B;フィールドに指定します。必要に応じて、プロパティのタイトルと説明を指定できます。
1. プロパティが計算済みの場合は、「計算済み」を有効にします。計算済みプロパティの値は、ルールまたは式に基づいて評価されます。詳しくは、[プロパティの編集](#properties)を参照してください。
1. データモデルオブジェクトがデータソースにバインドされている場合、追加された子プロパティは、同じ名前とデータタイプを持つ親データモデルオブジェクトのプロパティに自動的にバインドされます。

   子プロパティをデータモデルオブジェクトのプロパティに手動で連結するには、「**[!UICONTROL 参照をバインド]**」フィールドの横に表示されている参照アイコンを選択します。**[!UICONTROL オブジェクトの選択]**&#x200B;ダイアログには、親データモデルオブジェクトのすべてのプロパティが一覧表示されます。バインドするプロパティを選択し、チェックマークアイコンをクリックします。子プロパティと異なるデータタイプのプロパティを選択することはできません。

1. 「**[!UICONTROL 完了]**」を選択して子プロパティを保存し、「**[!UICONTROL 保存]**」を選択してフォームデータモデル（FDM）を保存します。これで、子プロパティがデータモデルオブジェクトに追加されました。

データモデルオブジェクトとプロパティを作成したら、続いて、アダプティブフォーム<!--and interactive communications-->をそのフォームデータモデル（FDM）に基づいて作成できます。データソースの設定が完了した時点で、フォームデータモデル（FDM）をデータソースにバインドできます。関連するアダプティブフォーム<!--and interactive communications-->では、連結が自動的に更新されます。フォームデータモデル（FDM）を使用してアダプティブフォーム<!--and interactive communications-->を作成する方法については、[フォームデータモデルの使用](using-form-data-model.md)を参照してください。

### データモデルオブジェクトとプロパティの連結 {#bind-data-model-objects-and-properties}

フォームデータモデル（FDM）に統合するデータソースが使用可能な状態になったら、[データソースの更新](create-form-data-models.md#update)に記載されている説明に従い、データソースをフォームデータモデル（FDM）に追加することができます。次に、バインドされていないデータモデルオブジェクトとプロパティを以下の手順でバインドします。

1. フォームデータモデルで、データソースへのバインドの対象となるバインドされていないデータソースを選択します。
1. 「**[!UICONTROL プロパティを編集]**」を選択します。
1. **[!UICONTROL プロパティを編集]**&#x200B;ペインで、**[!UICONTROL バインド]**&#x200B;フィールドの横にある参照アイコンを選択します。フォームデータモデル（FDM）に追加されたデータソースを一覧表示する&#x200B;**[!UICONTROL オブジェクトを選択]**&#x200B;ダイアログが開きます。

   ![select-object](assets/select-object.png)

1. データソースツリーを展開し、連結するデータモデルオブジェクトを選択してチェックマークアイコンを選択します。
1. 「**[!UICONTROL 完了]**」を選択してプロパティを保存し、「**[!UICONTROL 保存]**」を選択してフォームデータモデルを保存します。これで、データモデルオブジェクトがデータソースにバインドされました。これ以降は、データモデルオブジェクトに「連結されていない」というテキストが表示されることはありません。

   ![bound-model-object](assets/bound-model-object.png)

## サービスの設定 {#configure-services}

データモデルオブジェクトのデータの読み取りと書き込みを行うには、以下の手順を実行して、読み取りサービスと書き込みサービスを設定します。

1. データモデルオブジェクト上部のチェックボックスを選択して「**[!UICONTROL プロパティを編集]**」を選択します。

   ![edit-properties](assets/edit-properties.png)

   データモデルオブジェクトの読み取りサービスと書き込みサービスの設定を行う「プロパティを編集」

   [!UICONTROL プロパティを編集]ダイアログが表示されます。

   ![edit-properties-2](assets/edit-properties-2.png)

   プロパティを編集ダイアログ

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。OData サービスのデータソースをフォームデータモデル（FDM）に追加すると、データモデルオブジェクト内のすべてのナビゲーションプロパティに対し、フォームデータモデル（FDM）でサービスを使用できます。このサービスを使用して、対応するデータモデルオブジェクトのナビゲーションプロパティを読み取ることができます。
   >
   >
   >このサービスの使用について詳しくは、「[OData サービスのナビゲーションプロパティの操作](#work-with-navigation-properties-of-odata-services)」を参照してください。

1. **[!UICONTROL トップレベルオブジェクト]**&#x200B;を切り替えて、データモデルオブジェクトを最上位のモデルオブジェクトにするかどうかを指定します。

   フォームデータモデル（FDM）で設定したデータモデルオブジェクトは、そのフォームデータモデル（FDM）に基づくアダプティブフォームのコンテンツブラウザーの「データモデルオブジェクト」タブで使用できるようになります。2 つのデータモデルオブジェクト間の関連付けを追加すると、「**[!UICONTROL データモデルオブジェクト]**」タブで、関連付け先のデータモデルオブジェクトが、関連付け元のデータモデルオブジェクトの下にネストされます。ネストされたデータモデルが最上位のオブジェクトである場合は、「**[!UICONTROL データモデルオブジェクト]**」タブにもそのデータモデルが個別に表示されます。この場合、ネストされた階層の内側と外側に 1 つずつデータモデルのエントリが表示されるので、フォームの作成者が混乱する可能性があります。関連するデータモデルオブジェクトをネストされた階層内だけで表示するには、そのデータモデルオブジェクトの「トップレベルオブジェクト」プロパティを無効にします。

1. 選択したデータモデルオブジェクトの読み取りサービスと書き込みサービスを選択します。サービスの引数が表示されます。

   ![read-write-services](assets/read-write-services.png)

   従業員データソースに対して設定されている読み取りサービスと書き込みサービス

1. 読み取りサービスの引数に表示されている ![aem_6_3_edit](assets/edit.svg) を選択して、[ユーザープロファイル属性、リクエスト属性またはリテラル値にその引数を連結](#bindargument)し、連結値を指定します。
1. 「**[!UICONTROL 完了]**」を選択して引数を保存し、もう一度「**[!UICONTROL 完了]**」を選択してプロパティを保存します。次に、「**[!UICONTROL 保存]**」を選択してフォームデータモデル（FDM）を保存します。

### バインド読み取りサービスの引数 {#bindargument}

連結値に基づいて、バインド読み取りサービスの引数をユーザープロファイル属性、リクエスト属性またはリテラル値に連結します。この値が引数としてサービスに渡され、指定した値に関連付けられた詳細がデータソースから取得されます。

#### リテラル値 {#literal-value}

**[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューから「**[!UICONTROL リテラル]**」を選択し、「**[!UICONTROL 連結値]**」フィールドに値を入力します。値に関連付けられている詳細がデータソースから取得されます。静的な値に関連付けられた詳細を取得するには、このオプションを使用します。

この例では、**4367655678** に関連付けられた詳細が、`mobilenum` 引数の値としてデータソースから取得されます。モバイル番号の引数に値を渡す場合、関連する詳細には、顧客名、顧客の住所、市区町村などのプロパティを含めることができます。

![リテラル値](assets/fdm_binding_literal_new.png)

#### ユーザープロファイルの属性 {#user-profile-attribute}

**[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューから「**[!UICONTROL ユーザープロファイル属性]**」を選択し、「**[!UICONTROL 連結値]**」フィールドに属性名を入力します。[!DNL Experience Manager] インスタンスにログインしたユーザーの詳細は、属性名に基づいてデータソースから取得されます。

「**[!UICONTROL 連結値]**」フィールドで指定する属性名には、ユーザーの属性名までの完全な連結パスを含める必要があります。以下の URL を開いて、CRXDE のユーザー詳細にアクセスします。

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![ユーザープロファイル](assets/binding_crxde_user_profile_new.png)

この例では、`grios` ユーザーの「**[!UICONTROL 連結値]**」フィールドに `profile.empid` を指定します。

![引数を編集](assets/edit_argument_user_profile_new.png)

`id` 引数を使用してユーザープロファイルの `empid` 属性の値を取得し、それを引数として読み取りサービスに渡しています。ログインしたユーザーに関連付けられた `empid` の従業員データモデルオブジェクトから、関連付けられたプロパティの値を読み取って返します。

#### リクエスト属性 {#request-attribute}

リクエスト属性を使用して、データソースから関連付けられたプロパティを取得します。

1. **[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューから「**[!UICONTROL リクエスト属性]**」を選択し、「**[!UICONTROL 連結値]**」フィールドに属性名を入力します。

1. head.jsp の[オーバーレイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/overlays.html?lang=ja#developing)を作成します。オーバーレイを作成するには、CRX DEを開き、`https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp` ファイルを `https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp` にコピーします

   >[!NOTE]
   >
   > * 静的テンプレートを使用する場合は、head.jsp を以下の場所にオーバーレイします。
   >   `/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`
   > * 編集可能なテンプレートを使用する場合は、aftemplatedpage.jsp を以下の場所でオーバーレイします。
   >   `/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp`

1. リクエスト属性に [!DNL paramMap] を設定します。例えば、apps フォルダーの .jsp ファイルに以下のコードを含めます。

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   例えば、以下のコードを使用して、データソースから petid の値を取得します。


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

詳細は、リクエストで指定された属性名に基づいてデータソースから取得されます。

例えば、リクエストで属性を `petid=100` と指定すると、属性値に関連付けられたプロパティがデータソースから取得されます。

## 関連付けの追加 {#add-associations}

通常、データソース内のデータモデルオブジェクト間には関連付けが構築されています。この関連付けは、1 対 1 の場合もあれば、1 対多の場合もあります。例えば、1 人の従業員に対して複数の扶養家族を関連付けることができます。これを、1 対多の関連付けといいます。関連するデータモデルオブジェクトを接続するライン上では、「`1:n`」として表示されます。それに対して、特定の従業員 ID で一意の従業員名が返される場合などは、1 対 1 の関連付けになります。

データソース内の関連データモデルオブジェクト（FDM）をフォームデータモデルに追加した場合、それらの関連付けは維持され、矢印の線で接続された状態で表示されます。フォームデータモデル（FDM）内の異なる複数のデータソース全体で、データモデルオブジェクト間に関連付けを作成することができます。

>[!NOTE]
>
>JDBC データソースの事前定義済みの関連付けは、フォームデータモデル（FDM）では保持されません。それらは手動で作成する必要があります。

関連付けを追加するには：

1. データモデルオブジェクト上部のチェックボックスを選択して、データモデルオブジェクトを選択し「**[!UICONTROL 関連付けを追加]**」を選択します。関連付けを追加ダイアログが表示されます。

   ![add-association](assets/add-association.png)

   >[!NOTE]
   >
   >OData サービスのメタデータドキュメントには、データモデルオブジェクトとサービスのほかに、2 つのデータモデルオブジェクト間の関連付けを定義するナビゲーションプロパティが含まれます。フォームデータモデル（FDM）で関連付けを追加する際に、これらのナビゲーションプロパティを使用できます。詳しくは、[OData サービスのナビゲーションプロパティの操作](#work-with-navigation-properties-of-odata-services)を参照してください。

   [!UICONTROL 関連付けを追加]ダイアログが表示されます。

   ![add-association-2](assets/add-association-2.png)

   関連付けを追加ダイアログ

1. 関連付けを追加ペインで、以下の操作を実行します。

   * 関連付けのタイトルを入力します。
   * 関連付けのタイプ（「**[!UICONTROL 1 対 1]**」または「**[!UICONTROL 1 対多]**」）を選択します。
   * 関連付けるデータモデルオブジェクトを選択します。
   * 選択したモデルオブジェクトからデータを読み取るための読み取りサービスを選択します。読み取りサービスの引数が表示されます。必要に応じて引数を編集し、関連付けるデータモデルオブジェクトのプロパティにその引数をバインドします。

   以下に示す例では、「扶養家族」データモデルオブジェクトの読み取りサービスのデフォルト引数が `dependentid` になっています。

   ![add-association-example](assets/add-association-example.png)

   「扶養家族」読み取りサービスのデフォルト引数が dependentid になっている

   ただし、この引数は、関連付けるデータモデルオブジェクト間の共通プロパティ（この例の場合は `Employeeid`）でなければなりません。そのため、`Employeeid` 引数を「従業員」データモデルオブジェクトの `id` プロパティにバインドして、関連付けられている扶養家族の詳細情報を「扶養家族」データモデルオブジェクトから取得する必要があります。

   ![add-association-example-2](assets/add-association-example-2.png)

   更新後の引数とバインディング

   「**[!UICONTROL 完了]**」を選択して、引数を保存します。

1. 「**[!UICONTROL 完了]**」を選択して関連付けを保存し、「**[!UICONTROL 保存]**」をクリックしてフォームデータモデル（FDM）を保存します。
1. 必要に応じて上記の手順を繰り返し、さらに関連付けを作成します。

>[!NOTE]
>
>追加した関連付けは、入力したタイトルと、関連データモデルオブジェクトを接続する線とともに、データモデルオブジェクトのボックス内に表示されます。
>
>関連付けを編集するには、その関連付けのチェックボックスを選択して「**[!UICONTROL 関連付けを編集]**」を選択します。

![added-association](assets/added-association.png)

## プロパティの編集 {#properties}

フォームデータモデル（FDM）内で追加されたデータモデルオブジェクト、それらのプロパティおよびサービスのプロパティを編集できます。

プロパティを編集するには：

1. フォームデータモデル（FDM）内のデータモデルオブジェクト、プロパティまたはサービスの横に表示されているチェックボックスを選択します。
1. 「**[!UICONTROL プロパティを編集]**」を選択します。選択したモデルオブジェクト、プロパティまたはサービスの&#x200B;**[!UICONTROL プロパティを編集]**&#x200B;ペインが開きます。

   * **[!UICONTROL データモデルオブジェクト]**：読み取りサービスと書き込みサービスを指定し、引数を編集します。
   * **[!UICONTROL プロパティ]**：プロパティのタイプ、サブタイプ、形式を指定します。選択したプロパティをデータモデルオブジェクトのプライマリキーにするかどうかを指定することもできます。
   * **[!UICONTROL サービス]**：サービスの入力モデルオブジェクト、出力タイプおよび引数を指定します。Get サービスの場合は、配列を返すようにするかどうかを指定できます。

     ![edit-properties-service](assets/edit-properties-service.png)

   Get サービスのプロパティを編集ダイアログ

1. 「**[!UICONTROL 完了]**」を選択してプロパティを保存し、「**[!UICONTROL 保存]**」を選択してフォームデータモデル（FDM）を保存します。

### 計算済みプロパティを作成 {#computed}

計算済みプロパティとは、ルールまたは式に基づいて値が計算されるプロパティのことです。ルールを使用して、計算済みプロパティの値を、リテラル文字列、数値、数式の計算結果、フォームデータモデル（FDM）内の別のプロパティの値に設定できます。

例えば、既存の **FirstName** プロパティと **LastName** プロパティの値を組み合わせた値を持つ **FullName** という計算済みプロパティを作成することができます。そのためには、以下の手順を実行します。

1. `FullName` という名前の新しいプロパティを作成し、データタイプとして String を設定します。
1. 「**[!UICONTROL 計算済み]**」を有効にし、「**[!UICONTROL 完了]**」を選択してプロパティを作成します。

   ![計算済み](assets/computed.png)

   FullName という計算済みプロパティが作成されます。このプロパティの横に、計算済みプロパティであることを表すアイコンが表示されます。

   ![computed-prop](assets/computed-prop.png)

1. FullName プロパティを選択して「**[!UICONTROL ルールを編集]**」を選択します。ルールエディターウィンドウが表示されます。
1. ルールエディターウィンドウで、「**[!UICONTROL 作成]**」を選択します。「**[!UICONTROL Set Value]**」ルールウィンドウが開きます。

   オプション選択ドロップダウンで、「**[!UICONTROL 数式]**」を選択します。「**[!UICONTROL フォームデータモデルのオブジェクト]**」オプションや「**[!UICONTROL 文字列]**」オプションを選択することもできます。

1. 数式の最初のオブジェクトとして「**[!UICONTROL FirstName]**」を選択し、2 番目のオブジェクトとして「**[!UICONTROL LastName]**」を選択します。演算子として「**[!UICONTROL プラス]**」を選択します。

   「**[!UICONTROL 完了]**」、「**[!UICONTROL 閉じる]**」の順に選択して、ルールエディターウィンドウを閉じます。ルールは以下のようになります。

   ![ルール](assets/rule.png)

1. フォームデータモデル（FDM）で、「**[!UICONTROL 保存]**」を選択します。これで、計算済みプロパティが設定されました。

## OData サービスのナビゲーションプロパティを操作 {#work-with-navigation-properties-of-odata-services}

OData サービスでは、ナビゲーションプロパティを使用して、2 つのデータモデルオブジェクト間の関連付けが定義されます。これらのプロパティは、エンティティタイプまたは複合タイプで定義されます。例えば、サンプルの [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData サービスのメタデータファイルから抽出した以下のコードの場合、Friends、BestFriend、Trips という 3 つのナビゲーションプロパティが Person エンティティに含まれています。

ナビゲーションプロパティについて詳しくは、「[OData のドキュメント](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)」を参照してください。

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

フォームデータモデル（FDM）内で OData サービスを設定すると、そのフォームデータモデル（FDM）内のサービスを経由して、エンティティコンテナ内のすべてのナビゲーションプロパティを使用できるようになります。このサンプルの TripPin OData サービスでは、フォームデータモデル（FDM）内の `GET LINK` サービスを使用して、`Person` コンテナに含まれている 3 つのナビゲーションプロパティを読み取ることができます。

以下の図では、フォームデータモデル（FDM）内の `GET LINK of Person /People` サービスがハイライト表示されています。これは、TripPin OData サービスの `Person` エンティティに含まれている 3 つのナビゲーションプロパティを組み合わせたサービスです。

![nav-prop-service](assets/nav-prop-service.png)

フォームデータモデル（FDM）の「サービス」タブに `GET LINK` サービスを追加すると、サービス内で使用する出力モデルオブジェクトとナビゲーションプロパティを選択するための各種プロパティを編集できるようになります。例えば、以下の `GET LINK of Person /People` サービスでは、出力モデルオブジェクトとして「Trip」を使用し、ナビゲーションプロパティとして「Trips」を使用しています。

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>**NavigationPropertyName** 引数の「**[!UICONTROL デフォルト値]**」フィールドで指定できる値は、「**[!UICONTROL 配列を返しますか？]**」トグルボタンの状態によって異なります。このボタンが有効になっている場合は、コレクションタイプのナビゲーションプロパティが表示されます。

この例では、出力モデルオブジェクトとして「Person」を選択し、ナビゲーションプロパティの引数として「Friends」または「BestFriend」を選択することもできます（どちらを選択するかは、「**[!UICONTROL 配列を返しますか？]**」ボタンが有効になっているか無効になっているかによって異なります）。

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

同様に、フォームデータモデル（FDM）で関連付けを追加する際に `GET LINK` サービスを選択し、サービスのナビゲーションプロパティを設定することができます。ただし、ナビゲーションプロパティを選択するには、**[!UICONTROL 連結先]**&#x200B;ドロップダウンメニューで「**[!UICONTROL リテラル]**」に設定されている必要があります。

![add-association-nav-prop](assets/add-association-nav-prop.png)

## サンプルデータの生成と編集 {#sample}

フォームデータモデル（FDM）エディターを使用して、計算済みプロパティを含むすべてのデータモデルオブジェクトプロパティのサンプルデータを、フォームデータモデル（FDM）内で生成できます。各プロパティで設定されたデータタイプに基づいて、一連のランダムな値がサンプルデータとして生成されます。このサンプルデータを編集して保存することもできます。サンプルデータを再生成した場合も、編集したサンプルデータは保存されたままになります。

サンプルデータを生成して編集するには、以下の手順を実行します。

1. フォームデータモデル（FDM）を開いて「**[!UICONTROL サンプルデータを編集]**」を選択します。サンプルデータが生成され、サンプルデータ編集ウィンドウに表示されます。

   ![サンプルデータの生成](assets/form_data_model_generate_sample_data_new.png)

1. **[!UICONTROL サンプルデータを編集]**&#x200B;ウィンドウでデータを編集して「**[!UICONTROL 保存]**」を選択します。

<!--Next, you can use the sample data to prefill and test interactive communications based on the form data model. For more information, see [Use form data model](using-form-data-model.md).-->

## データモデルオブジェクトとサービスのテスト {#test-data-model-objects-and-services}

これまでの手順で設定したフォームデータモデル（FDM）を使用する前に、設定したデータモデルオブジェクトとサービスが正しく動作するかどうかをテストすることをお勧めします。データモデルオブジェクトとサービスをテストするには、以下の手順を実行します。

1. フォームデータモデル（FDM）でデータモデルオブジェクトまたはサービスを選択して、「**[!UICONTROL モデルオブジェクトをテスト]**」または「**[!UICONTROL サービスをテスト]**」をクリックします。

   フォームデータモデルをテストウィンドウが表示されます。

   ![test-data-model](assets/test-data-model.png)

1. [!UICONTROL フォームデータモデルをテスト] ウィンドウの入力ペインで、テストするデータモデルオブジェクトまたはサービスを選択します。

1. テストコードで引数の値を指定して「**[!UICONTROL テスト]**」を選択します。テストが成功すると、出力ペインに出力情報が返されます。

   ![テストの結果](assets/test_results_form_data_model_new.png)

同様の方法で、フォームデータモデル（FDM）内の他のデータモデルオブジェクトやサービスをテストすることができます。

## 入力データの自動検証 {#automated-validation-of-input-data}

フォームデータモデル（FDM）は、DermisBridge API を呼び出す際に入力として受け取ったデータを（フォームデータモデルで使用可能な検証条件に基づいて）検証します。検証は、API の呼び出しに使用されるクエリオブジェクトに設定された `ValidationOptions` フラグに基づいて行われます。

このフラグは、以下のいずれかの値に設定できます。

* **完全**：FDM は、すべての制約に基づいて検証を実行します
* **オフ**：検証なし
* **基本**：FDM は、「required」制約および「nullable」制約に基づいて検証を実行します

`ValidationOptions`フラグに値が設定されていない場合、入力データに対して&#x200B;**基本**&#x200B;検証が実行されます。

以下に、検証フラグを&#x200B;**完全**&#x200B;に設定する例を示します。

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>入力データの属性に指定する値は、メタデータドキュメントの属性に定義されているデータタイプと一致する必要があります。\
>値が属性に対して定義されたデータタイプと一致しない場合、DermisBridge API は `ValidationOptions` フラグの値に関係なく例外を表示します。ログレベルが「デバッグ」に設定されている場合は、**error.log** ファイルにエラーが記録されます。

フォームデータモデル（FDM）は、データタイプ制約のリストに基づいて入力データを検証します。入力データに対する制約のリストは、データソースによって異なる場合があります。

以下の表に、データソースに基づく入力データの制約事項を示します。

<table>
 <tbody> 
  <tr> 
   <td>制約</td> 
   <td>説明</td> 
   <td>入力データソース</td> 
  </tr> 
  <tr> 
   <td>required</td> 
   <td>true の場合、パラメーターを入力データに含める必要があります。</td> 
   <td>Swagger、WSDL およびデータベース</td> 
  </tr> 
  <tr> 
   <td>nullable</td> 
   <td>true の場合、入力データでパラメーターの値を Null に設定できます。</td> 
   <td>WSDL、Odata およびデータベース</td> 
  </tr> 
  <tr> 
   <td>maximum</td> 
   <td>数値の上限を指定します。また、上限として指定した最大値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>minimum</td> 
   <td>数値の下限を指定します。また、下限として指定した最小値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMaximum</td> 
   <td>数値の上限を指定します。上限として指定した最大値を入力データのパラメーターに割り当てないでください。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>数値の下限を指定します。下限として指定した最小値を入力データのパラメーターに割り当てないでください。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>文字列に含まれる文字数の下限を指定します。また、下限として指定した最小値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>文字列に含まれる文字数の上限を指定します。また、上限として指定した最大値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger、WSDL、Odata およびデータベース</td> 
  </tr> 
  <tr> 
   <td>pattern</td> 
   <td>文字の固定シーケンスを指定します。文字が指定したパターンに適合する場合にのみ、入力文字列が正常に検証されます。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>配列の項目の最小数を指定します。また、下限として指定した最小値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>配列の項目の最大数を指定します。また、上限として指定した最大値も入力データのパラメーターに割り当てることができます。</td> 
   <td>Swagger および WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>true の場合、配列のすべての要素は入力データ内で一意である必要があります。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>enum（文字列）<br /> <br /> </td> 
   <td>入力データ内のパラメーターの値を固定の文字列の値のセットに制限します。1 つ以上の要素がある配列であり、各要素は一意である必要があります。</td> 
   <td>Swagger、WSDL および Odata</td> 
  </tr> 
  <tr> 
   <td>enum （数値）<br /> <br /> </td> 
   <td>入力データ内のパラメーターの値を、一定の数値のセットに制限します。1 つ以上の要素がある配列であり、各要素は一意である必要があります。</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

この例では、Swagger ファイルで定義されている最大制約、最小制約、必須制約に基づいて入力データが検証されます。注文 ID が存在し、その値が 1～10 の場合にのみ、入力データは検証条件を満たします。

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that must be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

入力データが検証条件を満たさない場合は、例外が表示されます。ログレベルが「**デバッグ**」に設定されている場合は、**error.log** ファイルにエラーが記録されます。例：

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## 次の手順 {#next-steps}

これで、作業用のフォームデータモデル（FDM）を、アダプティブフォーム<!--and interactive communications-->のワークフローで使用する準備が整いました。次の手順として、実際にこのフォームデータモデル（FDM）を使用します。詳しくは、[フォームデータモデル（FDM）の使用](using-form-data-model.md)を参照してください。
