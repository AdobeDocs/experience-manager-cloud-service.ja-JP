---
title: Connected Assets を使用した [!DNL Sites] での DAM アセットの共有
description: リモート [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] デプロイメントで使用可能なアセットを使用します。
contentOwner: AG
feature: アセット管理，Connected Assets，アセット配布，ユーザーとグループ
role: Administrator,Business Practitioner,Architect
exl-id: 2346f72d-a383-4202-849e-c5a91634617a
source-git-commit: 6163b150e014ad8449e6b64a191213f72daf4410
workflow-type: tm+mt
source-wordcount: '2966'
ht-degree: 78%

---

# Connected Assets を使用した [!DNL Experience Manager Sites] での DAM アセットの共有 {#use-connected-assets-to-share-dam-assets-in-aem-sites}

大規模企業では、Web サイトの作成に必要なインフラストラクチャが分散していることがあります。Web サイト作成機能と、それらの Web サイトの作成に使用されたデジタルアセットが、別のデプロイメントに格納されている場合もあります。1つの理由は、連携が必要な既存のデプロイメントを地理的に分散させることができます。 もう1つの理由は、異なる[!DNL Experience Manager]バージョンを含む異種インフラストラクチャを導く買収で、親会社が一緒に使用したい場合です。

Connected Assetsの機能は、[!DNL Experience Manager Sites]と[!DNL Experience Manager Assets]を統合することで、上記の使用例をサポートします。 ユーザーは、別の[!DNL Assets]デプロイメントのデジタルアセットを使用するWebページを[!DNL Sites]に作成できます。

## Connected Assets の概要 {#overview-of-connected-assets}

[!UICONTROL ページエディター]でページをターゲット先として編集する場合、作成者は、アセットのソースとして機能する別の [!DNL Assets] デプロイメントのアセットをシームレスに検索、参照および埋め込むことができます。管理者は、 [!DNL Sites] の機能を備える [!DNL Experience Manager] のデプロイメントと [!DNL Assets] の機能を備える [!DNL Experience Manager] 別のデプロイメントとの 1 回限りの統合を作成します。

[!DNL Sites] 作成者の場合、リモートアセットは読み取り専用のローカルアセットとして利用できます。この機能は、一度に少数のリモートアセットをシームレスに検索および使用できるようサポートします。多くのリモートアセットを [!DNL Sites] ローカルデプロイメントで一度に利用できるようにするには、リモートアセットを一括で移行することを検討します。

### 前提条件とサポートされているデプロイメント {#prerequisites}

この機能を使用または設定する前に、以下を確認してください。

* ユーザーがそれぞれのデプロイメント上で適切なユーザーグループに属している。
* [!DNL Adobe Experience Manager] のデプロイメントタイプでは、サポートされている条件の 1 つが満たされます。[!DNL Experience Manager] Cloud Serviceは [!DNL Assets] 6.5 [!DNL Experience Manager] で機能します。この機能が [!DNL Experience Manager] 6.5で機能する方法について詳しくは、 [6.5の [!DNL Experience Manager] Connected Assets [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html?lang=ja)を参照してください。

   |  | [!DNL Sites] as a [!DNL Cloud Service] | AMS 上の [!DNL Experience Manager] 6.5 [!DNL Sites] | [!DNL Experience Manager] 6.5 [!DNL Sites] On-Premise |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]として[!DNL Cloud Service]** | サポート対象 | サポート対象 | サポート対象 |
   | AMS 上の **[!DNL Experience Manager]6.5 [!DNL Assets]** | サポート対象 | サポート対象 | サポート対象 |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] On-Premise** | サポートなし | サポートなし | サポートなし |

### サポートされているファイル形式 {#mimetypes}

作成者は、コンテンツファインダーで画像や次のタイプのドキュメントを検索し、検索したアセットをページエディターで使用します。ドキュメントが `Download` コンポーネントに追加され、画像が `Image` コンポーネントに追加されます。作成者は、デフォルトの `Download` または `Image` コンポーネントを拡張するカスタム [!DNL Experience Manager] コンポーネントにもリモートアセットを追加します。サポートされる形式は以下の通りです。

* **画像形式**：[画像コンポーネント](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html)がサポートする形式。
* **ドキュメント形式**：詳しくは、[サポートされるドキュメント形式](file-format-support.md#document-formats)を参照してください。

### 関連するユーザーとグループ {#users-and-groups-involved}

この機能の設定や使用に関係する様々な役割と対応するユーザーグループについて、以下で説明します。ローカルスコープは、作成者が Web ページを作成する場合に使用します。リモートスコープは、必要なアセットをホストしている DAM デプロイメントで使用されます。[!DNL Sites] 作成者は、これらのリモートアセットを取得します。

| 役割 | 対象範囲 | ユーザーグループ | 手順のユーザーネーム | 要件 |
|------|--------|-----------|-----|----------|
| [!DNL Sites] administrator | ローカル | [!DNL Experience Manager] `administrators` | `admin` | [!DNL Experience Manager]を設定し、リモート [!DNL Assets] デプロイメントとの統合を設定します。 |
| DAM ユーザー | ローカル | `Authors` | `ksaner` | `/content/DAM/connectedassets/` の取得済みアセットを表示／複製するために使用されます。 |
| [!DNL Sites] 作成者 | ローカル | <ul><li>`Authors`（リモート DAM での読み取りアクセス権とローカル [!DNL Sites] での作成者アクセス権を持つ） </li> <li>ローカル [!DNL Sites] の `dam-users`</li></ul> | `ksaner` | エンドユーザーは、この統合を使用してコンテンツの速度を向上させる[!DNL Sites]作成者です。 作成者は、[!UICONTROL コンテンツファインダー]を使用し、ローカルWebページで必要な画像を使用して、リモートDAM内のアセットを検索および参照できます。 `ksaner` DAM ユーザーの資格情報が使用されます。 |
| [!DNL Assets] administrator | リモート | [!DNL Experience Manager] `administrators` | リモート [!DNL Experience Manager] の `admin` | クロスオリジンリソース共有（CORS）を設定します。 |
| DAM ユーザー | リモート | `Authors` | リモート [!DNL Experience Manager] の `ksaner` | リモート [!DNL Experience Manager] デプロイメントでの作成者の役割。[!UICONTROL コンテンツファインダー]を使用して Connected Assets 内のアセットを検索／参照します。 |
| DAM ディストリビューター（テクニカルユーザー） | リモート | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | リモート [!DNL Experience Manager] の `ksaner` | リモートデプロイメント上に存在するこのユーザーは、（[!DNL Sites] 作成者の役割ではなく）[!DNL Experience Manager] ローカルサーバーによって、[!DNL Sites] 作成者の代わりにリモートアセットを取得するために使用されます。この役割は、上の 2 つの `ksaner` の役割とは異なり、別のユーザーグループに属しています。 |
| [!DNL Sites] 技術ユーザー | ローカル | `connectedassets-sites-techaccts` | - | [!DNL Assets] デプロイメントで、[!DNL Sites] Web ページ内のアセットへの参照を検索できるようにします。 |

## [!DNL Sites] デプロイメントと [!DNL Assets] デプロイメント間の接続の設定 {#configure-a-connection-between-sites-and-assets-deployments}

[!DNL Experience Manager] 管理者はこの統合を作成できます。作成した統合を使用するうえで必要な権限は、ユーザーグループを通じて設定されます。ユーザーグループは、[!DNL Sites] デプロイメントおよび DAM デプロイメントで定義されます。

Connected Assets とローカル [!DNL Sites] の接続を構成するには、次の手順を実行します:

1. 既存の [!DNL Sites] デプロイメントにアクセスします。この [!DNL Sites] デプロイメントは Web ページのオーサリングに使用されます（例：`https://[sites_servername]:port`）。ページオーサリングは [!DNL Sites] デプロイメントでおこなわれるので、ページオーサリングの観点から [!DNL Sites] デプロイメントをローカルとして呼びます。

1. 既存の [!DNL Assets] デプロイメントにアクセスします。この [!DNL Assets] デプロイメントはデジタルアセットの管理に使用されます（例：`https://[assets_servername]:port`）。

1. ローカルスコープのユーザーと役割が、[!DNL Sites] デプロイメント上と AMS の [!DNL Assets] デプロイメント上に存在していることを確認します。[!DNL Assets] デプロイメント上でテクニカルユーザーを作成し、[関連するユーザーとグループ](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)で説明したユーザーグループに追加します。

1. `https://[sites_servername]:port` にあるローカルの [!DNL Sites] デプロイメントにアクセスします。**[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL Connected Assets 設定]**&#x200B;をクリックし、次の値を入力します。

   1. 構成の&#x200B;**[!UICONTROL タイトル]**。
   1. **[!UICONTROL リモート DAM URL]** は、`https://[assets_servername]:[port]` 形式で指定した [!DNL Assets] の場所の URL です。
   1. DAM ディストリビューター（テクニカルユーザー）の資格情報。
   1. 「**[!UICONTROL マウントポイント]**」フィールドに、[!DNL Experience Manager] が取得したアセットの格納先となるローカルの [!DNL Experience Manager] パスを入力します。例：`connectedassets` フォルダー。DAM から取得したアセットは、[!DNL Sites] デプロイメントのこのフォルダーに保存されます。
   1. **[!UICONTROL ローカルサイト URL]** は、 [!DNL Sites] デプロイメントの場所です。[!DNL Assets] デプロイメントは、この値を使用して、この [!DNL Sites] デプロイメントによって取得されたデジタルアセットへの参照を維持します。
   1. [!DNL Sites] 技術ユーザーの資格情報。
   1. **[!UICONTROL 元のバイナリ転送最適化しきい値]**&#x200B;フィールドの値は、元のアセット（レンディションを含む）を同期的に転送するかどうかを指定します。ファイルサイズが比較的小さいアセットは簡単に取得できますが、ファイルサイズが大きいアセットは非同期で同期するのが最適です。値は、ネットワークの機能に応じて異なります。
   1. データストアを使用してアセットを保存し、データストアが両方のデプロイメント間に共通のストレージである場合は、「**[!UICONTROL Connected Assets とデータストアを共有]**」を選択します。この場合、実際のアセットバイナリはデータストアで利用可能で、転送されないため、しきい値の制限は重要ではありません。

   ![Connected Assets 機能の典型的な設定](assets/connected-assets-typical-config.png)

   *図：Connected Assets 機能の典型的な設定*

1. [!DNL Assets]デプロイメント上の既存のデジタルアセットは既に処理され、レンディションが生成されます。これらのレンディションは、この機能を使用して取得されるので、レンディションを再生成する必要はありません。 レンディションの再生成を禁止するには、ワークフローランチャーを無効にします。（[!DNL Sites]）デプロイメントのランチャーの設定を調整して、`connectedassets` フォルダーを除外します（アセットはこのフォルダーに取得されます）。

   1. [!DNL Sites] デプロイメントで、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL ランチャー]**&#x200B;をクリックします。

   1. **[!UICONTROL DAM アセットの更新]**&#x200B;および **[!UICONTROL DAM メタデータの書き戻し]**&#x200B;ワークフローを含むランチャーを検索します。

   1. ワークフローランチャーを選択し、アクションバーの「**[!UICONTROL プロパティ]**」をクリックします。

   1. [!UICONTROL プロパティ]ウィザードで、「**[!UICONTROL パス]**」フィールドを次のマッピングに従って変更し、マウントポイント **[!UICONTROL connectedassets]** が除外されるように正規表現を更新します。

   | 前 | 後 |
   | ------ | ------------ |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >作成者がアセットを取得する際、リモート デプロイメントで使用可能なすべてのレンディションが取得されます。取得したアセットのレンディションをさらに作成したい場合は、この設定手順をスキップしてください。[!UICONTROL DAM アセットの更新]ワークフローが開始され、追加のレンディションが作成されます。これらのレンディションは、ローカルの [!DNL Sites] デプロイメントでのみ使用でき、リモート DAM デプロイメントでは使用できません。

1. [!DNL Assets] デプロイメントの CORS 構成で、許可されたオリジンとして [!DNL Sites] デプロイメントを追加します。詳しくは、「[オリジン間リソース共有について（CORS）](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ja)」を参照してください。

1. [同じサイトcookieサポート](/help/security/same-site-cookie-support.md)を設定します。

設定済みの[!DNL Sites]デプロイメントと[!DNL Assets]デプロイメントの間の接続を確認できます。

![Connected Assetsの設定済み接続テ [!DNL Sites]](assets/connected-assets-multiple-config.png)
*スト図：設定済みのConnected Assetsの接続テスト [!DNL Sites]。*

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## [!DNL Sites] デプロイメントと [!DNL Dynamic Media] デプロイメント間の接続の設定 {#sites-dynamic-media-connected-assets}

[!DNL Sites]デプロイメントと[!DNL Dynamic Media]デプロイメントの間の接続を設定して、Webページの作成者がWebページで[!DNL Dynamic Media]イメージを使用できるようにすることができます。 Webページをオーサリングする際に、リモートアセットとリモート[!DNL Dynamic Media]デプロイメントを使用する経験は同じです。 これにより、Connected Assetsの機能（スマート切り抜きや画像プリセットなど）を使用して[!DNL Dynamic Media]機能を活用できます。

この接続を設定するには、次の手順に従います。

1. 上記の説明に従って、Connected Assets設定を作成します。 機能を設定する際に、「**[!UICONTROL Dynamic Media Connected Assetsのオリジナルのレンディションを取得]**」オプションを選択します。

1. ローカル[!DNL Sites]およびリモート[!DNL Assets]デプロイメントに[!DNL Dynamic Media]を設定します。 [configure [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)の指示に従います。

   * すべての設定で同じ会社名を使用します。
   * ローカルの[!DNL Sites]の[!UICONTROL Dynamic Media同期モード]で、「**[!UICONTROL デフォルトで無効]**」を選択します。 [!DNL Sites]デプロイメントでは、[!DNL Dynamic Media]アカウントに対する読み取り専用アクセスのみ必要です。
   * ローカルの[!DNL Sites]の「**[!UICONTROL アセットを公開]**」オプションで、「**[!UICONTROL 選択的公開]**」を選択します。 「**[!UICONTROL すべてのコンテンツを同期]**」は選択しないでください。
   * リモート[!DNL Assets]デプロイメントの[!UICONTROL Dynamic Media同期モード]で、「**[!UICONTROL デフォルトで有効]**」を選択します。

1. 画像コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media)で[[!DNL Dynamic Media] サポートを有効にします。 この機能を使用すると、ローカルの[!DNL Sites]デプロイメント上のWebページの作成者が[!DNL Dynamic Media]画像を使用する場合、デフォルトの[画像コンポーネント](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html)に[!DNL Dynamic Media]画像を表示できます。

## リモートアセットの使用 {#use-remote-assets}

Web サイト作成者は、コンテンツファインダーを使用して DAM デプロイメントに接続します。Web サイト作成者は、コンポーネント内のリモートアセットを参照、検索、ドラッグできます。リモート DAM への認証をおこなえるよう、管理者から提供された DAM ユーザーの資格情報を手元に用意してください。

作成者は、ローカル DAM デプロイメントで利用可能なアセットとリモート DAM デプロイメントで利用可能なアセットを、単一の Web ページ内で使用できます。コンテンツファインダーを使用すれば、ローカル DAM の検索とリモート DAM の検索を切り替えることができます。

ローカルの [!DNL Sites] デプロイメントで使用できる、完全に対応するタグ（同じ分類階層を持つ）を持つリモートアセットのタグのみが取得されます。その他のタグは破棄されます。作成者は、全文検索が提供されるので、リモート [!DNL Experience Manager] デプロイメントに存在するすべてのタグを使用して、リモートアセットを検索できます。

### 使用手順 {#walk-through-of-usage}

上記のセットアップを使用してオーサリングエクスペリエンスを試し、機能を理解してください。リモート DAM デプロイメントで、選択したドキュメントまたは画像を使用します。

1. リモートデプロイメントの [!DNL Assets] インターフェイスに移動するには、[!DNL Experience Manager] Workspace から **[!UICONTROL Assets]**／**[!UICONTROL ファイル]**&#x200B;にアクセスします。または、ブラウザーで `https://[assets_servername_ams]:[port]/assets.html/content/dam` にアクセスします。選択したアセットをアップロードします。
1. [!DNL Sites] デプロイメントの右上隅にあるプロファイルアクティベーターで、「**[!UICONTROL 別のユーザーとして実行する]**」をクリックします。ユーザー名として `ksaner` を入力し、提供されたオプションを選択し、「**[!UICONTROL OK]**」をクリックします。
1. **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**&#x200B;で`We.Retail`Webサイトページを開きます。 ページを編集します。または、ブラウザーで `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` にアクセスしてページを編集します。

   ページの左上隅にある「**[!UICONTROL サイドパネルを切り替え]**」をクリックします。

1. 「[!UICONTROL Assets]」タブを開き、「**[!UICONTROL Connected Assets へのログイン]**」をクリックします。
1. 資格情報（ユーザー名：`ksaner`、パスワード：`password`）を入力します。このユーザーには、両方の [!DNL Experience Manager] デプロイメントのオーサリング権限があります。
1. DAM に追加したアセットを検索します。リモートアセットは左側のパネルに表示されます。画像またはドキュメントでフィルタリングしてから、サポートされているドキュメントのタイプでさらにフィルタリングします。`Image` コンポーネント上の画像と `Download` コンポーネント上のドキュメントをドラッグします。

   ローカル [!DNL Sites] デプロイメントでは、取得されたアセットは読み取り専用です。[!DNL Sites] コンポーネントが提供するオプションを使用して、取得したアセットを編集できます。コンポーネントによる編集は非破壊的です。

   ![リモート DAM でアセットを検索するときにドキュメントタイプと画像をフィルタリングするオプション](assets/filetypes_filter_connected_assets.png)

   *図：リモート DAM でアセットを検索するときにドキュメントタイプと画像をフィルタリングするオプション*

1. アセットが非同期で取得され、取得タスクが失敗した場合、サイト作成者に通知されます。オーサリング中またはオーサリング後でも、作成者は[非同期ジョブ](/help/operations/asynchronous-jobs.md)ユーザーインターフェイスで取得タスクやエラーについての詳細情報を確認できます。

   ![バックグラウンドで発生するアセットの非同期取得に関する通知。](assets/assets_async_transfer_fails.png)

   *図：バックグラウンドで発生するアセットの非同期取得に関する通知。*

1. ページを公開すると、ページで使用されているアセットの完全なリストが [!DNL Experience Manager] に表示されます。公開時にリモートアセットが正常に取得されることを確認します。取得した各アセットのステータスを確認するには、[非同期ジョブ](/help/operations/asynchronous-jobs.md)ユーザーインターフェイスをご覧ください。

   >[!NOTE]
   >
   >1 つ以上のリモートアセットが取得されない場合でも、ページは公開されます。リモートアセットを使用するコンポーネントは空で公開されます。[!DNL Experience Manager] 通知領域では、非同期ジョブページに表示されるエラーの通知を確認できます。

>[!CAUTION]
>
>Web ページで使用すると、取得したリモートアセットは、ローカルフォルダーへのアクセス権限を持つユーザーが検索および使用できます。取得したアセットは、ローカルフォルダー（上のウォークスルーの `connectedassets`）に保存されます。これらのアセットは、ローカルリポジトリでも[!UICONTROL コンテンツファインダー]経由で検索および表示できます。

取得されたアセットは他のローカルアセットと同じように使用できます。ただし、関連するメタデータは編集できません。

### Web ページ間でのアセットの使用の確認 {#asset-usage-references}

[!DNL Experience Manager] DAM ユーザーは、アセットへのすべての参照を確認できます。リモートの [!DNL Sites] および複合アセット内のアセットの使用状況を理解し、管理するのに役立ちます。[!DNL Experience Manager Sites]デプロイメントのWebページの作成者の多くは、別のWebページのリモートDAMでアセットを使用できます。 アセット管理を単純化し、参照が壊れないようにするには、DAM ユーザーはローカルおよびリモートの Web ページ全体でのアセットの使用を確認することが重要です。アセットの[!UICONTROL プロパティ]ページの「[!UICONTROL 参照]」タブは、アセットのローカル参照とリモート参照をリストします。

[!DNL Assets] デプロイメントで参照を表示および管理するには、次の手順に従います。

1. [!DNL Assets] コンソールでアセットを選択し、ツールバーの「**[!UICONTROL プロパティ]**」をクリックします。
1. 「**[!UICONTROL 参照]**」タブをクリックします。[!DNL Assets] デプロイメントでのアセットの使用については、「**[!UICONTROL ローカルの参照]**」を参照してください。Connected Assets 機能を使用してアセットが取得された [!DNL Sites] デプロイメント上のアセットの使用については、「[!UICONTROL リモートの参照]」を参照してください。

   ![アセットプロパティページのリモート参照](assets/connected-assets-remote-reference.png)

1. [!DNL Sites]ページの参照には、各ローカル[!DNL Sites]の参照の合計数が表示されます。 すべての参照を見つけて、参照の総数を表示するのは時間がかかる場合があります。
1. 参照のリストはインタラクティブで、DAM ユーザーは参照をクリックして参照ページを開くことができます。何らかの理由でリモート参照を取得できない場合は、失敗の通知が表示されます。
1. ユーザーはアセットを移動または削除できます。アセットを移動または削除すると、選択したすべてのアセット／フォルダーの参照の合計数が警告ダイアログに表示されます。参照がまだ表示されていないアセットを削除すると、警告ダイアログが表示されます。

   ![強制削除警告](assets/delete-referenced-asset.png)

## 制限事項とベストプラクティス {#tip-and-limitations}

* アセットの使用状況に関するインサイトを取得するには、[!DNL Sites] インスタンスで[アセットインサイト](/help/assets/assets-insights.md)機能を設定します。

### 権限とアセット管理 {#permissions-and-managing-assets}

* ローカルアセットは、リモートデプロイメントの元のアセットと同期されません。DAM デプロイメント上での編集、削除または権限の失効は、ローカル側には一切伝播されません。
* ローカルアセットは読み取り専用のコピーです。[!DNL Experience Manager] コンポーネントは、アセットに対して非破壊編集をおこないます。その他のいかなる編集もできません。
* ローカルで取得されたアセットは、オーサリング用途でのみ使用できます。アセット更新ワークフローの適用やメタデータの編集はおこなえません。
* [!DNL Sites]ページで[!DNL Dynamic Media]を使用する場合、元のアセットを取得してローカルデプロイメントに保存することはできません。 `dam:Asset`ノード、メタデータ、および[!DNL Assets]デプロイメントで生成されたレンディションは、すべて[!DNL Sites]デプロイメントで取得されます。
* 画像とリストに表示されるドキュメント形式のみがサポートされます。[!DNL Content Fragments] およびはサ [!DNL Experience Fragments] ポートされていません。
* Adobe [!DNL Experience Manager] はメタデータスキーマを取得しません。つまり、取得されたすべてのメタデータが表示されない可能性があります。[!DNL Sites]デプロイメント上でスキーマが個別に更新されると、すべてのメタデータプロパティが表示されます。
* [!DNL Sites] 作成者は全員、リモート DAM デプロイメントへのアクセス権限を持っていなくても、取得されたコピーに対する読み取り権限を持ちます。
* 統合をカスタマイズするための API サポートはありません。
* この機能は、リモートアセットのシームレスな検索および使用をサポートします。多くのリモートアセットをローカルデプロイメントで一度に利用できるようにするには、リモートアセットの移行を検討します。
* リモートアセットを[!UICONTROL ページプロパティ]ユーザーインターフェイスのページサムネールとして使用することはできません。Web ページのサムネールは、[!UICONTROL ページプロパティ]ユーザインターフェイスの[!UICONTROL サムネール]から、「[!UICONTROL 画像を選択]」をクリックして設定できます。

### セットアップとライセンス {#setup-licensing}

* [!DNL Adobe Managed Services] での [!DNL Assets] のデプロイメントはサポートされています。
* [!DNL Sites] は一度に 1 つのリポジトリに接続できます。[!DNL Assets]
* リモートリポジトリとして動作する[!DNL Assets]のライセンスが必要です。
* ローカルオーサリングデプロイメントとして動作する[!DNL Sites]の1つ以上のライセンスが必要です。

### 使用方法 {#usage}

* ユーザーは、オーサリング時にリモートアセットを検索し、ローカルページにドラッグできます。その他の機能はサポートされていません。
* 取得操作は 5 秒でタイムアウトします。アセット取得時、問題が発生する場合があります（ネットワークに問題がある場合など）。作成者は、再試行をおこない、リモートアセットを[!UICONTROL コンテンツファインダー]から[!UICONTROL ページエディター]にドラッグ＆ドロップできます。
* 取得されたアセットに対しては、単純な非破壊編集と、 `Image` コンポーネント経由でサポートされている編集をおこなえます。アセットは読み取り専用です。
* アセットを再取得する唯一の方法は、アセットをページにドラッグすることです。アセットを再取得して更新するための API サポートなどの手段はありません。
* アセットが DAM から廃止されても、それらは引き続き [!DNL Sites] ページで使用されます。
* アセットのリモート参照エントリは非同期で取得されます。 参照と合計数はリアルタイムではなく、DAMユーザーが参照を表示している間に[!DNL Sites]作成者がアセットを使用すると、多少の違いが生じる場合があります。 DAM ユーザーは、ページを更新して数分後に再試行し、合計数を取得できます。

## 問題のトラブルシューティング {#troubleshoot}

一般的なエラーのトラブルシューティングをおこなうには、次の手順に従います。

* [!UICONTROL コンテンツファインダー]からリモートアセットを検索できない場合は、必要な役割と権限が設定されていることを確認してください。

* リモートDAMから取得されたアセットは、1つ以上の理由でWebページに公開されない場合があります。 リモートサーバーに存在しない、取得する適切なアクセス許可がない、ネットワーク障害、などが原因の可能性があります。アセットがリモート DAM から削除されていないことを確認してください。適切な権限が設定され、前提条件が満たされていることを確認します。アセットをページに追加し直して、再公開してください。アセット取得時のエラーについては、[非同期ジョブのリスト](/help/operations/asynchronous-jobs.md)を確認してください。

* ローカルの[!DNL Sites]デプロイメントからリモートDAMデプロイメントにアクセスできない場合は、クロスサイトcookieが許可され、[同じサイトcookieサポート](/help/security/same-site-cookie-support.md)が設定されていることを確認します。 クロスサイトcookieがブロックされた場合、[!DNL Experience Manager]のデプロイメントは認証されない可能性があります。 例えば、匿名モードの [!DNL Google Chrome] は、サードパーティ cookie をブロックする可能性があります。[!DNL Chrome]ブラウザーでCookieを許可するには、アドレスバーの「目」アイコンをクリックし、**Site Not Working** / **Blocked**&#x200B;に移動して、リモートDAM URLを選択し、ログイントークンCookieを許可します。 または、[サードパーティCookieを有効にする方法](https://support.google.com/chrome/answer/95647)を参照してください。

   ![匿名モードでのChromeブラウザーのCookieエラー](assets/chrome-cookies-incognito-dialog.png)

* リモート参照が取得されず、エラーメッセージが表示される場合は、[!DNL Sites]デプロイメントが使用可能かどうかを確認し、ネットワーク接続の問題がないか確認します。 確認のために後で再試行します。[!DNL Assets] デプロイメントは、 [!DNL Sites] デプロイメントとの接続の確立を 2 回試み、失敗を報告します。

   ![アセットのリモート参照の取得の失敗](assets/reference-report-failure.png)
