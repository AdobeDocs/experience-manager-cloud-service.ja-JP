---
title: アセット処理のためのアセットマイクロサービスの設定と使用
description: クラウドネイティブなアセットマイクロサービスを設定および使用してアセットを規模に応じて処理する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 367456bfad25a83a36ffe45e2d6092367740cd92
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 95%

---


# アセットマイクロサービスの基本 {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

アセットマイクロサービスは、クラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。アドビは、様々なアセットタイプや処理オプションを最適に処理するためのサービスを管理します。

アセット処理は、**[!UICONTROL 処理プロファイル]**&#x200B;の設定に依存してします。処理プロファイルには、デフォルトの設定が用意されていますが、管理者がより具体的なアセット処理設定を追加することもできます。管理者は、オプションのカスタマイズを含む、後処理ワークフローの設定を作成および管理できます。ワークフローのカスタマイズでは、拡張機能と完全なカスタマイズが可能です。

アセットマイクロサービスを使用すると、以前のバージョンの Experience Manager よりも多くの形式をカバーする[様々なファイルタイプ](/help/assets/file-format-support.md)を追加設定なしで処理できます。例えば、以前は ImageMagick などのサードパーティソリューションが必要だった PSD 形式と PSB 形式を、サムネール抽出できるようになりました。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![アセット処理の高レベル表示](assets/asset-microservices-flow.png "アセット処理の高レベル表示")

>[!NOTE]
>
> ここで説明するアセット処理は、以前のバージョンの Experience Manager に存在する `DAM Update Asset` ワークフローモデルに代わるものです。標準的なレンディション生成とメタデータ関連のステップのほとんどは、アセットマイクロサービスの処理に置き換わり、残りのステップは後処理ワークフロー設定に置き換えることができます。

## アセット処理の基本 {#get-started}

アセットマイクロサービスを使用したアセット処理は、デフォルト設定で事前設定されており、システムに必要なデフォルトのレンディションは確実に使用できるようになっています。また、メタデータ抽出およびテキスト抽出操作も使用できるようになっています。ユーザーはアセットのアップロードや更新を直ちに開始でき、基本的な処理がデフォルトで利用可能です。

レンディション生成やアセット処理に関する特定の要件に応じて、AEM 管理者が追加の[!UICONTROL 処理プロファイル]を作成できます。ユーザーは、使用可能な 1 つ以上のプロファイルを特定のフォルダーに割り当てて、追加の処理を完了することができます。例えば、Web、モバイル、タブレット固有のレンディションを生成する場合などです。次のビデオでは、[!UICONTROL 処理プロファイル]の作成および適用方法と、作成したレンディションへのアクセス方法を示しています。

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

既存のプロファイルを変更するには、[アセットマイクロサービスの設定](#configure-asset-microservices)を参照してください。
他のシステムとの統合などのカスタム要件に特化したカスタム処理プロファイルを作成する場合は、[後処理ワークフロー](#post-processing-workflows)を参照してください。

## アセットマイクロサービスの設定 {#configure-asset-microservices}

管理者がアセットマイクロサービスを設定するには、**[!UICONTROL ツール／アセット／処理プロファイル]**&#x200B;を選択して、設定ユーザーインターフェイスを使用できます。

### デフォルト設定 {#default-config}

デフォルト設定では、標準の処理プロファイルのみ設定されています。標準の処理プロファイルはユーザーインターフェイスに表示されず、変更することはできません。アップロードされたアセットは常に処理されます。標準の処理プロファイルを使用すると、Experience Manager で必要なあらゆる基本処理をすべてのアセットに対して実行できます。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png) -->

標準の処理プロファイルには、次の処理設定が用意されています。

* アセットユーザーインターフェイスで使用される標準サムネール（48、140、319 px）
* 大きなプレビュー（Web レンディション - 1280 px）
* メタデータ抽出
* テキスト抽出

### サポートされているファイル形式 {#supported-file-formats}

アセットマイクロサービスでは、レンディション生成やメタデータ抽出の機能に関して、様々なファイル形式をサポートしています。そのリストについては、[サポートされているファイル形式](file-format-support.md)を参照してください。

### 処理プロファイルの追加 {#processing-profiles}

追加の処理プロファイルは、**[!UICONTROL 作成]**&#x200B;アクションを使用して追加できます。

それぞれの処理プロファイル設定には、レンディションのリストが含まれています。レンディションごとに、以下を指定できます。

* レンディション名。
* JPEG、PNG、GIF など、サポートされるレンディション形式。
* レンディションの幅と高さをピクセル単位で指定します。指定しなかった場合は、元の画像の最大ピクセルサイズが使用されます。
* JPEG のレンディションの画質（％単位）。
* プロファイルの適用性を定義する、包含および除外 MIME タイプ。

![processing-profiles-adding](assets/processing-profiles-adding.png)

新しい処理プロファイルを作成して保存すると、設定済みの処理リストのプロファイルに追加されます。これらの処理プロファイルをフォルダー階層のフォルダーに適用して、アセットのアップロードやアセットの処理に対して有効にすることができます。

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) -->

#### レンディションの幅と高さ {#rendition-width-height}

レンディションの幅と高さの仕様には、生成される出力画像の最大サイズを指定します。アセットマイクロサービスでは、レンディションの幅と高さがそれぞれ指定の幅と高さを超えない範囲で、可能な限り大きなレンディションを生成しようとします。縦横比は維持され、元の縦横比と同じになります。

値が空の場合は、アセット処理で元の画像のピクセルサイズを前提とすることになります。

#### MIME タイプ包含ルール {#mime-type-inclusion-rules}

特定の MIME タイプのアセットが処理される際は、まず、その MIME タイプがレンディション仕様の除外 MIME タイプの値と照合されます。そのリストと一致する場合、この特定のレンディションはアセットに対して生成されません（「ブラックリストへの登録」）。

それ以外の場合は、MIME タイプが包含 MIME タイプと照合され、リストと一致する場合は、そのレンディションが生成されます（「ホワイトリストへの登録」）。

#### 特別な FPO レンディション {#special-fpo-rendition}

AEM の大きなサイズのアセットを Adobe InDesign ドキュメントに配置する場合、クリエイティブプロフェッショナルは、[アセットを配置](https://helpx.adobe.com/jp/indesign/using/placing-graphics.html)してからかなりの時間待つ必要があります。一方、ユーザーは InDesign の使用をブロックされます。これにより、クリエイティブの流れが中断され、ユーザーエクスペリエンスに悪影響が出ます。InDesign ドキュメントでは、小さいサイズのレンディションを一時的に配置して、最初に配置することができます。この作業は、後でオンデマンドにより、フル解像度のアセットに置き換えることができます。Experience Manager には、配置専用（FPO）のレンディションが用意されています。これらの FPO レンディションは、ファイルサイズは小さいですが、縦横比は同じです。

処理プロファイルには、FPO（配置専用）レンディションを含めることができます。これを処理プロファイルで有効にする必要がある場合は、Adobe Asset Link の[ドキュメント](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)を参照してください。詳しくは、[Adobe Asset Link の完全なドキュメント](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)を参照してください。

## アセットマイクロサービスを使用したアセットの処理 {#use-asset-microservices}

追加のカスタム処理プロファイルを作成し、Experience Manager の特定のフォルダーに適用して、これらのフォルダーにアップロードまたは更新されたアセットを処理します。デフォルトの組み込み標準処理プロファイルは常に実行されますが、ユーザーインターフェイスには表示されません。カスタムアセットを追加する場合、プロファイルされたアセットは両方のプロファイルを使用して処理されます。

処理プロファイルをフォルダーに適用する方法は次の 2 通りあります。

* 管理者が、**[!UICONTROL ツール／Assets／処理プロファイル]**&#x200B;で処理プロファイルの定義を選択し、「**[!UICONTROL プロファイルをフォルダーに適用]**」アクションを使用します。コンテンツブラウザーが開き、そこで特定のフォルダーに移動したり、フォルダーを選択したり、プロファイルの適用を確定したりできます。
* ユーザーが Assets ユーザーインターフェイスでフォルダーを選択し、「**[!UICONTROL プロパティ]**」アクションを使用してフォルダーのプロパティ画面を開き、「**[!UICONTROL 処理プロファイル]**」タブのドロップダウンでそのフォルダーに適した処理プロファイルを選択します。選択内容は、「**[!UICONTROL 保存して閉じる]**」アクションの実行時に保存されます。

>[!NOTE]
>
>特定のフォルダーに適用できる処理プロファイルは 1 つだけです。さらにレンディションを生成する必要がある場合は、処理プロファイルにレンディション定義を追加します。

処理プロファイルがフォルダーに適用されると、このフォルダーまたはその任意のサブフォルダー内でアップロード（または更新）された新しいアセットはすべて、設定された追加の処理プロファイルを使用して処理されます。この追加処理は、標準のデフォルトプロファイルによる処理に加えておこなわれます。フォルダーに複数のプロファイルを適用する場合、アップロードまたは更新されたアセットは、それぞれのプロファイルを使用して処理されます。

>[!NOTE]
>
>アセットがフォルダーにアップロードされると、Adobe Experience Manager は、そのフォルダーのプロパティで処理プロファイルを確認します。何も適用されていない場合は、適用された処理プロファイルが見つかるまでフォルダーツリー内を上に移動し、見つかった処理プロファイルをアセットに使用します。つまり、フォルダーに適用された処理プロファイルはツリー全体で機能しますが、サブフォルダーに適用された別のプロファイルでオーバーライドすることができます。

ユーザーは、新しくアップロードされ処理が完了したアセットのプレビューを開き、左側のパネルの&#x200B;**[!UICONTROL レンディション]**&#x200B;表示をクリックして、処理が実際におこなわれたかどうかを確認できます。特定のアセットのタイプが MIME タイプ包含ルールと一致する処理プロファイルの特定のレンディションが表示され、アクセス可能になります。

![additional-renditions](assets/renditions-additional-renditions.png)
*図：親フォルダーに適用された処理プロファイルで生成された 2 つの追加レンディションの例*

## 後処理ワークフロー {#post-processing-workflows}

処理プロファイルを使用して実現できない追加のアセット処理が必要な状況では、追加の後処理ワークフローを設定に追加できます。これにより、アセットマイクロサービスを使用して、設定可能な処理の上に完全にカスタマイズされた処理を追加できます。

後処理ワークフローが設定されている場合は、マイクロサービスの処理が終了した後に、AEM で後処理ワークフローが自動的に実行されます。ワークフローランチャーを手動で追加してトリガーする必要はありません。

次のような例があります。

* アセットを処理するためのカスタムワークフローステップ（独自のファイル形式からレンディションを生成する Java コードなど）。
* 外部システムから提供されるアセット（製品やプロセスの情報など）にメタデータやプロパティを追加するための統合機能。
* 外部サービスによる追加処理

後処理ワークフロー設定を Adobe Experience Manager に追加する作業は、次の手順で構成されます。

* 1 つ以上のワークフローモデルの作成。これらは「後処理ワークフローモデル」と呼ばれますが、通常の AEM ワークフローモデルです。
* これらのモデルに特定のワークフローステップを追加する。これらのステップは、ワークフローモデルの設定に基づいたアセットに対する処理の実行になります。
* このようなモデルの最後のステップは、`DAM Update Asset Workflow Completed Process` ステップでなければなりません。これは、処理が終了したことを AEM が把握し、アセットを処理済み（「新規」）としてマークできるようにするために必要になります。
* Custom Workflow Runner サービスの設定の作成。パス（フォルダーの場所）または正規表現で後処理ワークフローモデルの実行を設定できます

### 後処理ワークフローモデルの作成 {#create-post-processing-workflow-models}

後処理ワークフローモデルは、通常の AEM ワークフローモデルです。リポジトリの場所やアセットタイプごとに異なる処理が必要な場合は、異なるモデルを作成します。

処理ステップは、ニーズに応じて追加する必要があります。サポートされているステップのほか、カスタム実装されたワークフローステップも使用できます。

各後処理ワークフローの最後の手順が `DAM Update Asset Workflow Completed Process` であることを確認します。最後の手順は、アセットの処理が完了したことを Experience Manager が確実に把握できるようにするのに役立ちます。

### 後処理ワークフローの実行の設定 {#configure-post-processing-workflow-execution}

アセットマイクロサービスの処理が終了した後に、システム内でアップロードまたは更新されたアセットに対して実行する後処理ワークフローモデルを設定するには、Custom Workflow Runner サービスを設定する必要があります。

Custom Workflow Runner サービス（`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`）は OSGi サービスで、次の 2 つの設定オプションを提供します。

* パスによる後処理ワークフローの設定（`postProcWorkflowsByPath`）：異なるリポジトリパスに基づいて、複数のワークフローモデルをリストアップできます。パスとモデルはコロンで区切る必要があります。単純なリポジトリパスがサポートされており、`/var` パス内のワークフローモデルにマッピングされる必要があります。例：`/content/dam/my-brand:/var/workflow/models/my-workflow`
* 式による後処理ワークフローの設定（`postProcWorkflowsByExpression`）：異なる正規表現に基づいて、複数のワークフローモデルをリストアップできます。式とモデルはコロンで区切る必要があります。正規表現は、レンディションやファイルの 1 つではなく、アセットノードを直接指すものでなければなりません。例：`/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`

>[!NOTE]
>
>Custom Workflow Runner の設定は、OSGi サービスの設定になります。OSGi 設定のデプロイ方法については、[Adobe Experience Manager へのデプロイ](/help/implementing/deploying/overview.md)を参照してください。
> OSGi Web コンソールは、AEM の On-Premise デプロイメントや Managed Services デプロイメントとは異なり、Cloud Service デプロイメントでは直接使用できません。

後処理ワークフローで使用できる標準ワークフローステップについて詳しくは、開発者向けリファレンスの[後処理ワークフローのワークフローステップ](developer-reference-material-apis.md#post-processing-workflows-steps)を参照してください。

## Best practices and limitations {#best-practices-limitations-tips}

* ワークフローをデザインする際は、あらゆる種類のレンディションに対するニーズを考慮します。 レンディションが今後必要になることが予測されない場合は、ワークフローからレンディションの作成手順を削除します。 レンディションは、その後一括で削除することはできません。 を長時間使用した後、不要なレンディションを使用すると、ストレージ領域が大量に消費される場合があり [!DNL Experience Manager]ます。 個々のアセットについて、レンディションをユーザインターフェイスから手動で削除できます。 複数のアセットの場合は、特定のレンディションを削除す [!DNL Experience Manager] るようにカスタマイズするか、アセットを削除して再びアップロードできます。
