---
title: アセット処理のためのアセットマイクロサービスの設定と使用
description: クラウドネイティブのアセットマイクロサービスを設定して使用し、アセットをスケールで処理する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# アセットマイクロサービスの概要 {#get-started-using-asset-microservices}

<!--

* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.

-->

アセットマイクロサービスは、様々なアセットタイプや処理オプションを最適に処理するためにアドビが管理するクラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。

アセット処理は、デフォルトの設定を提供する **[!UICONTROL Processing Profiles]**（処理プロファイル）の設定に基づいて実行され、管理者は、より具体的なアセット処理設定を追加できます。 拡張性と完全なカスタマイズを可能にするために、アセット処理では後処理ワークフローのオプション設定が可能になり、後処理ワークフローは管理者が作成および管理します。

クラウドサービスとしてのExperience Managerでのアセット処理の概要を以下に示します。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![asset-microservices-flow](assets/asset-microservices-flow.png)

>[!NOTE]
>
> 以前のバージョンのExperience Managerからアップデートしたお客様向け：この節で説明するアセット処理は、以前のアセット取り込み処理に使用された「DAM Update Asset」ワークフローモデルに代わるものです。 標準的なレンディションの生成とメタデータ関連の手順のほとんどは、アセットマイクロサービスの処理に置き換えられ、残りの手順は、後処理ワークフローの設定に置き換えることができます。

## アセット処理の概要 {#get-started}

アセットマイクロサービスを使用したアセット処理は、デフォルト設定で事前設定され、システムで必要なデフォルトのレンディションが使用できるようになっています。 また、メタデータ抽出およびテキスト抽出の操作を使用できるようにします。 ユーザーはアセットのアップロードまたは更新を直ちに開始でき、デフォルトで基本処理を使用できます。

特定のレンディションの生成またはアセットの処理要件については、AEM管理者が追加の処理プロファイルを作 [!UICONTROL 成できます]。 ユーザーは、利用可能な1つ以上のプロファイルを特定のフォルダーに割り当てて、追加の処理を行うことができます。 例えば、Web、モバイル、タブレット固有のレンディションを生成する場合などです。 次のビデオでは、処理プロファイルの作成および適用方法 [!UICONTROL と、作成したレンディション] にアクセスする方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

既存のプロファイルを変更するには、アセットマイク [ロサービスの設定を参照してくださ](#configure-asset-microservices)い。
カスタム要件に固有のカスタム処理プロファイルを作成する場合は、他のシステムとの統合など、後処理のワークフ [ローを参照してください](#post-processing-workflows)。

## アセットマイクロサービスの設定 {#configure-asset-microservices}

アセットマイクロサービスを設定するには、管理者は、ツール/アセット/処理プロファ **[!UICONTROL イルの設定ユーザーインターフェイスを使用できます]**。

### デフォルト設定 {#default-config}

デフォルト設定では、標準の処理プロフ [!UICONTROL ァイル] のみが設定されます。 これは組み込み型のもので、変更できません。 アプリケーションが必要とするすべての処理を確実に行うために、常に実行されます。

![processing-profiles-standard](assets/processing-profiles-standard.png)

標準処理プロファイルには、次の処理設定が用意されています。

* アセットユーザーインターフェイスで使用される標準サムネール（48、140および319 px）
* 大きいプレビュー（Webレンディション — 1280 px）
* メタデータの抽出
* テキスト抽出

### サポートされているファイル形式 {#supported-file-formats}

アセットマイクロサービスは、レンディションの生成やメタデータの抽出の機能に関して、様々なファイル形式をサポートしています。 完全なリ [ストについては、「supported file formats](file-format-support.md) 」を参照してください。

### 追加の処理プロファイルの追加 {#processing-profiles}

追加の処理プロファイルは、 **[!UICONTROL Create]** （作成）アクションを使用して追加できます。

各処理プロファイル設定には、レンディションのリストが含まれます。 各レンディションに対して、次を指定できます。

* レンディション名
* レンディション形式（JPEG、PNGまたはGIFがサポートされます）
* レンディションの幅と高さ（ピクセル単位）（指定しない場合、元のレンディションの最大ピクセルサイズが想定されます）
* レンディション画質（JPEG用）(%)
* 含まれるMIMEタイプと除外されるMIMEタイプ。処理プロファイルが適用するアセットタイプを定義します。

![processing-profiles-adding](assets/processing-profiles-adding.png)

新しい処理プロファイルが保存されると、設定済みの処理プロファイルのリストに追加されます。 これらの処理プロファイルは、フォルダー階層内のフォルダーに適用して、アセットのアップロードやアセットのアップロードに有効にすることができます。

![processing-profiles-list](assets/processing-profiles-list.png)

#### レンディションの幅と高さ {#rendition-width-height}

レンディションの幅と高さの指定により、生成される出力画像の最大サイズが提供されます。 Asset Microserviceは、可能な限り大きなレンディションを生成しようとします。このレンディションの幅と高さは、それぞれ指定された幅と高さ以下です。 縦横比は維持され、元の縦横比と同じになります。

空の値は、アセット処理で元の画像のピクセル寸法を前提とすることを意味します。

#### MIMEタイプインクルージョンルール {#mime-type-inclusion-rules}

特定のMIMEタイプを持つアセットが処理されると、最初に、レンディションの指定で除外されたMIMEタイプの値に対してMIMEタイプが確認されます。 そのリストと一致する場合、この特定のレンディションはアセットに対して生成されません（「ブラックリスト」）。

それ以外の場合は、MIMEタイプが含まれているMIMEタイプと比較され、リストと一致する場合はレンディションが生成されます（「ホワイトリスト」）。

#### 特別FPOレンディション {#special-fpo-rendition}

処理プロファイルには、 [](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) Adobe Asset LinkをAdobe inDesignで使用してExperience ManagerからInDesignドキュメントにアセットへの直接リンクを配置する場合に使用する、特別な「FPOレンディション」を含めることができます。

処理プロファイルでアセットを有効にす [る必要がある場合は](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 、Adobe Asset linkのドキュメントを参照してください。

## アセットマイクロサービスを使用したアセットの処理 {#use-asset-microservices}

追加の処理プロファイルを作成したら、Experience Managerでそれらのフォルダー内でアップロードまたは更新されたアセットのアセット処理で使用するために、特定のフォルダーにそのプロファイルを適用する必要があります。 組み込みの標準処理プロファイルは常に実行されます。

フォルダーに適用された処理プロファイルを取得する方法は2つあります。

* 管理者は、ツール/アセット/処理プロファ **[!UICONTROL イルで処理プロファイルの定義を選択し]**、「プロファイルを **[!UICONTROL フォルダーに適用」アクションを使用できます]** 。 コンテンツブラウザーが開き、特定のフォルダーに移動したり、フォルダーを選択したり、プロファイルの適用を確認したりできます。
* ユーザーは、アセットユーザーインターフェイスでフォルダーを選択、「**[!UICONTROL プロパティ]**」アクションを使用してフォルダーのプロパティ画面を開きます。その後、「**[!UICONTROL 処理プロファイル]**」タブをクリックし、ドロップダウンでそのフォルダーに適した処理プロファイルを選択します。選択内容は、「**[!UICONTROL 保存して閉じる]**」アクションを実行すると保存されます。

>[!NOTE]
>
>特定のフォルダーに適用できる処理プロファイルは1つだけです。 さらにレンディションを生成する必要がある場合は、処理プロファイルにレンディション定義を追加できます。

処理プロファイルがフォルダーに適用された後、このフォルダーまたは任意のサブフォルダー内の新しいアセットがアップロード（または更新）されると、設定された追加の処理プロファイルを使用して処理されます。 この追加処理は、標準のデフォルトのプロファイルに加えて行われます。 フォルダーに複数のプロファイルを適用する場合、アップロードまたは更新されたアセットは、それぞれのプロファイルを使用して処理されます。

>[!NOTE]
>
>アセットがフォルダーにアップロードされると、Experience Managerは、そのフォルダーのプロパティで処理プロファイルを確認します。 何も適用されない場合は、適用された処理プロファイルが見つかるまでフォルダーツリー内で上に移動し、アセットに使用します。 つまり、フォルダーに適用された処理プロファイルはツリー全体で機能しますが、サブフォルダーに適用された別のプロファイルでオーバーライドできます。

ユーザーは、処理が完了した新しくアップロードしたアセットを開き、アセットのプレビューを開き、左側のパネルのレンディションビューをクリックして、処理が実際に行われたかどうかを確認で **[!UICONTROL きま]** す。 特定のアセットのタイプがMIMEタイプ包含ルールに一致する処理プロファイルの特定のレンディションが表示され、アクセス可能になる必要があります。

![追加レンディショ](assets/renditions-additional-renditions.png)*ン図：親フォルダーに適用された処理プロファイルによって生成された2つの追加レンディションの例*

## 後処理ワークフロー {#post-processing-workflows}

処理プロファイルを使用してアセットの追加処理が必要な場合は、追加の後処理ワークフローを設定に追加できます。 これにより、アセットマイクロサービスを使用して、設定可能な処理の上に、完全にカスタマイズされた処理を追加できます。

後処理ワークフローが設定されている場合、マイクロサービスの処理が終了すると、AEMによって自動的に実行されます。 ワークフローランチャーを手動で追加してトリガーする必要はありません。

次のような例があります。

* 独自仕様のファイル形式からレンディションを生成するJavaコードなど、アセットを処理するためのカスタムワークフロー手順。
* 統合を使用して、製品やプロセス情報など、外部システムからアセットにメタデータやプロパティを追加します。
* 外部サービスによる追加処理

後処理ワークフロー設定をExperience Managerに追加する手順は、次のとおりです。

* 1つ以上のワークフローモデルを作成しています。 「後処理ワークフローモデル」と呼びますが、通常のAEMワークフローモデルです。
* これらのモデルに特定のワークフロー手順を追加します。 これらの手順は、ワークフローモデルの設定に基づいてアセットに対して実行されます。
* そのようなモデルの最後のステップがステップでなければなり `DAM Update Asset Workflow Completed Process` ません。 これは、処理が終了し、アセットを処理済みとしてマーク（「新規」）できることをAEMが確認するために必要です。
* カスタムワークフローランナーサービスの設定を作成します。これにより、パス（フォルダーの場所）または正規表現で後処理ワークフローモデルの実行を設定できます

### 後処理ワークフローモデルの作成

後処理ワークフローモデルは、通常のAEMワークフローモデルです。 リポジトリの場所やアセットタイプごとに異なる処理が必要な場合は、異なる処理を作成してください。

処理手順は、ニーズに基づいて追加する必要があります。 サポートされているそのまま使用できる手順、およびカスタム実装のワークフロー手順を使用できます。

各後処理ワークフローの最後の手順は、である必要があります `DAM Update Asset Workflow Completed Process`。 これにより、アセットが「処理が完了しました」と正しくマークされます。

### 後処理ワークフローの実行の設定

アセットマイクロサービスの処理が終了した後に、システム内でアップロードまたは更新されたアセットに対して実行される後処理ワークフローモデルを設定するには、カスタムワークフローランナーサービスを設定する必要があります。

Custom Workflow Runnerサービス(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)はOSGiサービスで、設定には2つのオプションがあります。

* パス別の後処理ワークフロー(`postProcWorkflowsByPath`):様々なリポジトリパスに基づいて、複数のワークフローモデルを一覧表示できます。 パスとモデルはコロンで区切る必要があります。 単純なリポジトリパスがサポートされ、パス内のワークフローモデルにマッピングする必要があ `/var` ります。 For example: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* 式別の後処理ワークフロー(`postProcWorkflowsByExpression`):異なる正規表現に基づいて、複数のワークフローモデルを一覧表示できます。 式とモデルはコロンで区切る必要があります。 正規表現は、レンディションやファイルの1つではなく、アセットノードを直接指す必要があります。 For example: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>カスタムワークフローランナーの設定は、OSGiサービスの設定です。 OSGi設定の [デプロイ方法について詳しくは](/help/implementing/deploying/overview.md) 、Experience Managerへのデプロイを参照してください。
> OSGi webコンソールは、AEMのオンプレミスおよび管理サービスのデプロイメントとは異なり、クラウドサービスのデプロイメントでは直接使用できません。

後処理ワークフローで使用できる標準ワークフロー手順について詳しくは、開発者向けリファレンスの後処理ワークフローのワークフロー手順を参照して [ください](developer-reference-material-apis.md#post-processing-workflows-steps) 。
