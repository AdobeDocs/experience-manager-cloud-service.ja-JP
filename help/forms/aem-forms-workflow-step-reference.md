---
title: AEM FormsCloud Service上で、ワークフローを作成するのに使用できるワークフローステップと、ビジネスプロセスの自動化 (BPM) に使用できるワークフローステップはどれですか？
description: Forms 中心のワークフローを使用すると、アダプティブフォームベースのワークフローを迅速に構築できます。Adobe Sign を使用して、ドキュメントへの電子サイン、フォームをベースとしたビジネスプロセスの作成、複数データソースへのデータの取得と送信、メール通知の送信を行うことができます
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: タスクの割り当て手順の使用、PDF/A ステップへの変換、レコードステップのドキュメントの生成、ワークフローの使用、ドキュメントに署名ステップ、印刷出力ステップの生成、非インタラクティブPDF出力の生成
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '7409'
ht-degree: 99%

---


# Forms 中心の AEM Workflows - ステップリファレンスを使用して、ビジネスプロセスを自動化します。 {#forms-centric-workflow-on-osgi-step-reference}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

ワークフローモデルを使用します。 モデルは、一連の手順を定義して実行するのに役立ちます。ワークフローを一時的なものにするか、複数のリソースを使用するかなど、モデルのプロパティを定義することもできます。[ビジネスロジックを達成するために、様々な AEM ワークフローステップをモデルに含めることができます](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem)。

## Forms 中心のステップ {#forms-workflow-steps}

Forms 中心のワークフローステップは、AEM ワークフローで AEM Forms 固有の操作を実行します。これらのステップを使用すると、OSGi でアダプティブフォームをベースとした Forms 中心のワークフローを迅速に構築できます。これらのワークフローは、基本的なレビューワークフローおよび承認ワークフローの開発、ファイアウォール内およびファイアウォール間のビジネスプロセスの開発に使用できます。また、フォームのワークフローステップを使用して、次のようなことも行えます。

* 登録プロセスを管理するためのビジネスプロセス、送信後のワークフローおよびバックエンドワークフローを作成する。

* タスクを作成し、ユーザーまたはグループに割り当てる。

* AEM ワークフローで [!DNL Adobe Sign] を使用して署名用のドキュメントを送信する。

* オンデマンドまたはフォーム送信時にレコードのドキュメントを生成する。

* ワークフローモデルを様々なデータソースに接続し、データを容易に保存および取得する。

* メールステップを使用して、アクションの完了時やワークフローの開始時または完了時に、通知メールおよびその他の添付ファイルを送信する。

>[!NOTE]
>
>ワークフローモデルが外部ストレージ用にマークされている場合、すべての Forms ワークフローステップで、変数オプションのみを選択して、データファイルと添付ファイルを保存または取得できます。

## タスクを割り当てステップ {#assign-task-step}

タスクを割り当てステップは、作業項目を作成してユーザーまたはグループに割り当てます。このコンポーネントは、タスクの割り当てに加えて、タスクのアダプティブフォームまたは非インタラクティブ PDF を指定します。アダプティブフォームは、ユーザーからの入力を受け取るために必要です。また、非インタラクティブ PDF または読み取り専用のアダプティブフォームは、レビュー専用のワークフローに使用されます。

このコンポーネントを使用すると、タスクの動作を制御することもできます。例えば、レコードのドキュメントの自動作成、特定のユーザーまたはグループへのタスクの割り当て、送信済みデータのパスの指定、事前入力されるデータのパスの指定、デフォルトアクションの指定が対象になります。タスクを割り当てステップには、次のプロパティがあります。

* **[!UICONTROL タイトル]**：タスクのタイトル。タイトルは AEM インボックスに表示されます。
* **[!UICONTROL 説明]**：タスクで実行される操作の説明。この情報は、共有開発環境で作業している場合に他のプロセス開発者にとって有用です。

* **[!UICONTROL サムネールのパス]**：タスクサムネールのパス。パスを指定しない場合、アダプティブフォームではデフォルトのサムネールが表示され、レコードのドキュメントではデフォルトのアイコンが表示されます。
* **[!UICONTROL ワークフローステージ]**：1 つのワークフローに複数のステージを含めることができます。これらのステージは、AEM インボックスに表示されます。これらのステージは、モデルのプロパティ（サイドキック／ページ／ページのプロパティ／ステージ）で定義できます。
* **[!UICONTROL 優先度]**：選択した優先度が AEM インボックスに表示されます。「高」、「中」、「低」の各オプションを使用できます。デフォルト値は「中」です。
* **[!UICONTROL 期限]**：タスクが期限切れとマークされるまでの日数または時間数を指定します。「**[!UICONTROL オフ]**」を選択した場合、タスクが期限切れとマークされることはありません。タイムアウトハンドラーを指定して、タスクが期限切れになった後に特定のタスクを実行することもできます。

* **[!UICONTROL 日]**：タスクを完了するまでの日数。この日数は、タスクがユーザーに割り当てられた後にカウントされます。タスクが完了せず、「日」フィールドに指定された日数を過ぎると、期限後に選択した場合にタイムアウトハンドラーがトリガーされます。
* **[!UICONTROL 時間]**：タスクを完了するまでの時間数。時間数は、タスクがユーザーに割り当てられた後にカウントされます。タスクが完了せず、「時間」フィールドに指定された時間数を過ぎると、期限後に選択した場合にタイムアウトハンドラーがトリガーされます。
* **[!UICONTROL 期限後にタイムアウト]**：このオプションを選択して、タイムアウトハンドラー選択フィールドを有効にします。
* **[!UICONTROL タイムアウトハンドラー]**： タスクを割り当てステップが期限切れになったときに実行するスクリプトを選択します。CRX リポジトリ（[apps]/fd/dashboard/scripts/timeoutHandler）にあるスクリプトを選択できます。指定されたパスは crx リポジトリに存在しません。このパスは、使用する前に管理者が作成します。
* **[!UICONTROL タスクの詳細の最後のタスクからのアクションとコメントをハイライト表示]**： タスクの詳細セクションで最後に実行されたアクションと受け取ったコメントを表示するには、このオプションを選択します。
* **[!UICONTROL タイプ]**： ワークフローの開始時に入力するドキュメントのタイプを選択します。アダプティブフォーム、読み取り専用のアダプティブフォームまたは非インタラクティブ PDF ドキュメントを選択できます。

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL アダプティブフォームを使用]**：入力されたアダプティブフォームを検索する方法を指定します。このオプションは、「タイプ」ドロップダウンリストから「アダプティブフォーム」または「読み取り専用アダプティブフォーム」を選択した場合に使用できます。アダプティブフォームは、ワークフローに送信されたもの、絶対パスで利用できるもの、変数内のパスで利用できるものを使用できます。パスを指定するには、String 型の変数を使用します。\
  複数のアダプティブフォームをワークフローに関連付けることができます。それにより、使用可能な入力メソッドを使用して、ランタイム上でアダプティブフォームを指定できます。

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL アダプティブフォームのパス]**：アダプティブフォームのパスを指定します。ワークフローに送信済み、または絶対パスで使用可能なアダプティブフォームを使用できます。または、文字列データ型の変数に保存されたパスからアダプティブフォームを取得できます。
* **[!UICONTROL 次を使用して入力 PDF を選択]**：非インタラクティブ PDF ドキュメントのパスを指定します。このフィールドは、「タイプ」フィールドで非インタラクティブ PDF ドキュメントを選択した場合に使用できます。入力 PDF は、ペイロードに対する相対パス、絶対パスで保存されたもの、またはドキュメントデータ型の変数を使用して選択できます。例えば、[Payload_Directory]/Workflow/PDF/credit-card.pdf となります。このパスは crx リポジトリに存在しません。このパスは、使用する前に管理者が作成します。「PDF のパス」オプションを使用する場合は、有効な「レコードのドキュメント」オプションか、フォームテンプレートベースのアダプティブフォームが必要です。
* **[!UICONTROL 完了したタスクのアダプティブフォームを次の形式でレンダリングする：]**&#x200B;タスクが完了とマークされると、アダプティブフォームを読み取り専用のアダプティブフォームまたは PDF ドキュメントとしてレンダリングできます。アダプティブフォームをレコードのドキュメントとしてレンダリングするには、有効な「レコードのドキュメント」オプションか、フォームテンプレートベースのアダプティブフォームが必要です。
* **[!UICONTROL 埋め込み済み]**：以下のフィールドは、タスクへの入力として使用できます。

   * **[!UICONTROL 次を使用して入力データファイルを選択]**：入力データファイルのパス（.json、.xml、.doc またはフォームデータモデル（FDM））。ペイロードに対する相対パスを使用して入力データファイルを取得したり、ドキュメント、XML、JSON データ型の変数に格納されたファイルを取得したりできます。例えば、ファイルには、AEM インボックスアプリケーションを介してフォームに送信されるデータが含まれています。一例として、[Payload_Directory]/workflow/data というパスを指定します。
   * **[!UICONTROL 次を使用して入力添付ファイルを選択]**：指定した場所にある添付ファイルは、タスクに関連付けられたフォームに添付されます。パスは、ペイロードを基準とした相対パスにすることも、ドキュメントの変数に格納された添付ファイルを取得することもできます。一例として、[Payload_Directory]/attachments/ というパスを指定します。ペイロードを基準にして添付ファイルを指定するか、ドキュメントタイプ（配列リスト／ドキュメント）変数を使用して、アダプティブフォームの入力添付ファイルを指定できます。

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL 要求属性マッピング]**：要求属性マッピングセクションを使用して、[要求属性の名前と値を定義](work-with-form-data-model.md#bindargument)します。リクエストで指定された属性名と値に基づいて、データソースから詳細を取得します。リテラル値または String データ型の変数を使用して、要求属性値を定義できます。

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL 送信済み情報]**：以下のフィールドは、タスクの出力先として使用できます。

   * **[!UICONTROL 次を使用して出力データファイルを保存]**：データファイル（.json、.xml、.doc またはフォームデータモデル（FDM））を保存します。このデータファイルには、関連付けられたフォームを介して送信された情報が含まれます。ペイロードに対する相対パスを使用して出力データファイルを保存するか、ドキュメント、XML または JSON データ型の変数に保存できます。例えば、[Payload_Directory]/Workflow/data のように指定します。ここで、data はファイルです。
   * **[!UICONTROL 次を使用して添付ファイルを保存]**：タスクに指定されたフォーム添付ファイルを保存します。ペイロードに対する相対パスを使用して添付ファイルを保存するか、ドキュメントデータタイプの配列リストの変数に保存できます。
   * **[!UICONTROL 次を使用してレコードのドキュメントを保存]**：レコードのドキュメントファイルの保存先のパス。例えば、[Payload_Directory]/DocumentofRecord/credit-card.pdf のように指定します。レコードのドキュメントは、ペイロードに対する相対パスを使用して保存するか、ドキュメントデータ型の変数に格納できます。「**[!UICONTROL ペイロードを基準とする]**」オプションを選択した場合、パスフィールドを空のままにすると、レコードのドキュメントは生成されません。このオプションは、「タイプ」ドロップダウンリストから「アダプティブフォーム」を選択した場合にのみ使用できます。

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL 割り当て先]**／**[!UICONTROL 割り当てオプション]**：タスクをユーザーに割り当てる方法を指定します。参加者選択スクリプトを使用してタスクを動的にユーザーまたはグループに割り当てることも、タスクを特定の AEM ユーザーまたはグループに割り当てることもできます。
* **[!UICONTROL 参加者選択]**：このオプションは、「割り当てオプション」フィールドで「**[!UICONTROL ユーザーまたはグループに動的に割り当て]**」オプションを選択した場合に使用できます。ユーザーまたはグループを動的に選択するには、ECMAScript またはサービスを使用できます。詳しくは、[Adobe Experience Manager でのカスタムの動的参加者ステップの作成](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja&CID=RedirectAEMCommunityKautuk)を参照してください。

* **[!UICONTROL 参加者]**：このオプションは、「**[!UICONTROL 参加者選択]**」フィールドで「**[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]**」オプションが選択されている場合に使用できます。このフィールドでは、「RandomParticipantChooser」オプションのユーザーまたはグループを選択できます。

* **[!UICONTROL 担当者]**：このオプションは、「**[!UICONTROL 参加者選択]**」フィールドで「**[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]**」オプションが選択されている場合に使用できます。このフィールドでは、文字列データタイプの変数を選択することにより担当者を定義できます。

* **[!UICONTROL 引数]**：このフィールドは、参加者選択フィールドで RandomParticipantChoose スクリプト以外のスクリプトが選択されている場合に使用できます。このフィールドでは、参加者選択フィールドで選択したスクリプトに渡すコンマ区切りの引数のリストを指定できます。

* **[!UICONTROL ユーザーま、「割り当てオプション」フィールドたはグループ]**：選択したユーザーまたはグループにタスクが割り当てられます。このオプションは、「**[!UICONTROL 割り当てオプション]**」フィールドで「**[!UICONTROL 特定のユーザーまたはグループに割り当て]**」オプションを選択した場合に使用できます。このフィールドには、[!DNL workflow-users] グループのすべてのユーザーとグループが一覧表示されます。\
  「**[!UICONTROL ユーザーまたはグループ]**」ドロップダウンメニューには、ログインユーザーおよびグループがアクセスできるリストが表示されます。ユーザー名の表示は、その特定のユーザーの crx-repository の **[!UICONTROL users]** ノードに対するアクセス権限があるかどうかによって異なります。

* **[!UICONTROL 通知メールを送信]**： メール通知を担当者に送信するには、このオプションを選択します。この通知は、タスクがユーザーまたはグループに割り当てられたときに送信されます。「**[!UICONTROL 受信者のメールアドレス]**」オプションを使用して、メールアドレスを取得するメカニズムを指定できます。

* **[!UICONTROL 受信者のメールアドレス]**：メールアドレスは、変数に格納したり、リテラルを使用して永続的なメールアドレスを指定したり、担当者のプロファイルで指定したデフォルトのメールアドレスを使用したりできます。リテラルまたは変数を使用して、グループのメールアドレスを指定できます。変数オプションは、メールアドレスを動的に取得して使用する場合に便利です。「**[!UICONTROL 担当者のデフォルトのメールアドレスを使用する]**」オプションは、1 人の担当者に対してのみ使用できます。この場合、担当者のユーザープロファイルに保存されているメールアドレスが使用されます。

* **[!UICONTROL HTML メールテンプレート]**： 通知メールのメールテンプレートを選択します。テンプレートを編集するには、crx リポジトリの /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt にあるファイルを変更します。
* **[!UICONTROL 許可する委任先]**：AEM インボックスには、ログインユーザーが、割り当てられたワークフローを別のユーザーに委任するオプションが用意されています。同じグループ内または別のグループのワークフローユーザーにデリゲートできます。タスクが 1 人のユーザーに割り当てられ、「**[!UICONTROL 担当者グループのメンバーへのデリゲーションを許可]**」オプションが選択されている場合は、そのタスクを別のユーザーまたはグループにデリゲートできません。
* **[!UICONTROL 共有設定]**：AEM インボックスには、インボックス内の 1 人またはすべてのタスクを他のユーザーと共有するオプションが用意されています。
   * 「**[!UICONTROL 担当者がインボックスで明示的に共有することを許可する]**」オプションが選択されている場合、ユーザーは AEM インボックスでタスクを選択し、別の AEM ユーザーと共有できます。
   * 「**[!UICONTROL 担当者がインボックスの共有を使用して共有することを許可する]** option is selected and users share their Inbox items or allows other users to access their Inbox items」オプションを選択し、ユーザーがインボックス項目を共有したり、他のユーザーがインボックス項目にアクセスできるようにした場合、前述のオプションが有効になっているタスクのみが他のユーザーと共有されます。
   * **[!UICONTROL 「担当者が「不在」設定を使用して委任することを許可する]**」が選択されている場合。担当者は、このタスクを他のユーザーに委任すると共に、その他の「不在」オプションも指定できます。不在タスクに割り当てられた新しいユーザーは、不在設定で指定されたユーザーに自動的に委任（割り当て）されます。

  これにより、不在時に割り当てられたタスクを作業できない場合に、他のユーザーが担当者のタスクを選択できるようになります。

* **[!UICONTROL アクション]**／**[!UICONTROL デフォルトのアクション]**：標準提供されている送信、保存およびリセットアクションを使用できます。デフォルトのアクションはすべて、デフォルトで有効になっています。
* **[!UICONTROL ルート変数]**：ルート変数の名前。ルート変数は、ユーザーが AEM インボックスで選択したカスタムアクションを取得します。
* **[!UICONTROL ルート]**：タスクは様々なルートに分岐することができます。AEM インボックスで選択すると、ルートから値が返され、選択したルートに基づいてワークフローが分岐します。ルートは、文字列データ型の配列の変数に格納するか、**[!UICONTROL リテラル]**&#x200B;を選択して手動でルートを追加できます。

* **[!UICONTROL ルートタイトル]**：ルートのタイトルを指定します。これは AEM インボックスに表示されます。
* **[!UICONTROL Coral アイコン]**：Coral アイコンの HTML 属性を指定します。Adobe CoralUI ライブラリでは、多数のタッチファーストなアイコンを提供します。ルートのアイコンを選択して使用できます。アイコンは、タイトルと共に AEM インボックスに表示されます。変数にルートを格納した場合、ルートにはデフォルトの「タグ」Coral アイコンが使用されます。
* **[!UICONTROL 担当者がコメントを追加することを許可]**： タスクのコメントを有効にするには、このオプションを選択します。担当者は、タスクの送信時に AEM インボックス内からコメントを追加できます。
* **[!UICONTROL 変数にコメントを保存]**：コメントを文字列データ型の変数に保存します。このオプションは、「**[!UICONTROL 担当者がコメントを追加することを許可]**」チェックボックスを選択した場合にのみ表示されます。

* **[!UICONTROL 担当者がタスクに添付ファイルを追加することを許可]**： タスクの添付ファイルを有効にするには、このオプションを選択します。担当者は、タスクの送信時に AEM インボックス内から添付ファイルを追加できます。添付ファイルの最大サイズ&#x200B;**[!UICONTROL （最大ファイルサイズ）]**&#x200B;を制限することもできます。デフォルトサイズは 2 MB です。

* **[!UICONTROL 次を使用して出力タスクの添付ファイルを保存]**：添付ファイルフォルダーの場所を指定します。出力タスクの添付ファイルは、ペイロードに対する相対パスを使用するか、ドキュメントデータタイプの配列の変数に保存できます。このオプションは、「**[!UICONTROL 担当者がタスクに添付ファイルを追加することを許可]**」チェックボックスを選択し、「**[!UICONTROL フォーム / ドキュメント]**」タブの「**[!UICONTROL タイプ]**」ドロップダウンリストから、「**[!UICONTROL アダプティブフォーム]**」、「**[!UICONTROL 読み取り専用アダプティブフォーム]**」または「**[!UICONTROL 非インタラクティブ PDF ドキュメント]**」を選択した場合にのみ表示されます。

* **[!UICONTROL カスタムメタデータを使用]**： カスタムメタデータフィールドを有効にするには、このオプションを選択します。カスタムメタデータはメールテンプレートで使用されます。
* **[!UICONTROL カスタムメタデータ]**： メールテンプレートのカスタムメタデータを選択します。カスタムメタデータは、crx リポジトリの apps/fd/dashboard/scripts/metadataScripts にあります。指定されたパスは crx リポジトリに存在しません。このパスは、使用する前に管理者が作成します。また、カスタムメタデータ用のサービスを使用することもできます。さらに、`WorkitemUserMetadataService` インターフェイスを拡張してカスタムメタデータを提供することもできます。
* **[!UICONTROL 前のステップのデータを表示します]**：以前の担当者、タスクに対して既に実行されたアクション、タスクに追加されたコメントおよび完了したタスクのレコードのドキュメント（使用可能な場合）を担当者が表示できるようにするには、このオプションを選択します。
* **[!UICONTROL 以降のステップのデータを表示します]**： 後続の担当者が実行したアクションと追加したコメントを現在の担当者が表示できるようにするには、このオプションを選択します。また、このオプションを選択すると、完了したタスクのレコードのドキュメント（使用可能な場合）を現在の担当者が表示できるようになります。
* **[!UICONTROL データタイプの表示]**：デフォルトで、担当者は、レコードのドキュメント、担当者、実行されたアクションに加え、前の担当者および後続の担当者が追加したコメントを表示することができます。「データタイプの表示」オプションを使用すると、担当者に表示されるデータタイプが制限されます。

>[!NOTE]
>
>外部データストレージを使用するように AEM ワークフローモデルを設定する場合、「タスクを割り当て」ステップをドラフトとして保存するオプションと、「タスクを割り当て」ステップの履歴を取得するオプションは無効です。また、インボックスでは、保存するオプションは無効になっています。

## PDF/A に変換ステップ {#convert-pdfa}

PDF/A は、フォントを埋め込み、ファイルを解凍することで、ドキュメントのコンテンツを長期保存するためのアーカイブ形式です。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。AEM ワークフローの ***PDF/A に変換***&#x200B;ステップを使用して、PDF ドキュメントを PDF/A 形式に変換できます。

PDF/A に変換ステップには、次のプロパティがあります。

**[!UICONTROL 入力ドキュメント]**：入力ドキュメントは、ペイロードに対して相対的であり、絶対パスを持ち、ペイロードとして提供するか、ドキュメントデータタイプの変数に格納することができます。

**[!UICONTROL 変換オプション]**：このプロパティを使用して、PDF ドキュメントを PDF/A ドキュメントに変換するための設定を指定します。 このタブで使用できる様々なオプションを次に示します。

* **[!UICONTROL 互換性]**：出力 PDF/A ドキュメントが準拠しなければならない標準を指定します。PDF/A-1b、PDF/A-2b、PDF/A-3b など、様々な PDF 規格をサポートします。
* **[!UICONTROL 結果レベル]**：変換出力の結果レベルを PassFail、Summary または Detailed と指定します。
* **[!UICONTROL カラースペース]**：事前に定義されたカラースペースを、出力 PDF/A ファイルに使用できる S_RGB、COATED_FOGRA27、JAPAN_COLOR_COATED または SWOP と指定します。
* **[!UICONTROL オプションコンテンツ]**：指定した基準のセットを満たした場合にのみ、特定のグラフィックオブジェクトや注釈を出力 PDF/A ドキュメントに表示できるようにします。

**[!UICONTROL 出力ドキュメント]**：出力ファイルを保存する場所を指定します。出力ファイルは、ペイロードに関連する場所に保存でき、ペイロードがファイルの場合はペイロードを上書きするか、ドキュメントデータタイプの変数に保存できます。


## 「メールを送信」ステップ {#send-email-step}

メールのステップを使用して、レコードのドキュメント、アダプティブフォームのリンク<!-- , link of an interactive communication-->または添付 PDF ドキュメントを含むメールを送信します。メールを送信ステップは、[HTML メール](https://ja.wikipedia.org/wiki/HTML電子メール)をサポートします。HTML メールは、受信者のメールクライアントや画面サイズにレスポンシブに対応します。HTML メールテンプレートを使用して、メールの外観、カラースキーム、動作を定義できます。

メールステップは、Day CQ Mail Service を使用してメールを送信します。メールステップを使用する前に、メールサービスが設定されていることを確認してください。メールは、デフォルトで HTTP および HTTPs プロトコルのみをサポートします。[サポートチームに問い合わせて](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=ja#sending-email)、メールの送信用のポートと、環境用の SMTP プロトコルを有効にします。この制限は、プラットフォームのセキュリティの向上に役立ちます。

メールステップには、次のプロパティがあります。

**[!UICONTROL タイトル]**：ステップのタイトルは、ワークフローエディターでステップを識別するのに役立ちます。

**[!UICONTROL 説明]**：説明は、共通の開発環境で作業する他のプロセス開発者にとって有用です。

**[!UICONTROL メールの件名]**：件名は、ワークフローメタデータから取得でき、手動で指定することも、変数に格納されている値から取得することもできます。次のいずれかのオプションを選択します。

* **[!UICONTROL リテラル]** - 件名を手動で指定します。
* **[!UICONTROL ワークフローメタデータから取得]** - メタデータプロパティから件名を取得します。
* **[!UICONTROL 変数]** - 文字列データ型の変数に格納された値から件名を取得します。

**[!UICONTROL HTML メールテンプレート]**：メールの HTML テンプレート。変数はメールテンプレートで指定できます。メールステップは、入力のため、テンプレートに含まれるすべての変数を抽出して表示します。

**[!UICONTROL メールテンプレートメタデータ]**：メールテンプレート変数の値は、ユーザー指定の値にすることも、オーサーサーバーまたはパブリッシュサーバー上のアセットのパスや、画像、ワークフローメタデータプロパティにすることもできます。

* **[!UICONTROL リテラル]**：指定する値が正確に分かっている場合は、このオプションを使用します。例えば、[example@example.com](mailto:example@example.com) と指定します。

* **[!UICONTROL ワークフローメタデータ]**：使用する値がワークフローメタデータプロパティに保存されている場合は、このオプションを使用します。オプションを選択した後、「ワークフローメタデータ」オプションの下にある空のテキストボックスに、メタデータプロパティ名を入力します。例えば、emailAddress と指定します。

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL 画像]**：画像をメールに埋め込むには、このオプションを使用します。このオプションを選択したら、画像を参照して選択します。「画像」オプションは、メールテンプレートで使用できる画像タグ（&lt;img src=&quot;&#42;&quot;/>）に対してのみ使用できます。

**[!UICONTROL 送信者／受信者のメールアドレス]**：メールアドレスを手動で指定するには、「**[!UICONTROL リテラル]**」オプションを選択します。メールアドレスをメタデータプロパティから取得するには、「**[!UICONTROL ワークフローメタデータから取得]**」オプションを選択します。「**[!UICONTROL ワークフローメタデータから取得]**」オプションのメタデータプロパティ配列のリストを指定することもできます。「**[!UICONTROL 変数]**」オプションを選択して、文字列データ型の変数に格納されている値からメールアドレスを取得します。

* **[!UICONTROL 添付ファイル]**：指定された場所で使用可能なアセットがメールに添付されます。アセットのパスは、ペイロードに対する相対パスまたは絶対パスのどちらでもかまいません。一例として、[Payload_Directory]/attachments/ というパスを指定します。

「**[!UICONTROL 変数]**」オプションを選択して、ドキュメント、XML、JSON データ型の変数に格納された添付ファイルを取得します。

**[!UICONTROL ファイル名]**：メール添付ファイルの名前です。メールステップは、添付ファイルの元のファイル名を指定されたファイル名に変更します。この名前は、手動で指定することも、ワークフローメタデータのプロパティまたは変数から取得することもできます。指定する値が正確に分かっている場合は、「**[!UICONTROL リテラル]**」オプションを使用します。「**[!UICONTROL 変数]**」オプションを使用して、文字列データ型の変数に格納された値からファイル名を取得します。使用する値がワークフローメタデータプロパティに保存されている場合は、「**[!UICONTROL ワークフローメタデータから取得]**」オプションを使用します。

## レコードのドキュメントを生成ステップ {#generate-document-of-record-step}

フォームの入力時または送信時には、そのフォームを印刷物またはドキュメント形式で記録しておくことができます。このレコードは、レコードのドキュメント（DoR）と呼ばれる、レコードのドキュメントを生成ステップを使用して、アダプティブフォームの（読み取り専用またはインタラクティブの）PDF バージョンを作成することができます。PDF バージョンには、アダプティブフォームのレイアウトと共にフォームに入力された情報が含まれます。

レコードのドキュメントステップには、次のプロパティがあります。

**[!UICONTROL アダプティブフォームを使用]**：入力されたアダプティブフォームを検索する方法を指定します。アダプティブフォームは、ワークフローに送信されたもの、絶対パスで利用できるもの、変数内のパスで利用できるものを使用できます。文字列データ型の変数を使用して、「**[!UICONTROL 変数を選択して解決]**」フィールドのパスを指定できます。\
複数のアダプティブフォームをワークフローに関連付けることができます。それにより、使用可能な入力メソッドを使用して、ランタイム上でアダプティブフォームを指定できます。

**[!UICONTROL アダプティブフォームのパス]**：アダプティブフォームのパスを指定します。このフィールドは、「**[!UICONTROL アダプティブフォームを使用]**」フィールドから「**[!UICONTROL 絶対パスで使用可能]**」オプションを選択した場合に使用できます。

**[!UICONTROL 以下のオプションを使用して入力データを選択]**：アダプティブフォームの入力データのパス。データは、ペイロードに対する相対的な場所に保持したり、データの絶対パスを指定したり、ドキュメント、JSON または XML データ型の変数に格納されたデータを取得したりできます。入力データは、レコードのドキュメントを作成するためにアダプティブフォームと結合されます。

**[!UICONTROL 次を使用して入力添付ファイルのパスを選択]**：添付ファイルのパス。これらの添付ファイルは「レコードのドキュメント」に含まれます。添付ファイルは、ペイロードに対する相対的な場所に保持したり、添付ファイルの絶対パスを指定したり、ドキュメントデータ型配列の変数に格納された添付ファイルを取得したりできます。

フォルダーのパスを指定すると、添付ファイルなど、そのフォルダー内で直接使用可能なすべてのファイルがレコードのドキュメントに添付されます。指定された添付ファイルのパスに直接存在するフォルダー内に使用できるファイルがある場合、そのファイルはレコードのドキュメントに添付ファイルとして含まれます。直接存在するフォルダー内にフォルダーがある場合、それらはスキップされます。

**[!UICONTROL 以下のオプションを使用して生成されたレコードのドキュメントを保存]**：レコードのドキュメントファイルを保持する場所を指定します。ペイロードフォルダーを上書き、ペイロードディレクトリ内の任意の場所にレコードのドキュメントを配置、ドキュメントデータ型の変数にレコードのドキュメントを格納することを選択できます。

**[!UICONTROL ロケール]**：レコードのドキュメントの言語を指定します。ドロップダウンリストからロケールを選択する場合は「**[!UICONTROL リテラル]**」を選択し、文字列データ型の変数に格納されている値からロケールを取得する場合は「**[!UICONTROL 変数]**」を選択します。ロケールの値を変数に格納する際は、ロケールコードを定義します。例えば、英語は **en_US**、フランス語は **fr_FR** と指定します。

## DDX を呼び出しステップ {#invokeddx}

Document Description XML（DDX） は、その要素がドキュメントの構築ブロックを表す宣言型のマークアップ言語です。この構築ブロックには、PDF ドキュメント、XDP ドキュメントおよびその他の要素（コメント、しおり、スタイルを設定したテキストなど）が含まれます。DDX は、1 つ以上の入力ドキュメントに適用して、1 つ以上の出力ドキュメントを生成することができる一連の操作を定義します。1 つの DDX を様々なソースドキュメントに使用できます。AEM ワークフローでは様々な操作（ドキュメントのアセンブリと分割、Acrobat と XFA Forms の作成と変更およびその他 ***DDX リファレンスドキュメント***&#x200B;で説明される操作）を実行するために、[DDX を呼び出しステップ](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)を使用することができます。

DDX を呼び出しステップには次のプロパティがあります。

**[!UICONTROL 入力ドキュメント]**：入力ドキュメントのプロパティを設定するために使用します。このタブで使用できる様々なオプションを次に示します。

* **[!UICONTROL 次を使用して DDX を指定]**：ペイロードに関連する入力ドキュメントを指定し、絶対パスを持ち、ペイロードとして提供するか、ドキュメントデータタイプの変数に格納できます。
* **[!UICONTROL ペイロードからマップを作成]**：ペイロードフォルダーの下のすべてのドキュメントを Assembler で API を呼び出すのための入力ドキュメントマップに追加します。各ドキュメントのノード名は、マップのキーとして使用されます。
* **[!UICONTROL 入力ドキュメントのマップ]**：オプションは、「**[!UICONTROL 追加]**」ボタンで複数のエントリを追加するために使用します。各エントリは、マップ内のドキュメントのキーとドキュメントのソースを表します。

**[!UICONTROL 環境オプション]**：このオプションは、呼び出し API の処理設定を設定するために使用します。 このタブで使用できる様々なオプションを次に示します。

* **[!UICONTROL 検証のみ]**：入力DDXの有効性をチェックします。
* **[!UICONTROL エラー時に失敗]**：エラーの場合に呼び出し API サービスが失敗するかどうか、エラーがあるかどうかを示すブーリアン値。デフォルトでは、この値は False に設定されています。
* **[!UICONTROL 最初のベイツ番号]**：自己増分する数を指定します。 この自己増分値は、連続する各ページに自動的に表示されます。
* **[!UICONTROL デフォルトのスタイル]**：出力ファイルのデフォルトのスタイルを設定します。

>[!NOTE]
>
>環境オプションは、HTTP API との同期が維持されます。

**[!UICONTROL 出力ドキュメント]**：出力ファイルを保存する場所を指定します。 このタブで使用できる様々なオプションを次に示します。

* **[!UICONTROL ペイロードでの出力ドキュメント保存]**：ペイロードフォルダーの下で出力ドキュメントを保存したり、ペイロードがファイルの場合はペイロードを上書きしたりします。
* **[!UICONTROL 出力ドキュメントのマップ]**：ドキュメントごとに 1 つのエントリを追加して、各ドキュメントファイルを保存する場所を明示的に指定します。各エントリは、ドキュメントと、その保存場所を表します。 出力ドキュメントが複数ある場合は、このオプションが使用されます。

## フォームデータモデル（FDM）サービスの呼び出しステップ {#invoke-form-data-model-service-step}

[[!DNL AEM Forms]  のデータ統合](data-integration.md)機能により、複数の異なるデータソースを設定して接続することができます。これらのデータソースには、web サービス、REST サービス、OData サービス、CRM ソリューションがあります。[!DNL AEM Forms] のデータ統合機能を使用すると、様々なサービスを実行するフォームデータモデル（FDM）を作成して、構成されたデータベースに対して、データの取得、追加、更新を実行できます。**[!UICONTROL データモデルサービスの呼び出しステップ]**&#x200B;を使用して、フォームデータモデル（FDM）を選択し、FDM のサービスを使用できます。例えば、各種データソースの取得、更新、追加を行うことができます。

手順のフィールドの入力を説明するために、次のデータベーステーブルと JSON ファイルを例として使用します。

**[!UICONTROL CustomerDetails テーブルの例]**

<table>
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>値<br /> </td> 
  </tr> 
  <tr> 
   <td>FirstName<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>LastName</td> 
   <td>Rose</td> 
  </tr> 
  <tr> 
   <td>顧客 ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>メールアドレス<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL サンプル JSON ファイル]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

フォームデータモデル（FDM）サービスの呼び出しステップには、以下に一覧されたフィールドがあり、フォームデータモデル（FDM）の操作に役立ちます。

* **[!UICONTROL タイトル]**：ステップのタイトルです。ワークフローエディターでステップを識別するのに役立ちます。
* **[!UICONTROL 説明]**：説明は、共通の開発環境で作業する他のプロセス開発者にとって有用です。

* **[!UICONTROL フォームデータモデルのパス]**：サーバー上のフォームデータモデル（FDM）を参照して選択します。

* **[!UICONTROL エラーと検証]**：このオプションを使用すると、エラーメッセージを取得し、データソースに取得して送信するデータの検証オプションを指定できます。これらの変更により、フォームデータモデル（FDM）サービスを呼び出しステップに渡されたデータが、データソースで定義されているデータ制約に従っていることを確認できます。詳しくは、[入力データの自動検証](work-with-form-data-model.md#automated-validation-of-input-data)を参照してください

* **[!UICONTROL 検証レベル]**：検証には、基本、完全、オフの 3 つのカテゴリがあります。

   * 完全：すべての制約が検証されます。
   * 基本：必須および NULL 許容の制約のみ
   * オフ：検証は行われません。

* **[!UICONTROL 失敗時にワークフローを終了]**：制約の検証に失敗すると、ワークフローは停止します。

* **[!UICONTROL エラーコードを変数内に格納]**：エラーコードは、[文字列型の変数](variable-in-aem-workflows.md)に格納できます。

* **[!UICONTROL エラーメッセージを変数内に格納]**：エラーメッセージは、[文字列型の変数](variable-in-aem-workflows.md)に格納できます。

* **[!UICONTROL エラーの詳細を変数内に格納]**：エラーの詳細は、[JSON 型の変数に格納できます](variable-in-aem-workflows.md)。

* **[!UICONTROL サービス]**：選択したフォームデータモデル（FDM）が提供するサービスのリストです。
* **[!UICONTROL サービスの入力]**／**[!UICONTROL リテラル、変数またはワークフローメタデータおよび JSON ファイルを使用して入力データを指定]**：サービスには複数の引数を持たせることができます。ワークフローメタデータプロパティ、JSON オブジェクト、変数からサービス引数の値を取得するか、用意されたテキストボックスに直接値を入力するには、このオプションを選択します。

   * **[!UICONTROL リテラル]**：指定する値が正確に分かっている場合は、このオプションを使用します。例えば、srose@we.info と指定します。
   * **[!UICONTROL 変数]**：変数に格納された値を取得するには、このオプションを使用します。
   * **[!UICONTROL ワークフローメタデータから取得]**：使用する値がワークフローメタデータプロパティに保存されている場合は、このオプションを使用します。例えば、emailAddress と指定します。

   * **[!UICONTROL ペイロードに相対的]**：ペイロードへの相対パスに保存された添付ファイルを取得するには、オプションを使用します。オプションを選択し、添付ファイルを含むフォルダー名を指定するか、テキストボックスで添付ファイル名を指定します。

     >[!NOTE]
     >
     > **フォームデータモデルの呼び出し** ワークフローステップでは、[SharePoint リストベースのフォームデータモデルで、Base64 でエンコードされた添付ファイル配列のワークフロー側メタデータをサポートしており &#x200B;](/help/forms/connect-forms-to-sharepoint-list.md) 添付ファイルのファイル名、MIME タイプ、カスタムプロパティなどのメタデータをワークフローで渡し、保存、取得できます。
     > ![SP リストの添付ファイル &#x200B;](/help/edge/docs/forms/assets/workflow-sp-list.png)
     >
     > 「ペイロードに相対的」フォルダーの `attachment` の場所にはファイル添付が含まれています。`attachment` ペイロードに相対的 **[!UICONTROL オプションを選択した後、テキストボックスで]** を指定します。

   * **[!UICONTROL JSON ドット表記法]**：使用する値が JSON ファイル内にある場合は、このオプションを使用します。例えば、insurance.customerDetails.emailAddress と指定します。「JSON ドット表記法」オプションを使用できるのは、「入力 JSON からのマップ入力フィールド」オプションが選択されている場合だけです。
   * **[!UICONTROL 入力 JSON からのマップ入力フィールド]**：JSON ファイルのパスを指定して、その JSON ファイルから一部のサービスの引数の入力値を取得します。JSON ファイルのパスは、ペイロードとの相対パス、絶対パスにするか、JSON またはフォームデータモデル（FDM）型の変数を使用して入力 JSON ドキュメントを選択できます。

* **[!UICONTROL サービスの入力]**／**[!UICONTROL 変数または JSON ファイルを使用して入力データを指定]**：絶対パス、ペイロードに対する相対パスまたは変数に保存された JSON ファイルからすべての引数の値を取得する場合は、このオプションを選択します。
* **[!UICONTROL 次を使用して入力 JSON ドキュメントを選択]**：すべてのサービス引数の値を含む JSON ファイル。JSON ファイルのパスは、**[!UICONTROL ペイロードに対する相対パス]**&#x200B;または&#x200B;**[!UICONTROL 絶対パス]**&#x200B;のどちらでもかまいません。また、JSON またはフォームデータモデル（FDM）データ型の変数を使用して、入力 JSON ドキュメントを取得することもできます。

* **[!UICONTROL JSON ドット表記法]**：指定した JSON ファイルのすべてのオブジェクトをサービス引数の入力として使用するには、フィールドを空のままにします。指定した JSON ファイルからサービス引数の入力として特定の JSON オブジェクトを読み取るには、JSON オブジェクトにドット表記法を指定します。例えば、この節の冒頭に一覧表示されている JSON に似た JSON を使用している場合は、insurance.customerDetails を指定して、顧客のすべての詳細をサービスへの入力として提供します。
* **[!UICONTROL サービスの出力**&#x200B;[!UICONTROL ／]&#x200B;**マップして出力値を変数またはメタデータに書き込む]**： CRX リポジトリ内のワークフローインスタンスのメタデータノードのプロパティとして出力値を保存するには、このオプションを選択します。メタデータプロパティの名前を指定し、メタデータプロパティにマップされる対応するサービス出力属性を選択します。例えば、出力サービスが返す phone_number をワークフローメタデータの phone_number プロパティでマッピングします。同様に、出力は Long データ型の変数に格納できます。「**[!UICONTROL マッピングする必要があるサービス出力属性]**」オプションのプロパティを選択すると、選択したプロパティのデータを保存できる変数のみが、「**[!UICONTROL 出力を次に保存]**」オプションに設定されます。

* **[!UICONTROL サービスの出力]**／**[!UICONTROL 出力を変数または JSON ファイルに保存]**： 出力値を絶対パス、ペイロードに対する相対パス、または変数内の JSON ファイルに保存する場合は、このオプションを選択します。
* **[!UICONTROL 以下のオプションを使用して出力 JSON ドキュメントを保存する]**：出力 JSON ファイルを保存します。出力 JSON ファイルのパスは、ペイロードに対する相対パスまたは絶対パスのどちらでもかまいません。また、JSON またはフォームデータモデル（FDM）データ型の変数を使用して、出力 JSON ファイルを保存することもできます。



## ドキュメントに署名ステップ {#sign-document-step}

ドキュメントに署名ステップでは、[!DNL Adobe Sign] を使用してドキュメントに署名できます。[!DNL Adobe Sign] ワークフローステップを使用してアダプティブフォームに署名する場合、ワークフローステップの設定に応じて、フォームを順番に署名者に渡すか、すべての署名者に同時送信することができます。[!DNL Adobe Sign] が有効なアダプティブフォームは、すべての署名者が署名プロセスを完了した後にのみ、Experience Manager Forms サーバーに送信されます。

デフォルトでは、[!DNL Adobe Sign] スケジューラーサービスは、24 時間ごとに署名者の応答を確認（ポーリング）します。[現在の環境に合わせて、このデフォルト値を変更](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status)することができます。

ドキュメントへの署名手順には、次のプロパティがあります。

* **[!UICONTROL 契約名]**：契約のタイトルを指定します。契約名は、署名者に送信されるメールの件名と本文の一部として使用されます。名前は文字列データ型の変数に格納するか、**[!UICONTROL リテラル]**&#x200B;を選択して手動で追加できます。

* **[!UICONTROL ロケール]**：メールと検証オプションの言語を指定します。ロケールは文字列データ型の変数に格納するか、**[!UICONTROL リテラル]**&#x200B;を選択して、使用可能なオプションのリストからロケールを選択できます。ロケールの値を変数に格納する際は、ロケールコードを定義する必要があります。例えば、英語は **[!UICONTROL en_US]**、フランス語は **[!UICONTROL fr_FR]** と指定します。

* **[!UICONTROL Adobe Sign クラウド設定]**：[!DNL Adobe Sign] クラウド設定を選択します。[!DNL Adobe Sign] を [!DNL AEM Forms] 用に設定していない場合は、 [Adobe Sign と  [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) の統合を参照してください。

* **[!UICONTROL 次を使用して署名するドキュメントを選択]**：ペイロードに対する相対的な場所からドキュメントを選択、ドキュメントとしてペイロードを使用、ドキュメントの絶対パスを指定、またはドキュメントデータ型の変数に格納されたドキュメントを取得できます。
* **[!UICONTROL 期限までの残り日数]**：「**[!UICONTROL 期限までの残り日数]**」フィールドに指定された日数の間にタスクのアクティビティがない場合、ドキュメントは期限切れ（期限を過ぎた）としてマークされます。日数は、ドキュメントが署名のためにユーザーに割り当てられた後にカウントされます。
* **[!UICONTROL リマインダーメールの頻度]**：リマインダーメールを日単位または週単位で送信できます。週のカウントは、ドキュメントが署名のためにユーザーに割り当てられた日から始まります。
* **[!UICONTROL 署名プロセス：]**&#x200B;ドキュメントへの署名を順次おこなうか並列でおこなうかを選択できます。順次署名する場合、ドキュメントは署名のために一度に 1 人の署名者に送信されます。最初の署名者がドキュメントの署名を完了すると、ドキュメントは 2 人目の署名者に送信され、それ以降も同様です。並列で署名する場合、複数の署名者が同時に 1 つのドキュメントに署名することができます。
* **[!UICONTROL リダイレクト URL]**：リダイレクト URL を指定します。ドキュメントへの署名が完了したら、担当者を URL にリダイレクトできます。通常、この URL には、感謝のメッセージやその後の手順が含まれています。
* **[!UICONTROL ワークフローステージ]**：1 つのワークフローに複数のステージを含めることができます。これらのステージは、AEM インボックスに表示されます。これらのステージは、モデルのプロパティ（**[!UICONTROL サイドキック]**／**[!UICONTROL ページ]**／**[!UICONTROL ページのプロパティ]**／**[!UICONTROL ステージ]**）で定義できます。
* **[!UICONTROL 署名者を選択]**：ドキュメントの署名者を選択する方法を指定します。ワークフローを動的にユーザーまたはグループに割り当てることも、手動で署名者の詳細を追加することもできます。ドロップダウンで「手動」を選択すると、受信者の詳細（メール、役割、認証方法など）が追加されます。

  >[!NOTE]
  >
  >* 「役割」セクションで、受信者の役割として「署名者」、「承認者」、「同意者」、「認証済み受信者」、「フォーム入力者」および「委任者」を指定できます。
  >* 「役割」オプションで「委任者」を選択した場合、委任者は署名タスクを別の受信者に割り当てることができます。
  >* 次の認証方法を設定済みの場合： [!DNL Adobe Sign]設定に基づいて、電話による認証、ソーシャル ID に基づく認証、ナレッジベースの認証、政府機関の ID に基づく認証などの認証方法を選択します。

* **[!UICONTROL 署名者を選択するスクリプトまたはサービス]**：このオプションを使用できるのは、「署名者を選択」フィールドで「動的」オプションが選択されている場合のみです。ECMAScript またはサービスを指定して、ドキュメントの署名者と検証オプションを選択することができます。
* **[!UICONTROL 署名者の詳細]**：このオプションを使用できるのは、「署名者を選択」フィールドで「手動」オプションが選択されている場合のみです。メールアドレスを指定し、オプションの検証メカニズムを選択します。2 段階認証メカニズムを選択する前に、設定済みの [!DNL Adobe Sign] アカウントに対して対応する認証オプションが有効になっていることを確認してください。文字列データ型の変数を使用して、「メール」、「国コード」、「電話番号」の各フィールドの値を定義できます。「国コード」と「電話番号」フィールドは、「2 段階認証」ドロップダウンリストから「電話の検証」を選択した場合にのみ表示されます。
* **[!UICONTROL 署名済みドキュメント]**：署名済みドキュメントのステータスを変数に保存できます。 電子署名監査記録を追加して、よりセキュリティと合法性を確保するには、監査レポートを含めます。変数フォルダーまたはペイロードフォルダーを使用して、署名済みドキュメントを保存できます。

  >[!NOTE]
  >
  > 監査レポートは、署名済みドキュメントの最後のページに追加されます。

<!--
## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).
 
### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## 印刷出力ステップを生成 {#generatePrintedOutput}

指定したフォームデザインとデータファイルに対して PCL、PostScript、ZPL、IPL、TPCL または DPL の出力を生成します。データファイルはフォームデザインとマージされ、印刷用にフォーマットされます。この操作で生成された出力はプリンターに直接送信したり、ファイルとして保存したりできます。フォームデザインやデータをアプリケーションから使用する場合は、この操作を実行することをお勧めします。フォームデザインがネットワーク、ローカルファイルシステム、または HTTP 上の場所にある場合は、「generatePrintedOutput」操作を使用します。

例えば、アプリケーションでフォームデザインをデータファイルとマージする必要があるとします。データには数百件のレコードがあります。さらに、ZPL をサポートしているプリンターに出力を送信する必要があります。フォームデザインと入力データはアプリケーション内にあります。generatePrintedOutput 操作を使用して、レコードをフォームデザインとマージし、ZPL がサポートされるプリンターに出力を送信します。

「印刷出力を生成」ステップには、次のプロパティがあります。

**[!UICONTROL Input プロパティ]**

* **[!UICONTROL 次を使用してテンプレートファイルを選択]**：テンプレートファイルのパスを指定します。 テンプレートファイルは、ペイロードに対する相対パス、絶対パスで保存されたもの、またはドキュメントデータタイプの変数を使用して選択できます。例： [Payload_Directory]/Workflow/data.xml。パスが crx-repository に存在しない場合、管理者はパスを作成してから使用できます。 さらに、ペイロードを入力データファイルとして受け入れることもできます。

* **[!UICONTROL 次を使用してデータドキュメントを選択]**：入力データファイルのパスを指定します。入力データファイルは、ペイロードに対する相対パス、絶対パスで保存されたもの、またはドキュメントデータタイプの変数を使用して選択できます。例： [Payload_Directory]/Workflow/data.xml。パスが crx-repository に存在しない場合、管理者はパスを作成してから使用できます。

* **[!UICONTROL プリンター形式]**：XDC ファイルがない場合に出力ストリームの生成に使用するページ説明言語を指定する値。リテラル値を指定する場合、次のいずれかの値を選択します。

   * **[!UICONTROL カラー PCL]**：PCL 用の XDC ファイルを指定するには、このオプションを使用します。
   * **[!UICONTROL Generic PostScript]**：PostScript の汎用 XDC ファイルを指定するには、このオプションを使用します。
   * **[!UICONTROL ZPL 300 DPI]**：ZPL 300 DPI を使用します。 zpl300.xdc が使用されます。
   * **[!UICONTROL ZPL 600 DPI]**：ZPL 600 DPI を使用します。 zpl600.xdc ファイルが使用されます。
   * **[!UICONTROL IPL 300 DPI]**：IPL 300 DPI を使用します。 ipl300.xdc が使用されます。
   * **[!UICONTROL IPL 400 DPI]**：IPL 400 DPI を使用します。 ipl400.xdc ファイルが使用されます。
   * **[!UICONTROL TPCL 600 DPI]**：TPCL 600 DPI を使用します。 tpcl600.xdc ファイルが使用されます。
   * **[!UICONTROL PostScript Plain]**：PostScript のプレーンテキスト XDC ファイルを指定するには、このオプションを使用します。
   * **[!UICONTROL DPL300DPI]**：DPL 300 DPI を使用します。 dpl300.xdc が使用されます。
   * **[!UICONTROL DPL400DPI]**：DPL 400 DPI を使用します。 dpl400.xdc が使用されます。
   * **[!UICONTROL DPL600DPI]**：DPL 600 DPI を使用します。 dpl600.xdc が使用されます。
   * **[!UICONTROL HP_PCL_5e]**：複数の Canon デバイスをサポートするには、このオプションを使用します。


**[!UICONTROL 出力プロパティ]**

* **[!UICONTROL 次を使用して出力ドキュメントを保存]**：出力ファイルを保存する場所を指定します。 出力ファイルは、ペイロードに相対した場所の変数に保存するか、出力ファイルを保存する絶対位置を指定できます。パスが crx-repository に存在しない場合、管理者はパスを作成してから使用できます。

**[!UICONTROL 詳細プロパティ]**

* **[!UICONTROL 次を使用してコンテンツルートの場所を選択]**：コンテンツルートは、フォームデザインで使用される相対アセットを取得するための、リポジトリ内の URI、絶対参照、または場所を指定する文字列値です。 例えば、フォームデザインが `../myImage.gif` のように画像を相対的に参照する場合、`myImage.gif` は `repository://` に配置する必要があります。デフォルト値は `repository://` で、リポジトリのルートレベルを指します。

  アプリケーションからアセットを選択するとき、コンテンツルート URI パスは正確な構造になっている必要があります。例えば、フォームを SampleApp というアプリケーションから選択し、`SampleApp/1.0/forms/Test.xdp` に配置する場合、コンテンツルート URI は `repository://administrator@password/Applications/SampleApp/1.0/forms/` または `repository:/Applications/SampleApp/1.0/forms/`（認証機関情報が NULL の場合）と指定する必要があります。コンテンツルート URI をこのように指定すると、フォーム内の参照されているすべてのアセットのパスがこの URI に対して解決されます。

* **[!UICONTROL を使用して XCI ファイルを選択]**：XCI ファイルは、フォームデザイン要素に使用されるフォントやその他のプロパティを記述するために使用されます。 XCI ファイルは、ペイロードに対する相対パス、絶対パス、またはドキュメントデータタイプの変数を使用して保持できます。

* **[!UICONTROL ロケール]**：PDF ドキュメントの生成に使用する言語を設定します。リテラル値を指定する場合、リストから言語を選択するか、次のいずれかの値を選択します。
   * **[!UICONTROL Use Server Default]**&#x200B;[!DNL AEM Forms]：
（デフォルト） サーバー上で設定されているロケール設定を使用します。ロケール設定は、管理コンソールを使用して設定します（「[Designer ヘルプ](https://helpx.adobe.com/content/dam/help/ja/experience-manager/6-5/forms/pdf/using-designer.pdf)」を参照）。

   * **[!UICONTROL カスタム値を使用するには]**：
リテラルボックスにロケールコードを入力するか、ロケールコードを含む文字列変数を選択します。サポートされているすべてのロケールコードのリストについては、https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html を参照してください。

* **[!UICONTROL Copies]**：出力の作成部数を指定する整数値。デフォルト値は 1 です。

* **[!UICONTROL Duplex Printing]**：両面印刷か片面印刷かを指定する Pagination 値。この値は、PostScript と PCL をサポートするプリンターで使用されます。リテラル値を指定する場合、次のいずれかの値を選択します。
   * **[!UICONTROL Duplex Long Edge]**：両面印刷を使用し、長辺のページネーションを使用して印刷します。
   * **[!UICONTROL Duplex Short Edge]**：両面印刷を使用し、短辺のページネーションを使用して印刷します。
   * **[!UICONTROL Simplex]**：片面印刷を使用します。

## 非インタラクティブ PDF 出力手順の生成 {#generatePDFdocuments}

1. サイドキックの「Forms Workflow」タブの下にある、「非インタラクティブ PDF 出力を生成」ワークフローをドラッグします。
1. 追加したワークフローステップをダブルクリックして、コンポーネントを編集します。
1. 編集コンポーネントダイアログでは、入力ドキュメント、出力ドキュメントおよびその他のパラメーターを設定して、**[!UICONTROL OK]** をクリックします。

### 入力ドキュメント {#input-documents-3}

* **テンプレートファイル**：XDP テンプレートの場所を指定します。このフィールドは必須です。

* **データドキュメント**：テンプレートとマージする必要があるデータ xml の場所を指定します。

### 出力ドキュメント {#output-document}

**出力ドキュメント**：生成された PDF フォームの名前を指定します。

### 追加のパラメーター {#additional-parameters-1}

* **コンテンツルート**：入力 XDP テンプレートで使用されるフラグメントまたは画像が保存されるリポジトリ内のフォルダーのパスを指定します。
* **ロケール**：生成された PDF フォームのデフォルトのロケールを指定します。
* **Acrobat のバージョン**：生成された PDF フォームのターゲットの Acrobat バージョンを指定します。
* **&#x200B;**&#x200B;Linearized PDF：Web表示のために生成されたPDFフォームを最適化するかどうかを指定します。
* **タグ付き PDF**：生成された PDF をアクセシビリティ対応にするかどうかを指定します。
* **XCI ドキュメント**：XCI ファイルへのパスを指定します。

## 関連トピック {#see-also}

* [Forms 中心の AEM ワークフローの変数](/help/forms/variable-in-aem-workflows.md)
* [不在設定の指定](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->