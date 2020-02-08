---
title: ローンチの作成
description: 今後のアクティベートのために既存の Web ページの新しいバージョンを更新できるように、ローンチを作成できます。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# ローンチの作成 {#creating-launches}

ローンチを作成し、今後のアクティベートのために既存の Web ページの新しいバージョンを更新できるようにします。起動を作成する際に、タイトルとソースページを指定します。

* The title appears in the [References](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) rail, from where authors can access them to work on them.
* デフォルトで、ソースページの子ページがローンチに含まれています。希望に応じて、ソースページのみを使用することもできます。
* デフォルトでは、ライブコピーによってソースページの変更に合わせてローンチページが自動的に更新されます。You can specify that a static copy is created to prevent automatic changes. <!--By default, [Live Copy](/help/sites-administering/msm.md) automatically updates the launch pages as the source pages change. You can specify that a static copy is created to prevent automatic changes.-->

オプションとして、**ローンチ日**（と時間）を指定して、ローンチページを昇格およびアクティベートするタイミングを定義できます。However the **Launch Date** only operates in combination with the **Production Ready** flag (see [Editing a Launch Configuration](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)); for the actions to actually occur automatically, both must be set.

## ローンチの作成 {#creating-a-launch}

ローンチは、次のようにサイトまたはローンチコンソールから作成できます。

1. **サイト**&#x200B;コンソールまたは&#x200B;**ローンチ**&#x200B;コンソールを開きます。

   >[!NOTE]
   >
   >**サイト**&#x200B;コンソールを使用する場合、通常はソースページに移動しますが、ウィザードで「**ローンチのソース**」を選択するときに移動できるので、これは強制ではありません。

1. 使用しているコンソールに応じて、次の操作をおこないます。
   * **ローンチ**:
      1. ツールバーの「**ローンチを作成**」を選択してウィザードを開きます。
   * **サイト**：
      1. ツールバーの「**作成**」を選択して選択ボックスを開きます。
      1. ここから「**ローンチを作成**」を選択してウィザードを開きます。
   >[!NOTE]
   >
   >**サイト**&#x200B;コンソールで、「[選択モード](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)」を使用して、「**作成**」を選択する前にページを選択できます。
   >
   >こうすることで、最初のソースページとして選択されたページが使用されます。

1. **ソースを選択**&#x200B;のステップでは、**ページを追加**&#x200B;する必要があります。複数のページを選択することもできます。それぞれにパスを指定します。
   * 必要な場所に移動します。
   * ソースページを選択し、確認（チェックマーク）します。
   必要に応じて繰り返します。

   ![起動元の選択](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >ローンチにページやブランチを追加するには、ページやブランチがサイト内（共通のトップレベルのルートの下）にある必要があります。
   >
   >サイトのトップレベルの下に言語ルートがある場合、ローンチのページやブランチは共通の言語ルートに下にある必要があります。

1. 各エントリについて、次の操作をおこなうかどうかを指定できます。

   * **サブページを含める**：

      * ローンチを子ページと共に作成するかどうかを指定します。 デフォルトでは、このサブページが含まれます。
   「**次へ**」をクリックして次に進みます。

   ![起動元の選択](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. ウィザードの&#x200B;**プロパティ**&#x200B;のステップでは、次の情報を指定できます。

   * **ローンチタイトル**：ローンチの名前。作成者にとって意味のある名前にしてください。
   * **既存のコンテンツを使用**：元のコンテンツを使用してローンチを作成します。
   * **新しいテンプレートを使用してページを置き換える**：詳しくは、[新しいテンプレートでのローンチの作成](#create-launch-with-new-template)を参照してください。
   * **ソースページのライブデータを継承**：ソースページに変更があったときにローンチページのコンテンツを自動的に更新する場合は、このオプションを選択します。このオプションは、起動をライブコピーにすることで実現します。  デフォルトでは、このオプションが選択されています。<!--Select this option to automatically update the content of launch pages when the source pages change. This option achieves this by making the launch a [live copy](/help/sites-administering/msm.md). By default, this option is selected.-->
   * **ローンチ日**：ローンチコピーがアクティベートされる日付と時間（「**実稼動準備完了**」フラグによって変わります。[ローンチ - イベントの順序](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)を参照してください）。
   ![起動プロパティ](/help/sites-cloud/authoring/assets/launches-properties.png)

1. 「**作成**」を使用してプロセスを完了し、新しいローンチを作成します。ローンチをすぐに開くかどうかを確認するダイアログが表示されます。

   （「**完了**」を使用して）コンソールを戻す場合、次のいずれかからローンチを確認（およびアクセス）できます。

   * The [**Launches **console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * The [**References **in the** Sites **console](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### 新しいテンプレートでのローンチの作成 {#create-launch-with-new-template}

ローンチを作成するときに、新しいテンプレートを使用するかどうかを選択できます。

>[!NOTE]
>
>このオプションは、**サイト**&#x200B;コンソールからローンチを作成する場合にのみ使用できます。**ローンチ**&#x200B;コンソールからローンチを作成する場合は使用できません。

![新しいテンプレートを使用した起動の作成](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

これを選択すると、次の処理がおこなわれます。

* 使用可能な他のオプションを更新します。
* 必要なテンプレートを選択できる新しい手順を含めます。

![新しいテンプレートの選択](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>別のテンプレートが使用されると、新しいページは空になります。ページ構造が異なるので、コンテンツはコピーされません。
>
>このメカニズムを使用して、[既存のページ](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)のテンプレートを変更できます。ただし、コンテンツが失われることは考慮する必要があります。

### ネストされたローンチの作成 {#creating-a-nested-launch}

ネストされたローンチを作成（ローンチをローンチ内に作成）して、既存のローンチからローンチを作成できます。これにより、作成者は各ローンチで同じ変更を複数回加えることなく、既に加えられた変更を活用できます。

>[!NOTE]
>
>[ネストされたローンチの作成](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch)も参照してください。

#### ネストされたローンチの作成 - ローンチコンソール {#creating-a-nested-launch-launches-console}

Creating a nested launch from the **Launches** console is basically the same as creating any other form of launch, with the exception that you need to navigate to the launches branch `/content/launches`:

1. **ローンチ**&#x200B;コンソールで「**作成**」を選択します。
1. Select **Add Pages**, then navigate to the launches branch by specifying `/content/launches` in the filter. 必要なローンチを選択し「**選択**」で確認します。

   ![ネストされた起動の作成](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. 「**次へ**」で続行し、他のローンチと同様に「**プロパティ**」に入力します。

   ![入れ子になった起動のソースを選択](/help/sites-cloud/authoring/assets/launches-create-nested-select.png)

#### ネストされたローンチの作成 - サイトコンソール {#creating-a-nested-launch-sites-console}

既存のローンチに基づいてネストされたローンチを&#x200B;**サイト**&#x200B;コンソールから作成するには、次のようにします。

1. [「参照」のローンチ（サイトコンソール）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)にアクセスして使用可能なアクションを表示します。
1. 「**ローンチを作成**」を選択してウィザードを開きます（ソースは既に選択されているので、**ソースを選択**&#x200B;のステップはスキップします）。
1. **ローンチタイトル**&#x200B;やその他必要な詳細を、通常のローンチと同様に入力します。
1. 「**作成**」を使用してプロセスを完了し、新しいローンチを作成します。ローンチをすぐに開くかどうかを確認するダイアログが表示されます。

If you select **Done**, you are returned to the **References** rail of the **Sites** console, if you select the appropriate page your new launch is shown.

### ローンチの削除 {#deleting-a-launch}

ローンチは[ローンチコンソール](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)から削除できます。

* サムネイルをタップまたはクリックして、ローンチを選択します。
* ツールバーが表示されたら、「削除」を選択します。
* アクションを確定します。

>[!CAUTION]
>
>ローンチを削除すると、ローンチ自体およびネストされているすべてのローンチが削除されます。
