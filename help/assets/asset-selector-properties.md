---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] のアセットセレクター'
description: アセットセレクターを使用して、アプリケーション内のアセットのメタデータとレンディションを検索および取得します。
role: Admin, User
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: 97a432270c0063d16f2144d76beb437f7af2895a
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 98%

---

# アセットセレクターのプロパティ {#asset-selector-properties}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

アセットセレクターのプロパティを使用して、アセットセレクターのレンダリング方法をカスタマイズできます。次の表に、アセットセレクターをカスタマイズして使用するために利用できるプロパティを示します。

| Property | タイプ | 必須 | デフォルト | 説明 |
|---|---|---|---|---|
| *rail* | ブール値 | いいえ | False | `true` とマークされている場合、アセットセレクターは左側のパネルビューにレンダリングされます。`false` とマークされている場合、アセットセレクターはモーダルビューにレンダリングされます。 |
| *imsOrg* | 文字列 | はい | | [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] を組織にプロビジョニングする場合に割り当てられる Adobe Identity Management System（IMS）の ID です。`imsOrg` キーは、アクセスしようとしている組織が Adobe IMS 内にあるかどうかを認証するために必要です。 |
| *imsToken* | 文字列 | いいえ | | 認証に使用される IMS ベアラートークンです。統合に [!DNL Adobe] アプリケーションを使用している場合、`imsToken` は必須です。 |
| *apiKey* | 文字列 | いいえ | | AEM Discovery サービスへのアクセスに使用する API キーです。[!DNL Adobe] アプリケーション統合を使用している場合、`apiKey` は必須です。 |
| *filterSchema* | 配列 | いいえ | | フィルタープロパティの設定に使用するモデルです。これは、アセットセレクターで特定のフィルターオプションを制限する場合に便利です。 |
| *filterFormProps* | オブジェクト | いいえ | | 検索を絞り込むために使用する必要があるフィルタープロパティを指定します。（例：MIME タイプの JPG、PNG、GIF） |
| *selectedAssets* | 配列 `<Object>` | いいえ |                 | アセットセレクターがレンダリングされる際に、選択したアセットを指定します。アセットの ID プロパティを含むオブジェクトの配列が必要です。（例：`[{id: 'urn:234}, {id: 'urn:555'}]`）アセットは、現在のディレクトリで使用できる必要があります。別のディレクトリを使用する必要がある場合は、`path` プロパティの値も指定します。 |
| *acvConfig* | オブジェクト | いいえ | | デフォルトを上書きするカスタム設定が含まれているオブジェクトを含む、アセットコレクション表示プロパティです。また、このプロパティは、アセットビューアのパネルビューを有効にするために `rail` プロパティと共にに使用されます。 |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | いいえ |                 | OOTB 翻訳がアプリケーションのニーズを満たさない場合は、独自のローカライズされたカスタム値を `i18nSymbols` プロップ経由で渡すことができるインターフェイスを表示できます。このインターフェイスを介して値を渡すと、提供されたデフォルトの翻訳が上書きされ、代わりに独自の翻訳が使用されます。上書きを実行するには、上書きしたい `i18nSymbols` のキーに有効な[メッセージ記述子](https://formatjs.io/docs/react-intl/api/#message-descriptor)オブジェクトを渡す必要があります。 |
| *intl* | オブジェクト | いいえ | | アセットセレクターはデフォルトの OOTB 翻訳を提供します。`intl.locale` プロップを介して有効なロケール文字列を指定することで、翻訳言語を選択できます。（例：`intl={{ locale: "es-es" }}` </br></br>）サポートされているロケール文字列は、言語名の標準規格を表す [ISO 639 - コード](https://www.iso.org/iso-639-language-codes.html)に従います。</br></br> サポートされているロケールの一覧：英語 - &#39;en-us&#39;（デフォルト）スペイン語 - &#39;es-es&#39; ドイツ語 - &#39;de-de&#39; フランス語 - &#39;fr-fr&#39; イタリア語 - &#39;it-it&#39; 日本語 - &#39;ja-jp&#39; 韓国語 - &#39;ko-kr&#39; ポルトガル語 - &#39;pt-br&#39; 中国語（簡体字） - &#39;zh-cn&#39; 中国語（繁体字） - &#39;zh-tw&#39; |
| *repositoryId* | 文字列 | いいえ | &#39;&#39; | アセットセレクターがコンテンツを読み込む元のリポジトリです。 |
| *additionalAemSolutions* | `Array<string>` | いいえ | [ ] | 追加の AEM リポジトリのリストを追加できます。このプロパティで情報が指定されない場合、メディアライブラリまたは AEM Assets リポジトリのみが考慮されます。 |
| *hideTreeNav* | ブール値 | いいえ |  | アセットツリーのナビゲーションサイドバーを表示するか非表示にするかを指定します。このプロパティはモーダルビューでのみ使用されるので、パネルビューではこのプロパティの影響はありません。 |
| *onDrop* | 関数 | いいえ | | このプロパティで、アセットのドロップ機能を許可することができます。 |
| *dropOptions* | `{allowList?: Object}` | いいえ | | 「allowList」を使用してドロップオプションを設定します。 |
| *colorScheme* | 文字列 | いいえ | | アセットセレクターのテーマ（`light` または `dark`）を設定します。 |
| *テーマ* | 文字列 | いいえ | デフォルト | アセットセレクターアプリケーションに、`default` と `express` の間のテーマを適用します。また、`@react-spectrum/theme-express` もサポートしています。 |
| *handleSelection* | 関数 | いいえ | | アセットが選択され、モーダルの `Select` ボタンがクリックされた場合に、アセットの項目の配列と一緒に呼び出されます。この関数は、モーダルビューでのみ呼び出されます。パネルビューの場合は、`handleAssetSelection` 関数または `onDrop` 関数を使用します。例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 詳しくは、[アセットの選択](/help/assets/asset-selector-customization.md#selection-of-assets)を参照してください。 |
| *handleAssetSelection* | 関数 | いいえ | | アセットが選択または選択解除されたときに、項目の配列と一緒に呼び出されます。これは、ユーザーがアセットの選択時にアセットをリッスンする場合に役立ちます。例： <pre>handleSelection=(assets: Asset[])=> {...}</pre> 詳しくは、[アセットの選択](/help/assets/asset-selector-customization.md#selection-of-assets)を参照してください。 |
| *onClose* | 関数 | いいえ | | モーダルビューで `Close` ボタンが押された際に呼び出されます。これは、`modal` ビューでのみ呼び出され、`rail` ビューでは無視されます。 |
| *onFilterSubmit* | 関数 | いいえ | | ユーザーが別のフィルター条件を変更したときに、フィルター項目と一緒に呼び出されます。 |
| *selectionType* | 文字列 | いいえ | シングル | 一度にアセットを `single` 選択または `multiple` 選択するための設定です。 |
| *dragOptions.allowList* | ブール値 | いいえ | | プロパティは、選択できないアセットのドラッグを許可または拒否するために使用されます。 [dragOptions プロパティ ](/help/assets/asset-selector-customization.md#drag-options-property) を参照 |
| *aemTierType* | 文字列 | いいえ |  | 配信層、オーサー層またはその両方のアセットを表示するかを選択できます。<br><br>構文：`aemTierType:[0]: "author" 1: "delivery"` <br><br>例えば、`["author","delivery"]` の両方を使用する場合、リポジトリスイッチャーにはオーサーと配信の両方のオプションが表示されます。 |
| *handleNavigateToAsset* | 関数 | いいえ | | アセットの選択を処理するコールバック関数です。 |
| *noWrap* | ブール値 | いいえ | | *noWrap* プロパティは、サイドパネルでのアセットセレクターのレンダリングに役立ちます。このプロパティを指定しない場合、デフォルトで&#x200B;*ダイアログビュー*&#x200B;がレンダリングされます。 |
| *dialogSize* | 小、中、大、フルスクリーン、またはフルスクリーンのテイクオーバー | 文字列 | オプション | 指定されたオプションを使用してサイズを指定することで、レイアウトを制御できます。 |
| *colorScheme* | ライトまたはダーク | いいえ | | このプロパティは、アセットセレクターアプリケーションのテーマを設定するために使用されます。テーマは、ライトテーマとダークテーマから選択できます。 |
| *filterRepoList* | 関数 | いいえ |  | Experience Manager リポジトリを呼び出し、フィルタリングされたリポジトリのリストを返す `filterRepoList` コールバック関数を使用できます。 |
| *expiryOptions* | 関数 | | | 次の 2 つのプロパティ間で使用できます。**getExpiryStatus** では、有効期限切れのアセットのステータスが表示されます。関数は、指定したアセットの有効期限に基づいて、`EXPIRED`、`EXPIRING_SOON` または `NOT_EXPIRED` を返します。[有効期限切れのアセットのカスタマイズ](/help/assets/asset-selector-customization.md#customize-expired-assets)を参照してください。さらに、**allowSelectionAndDrag** を使用できます。この場合、関数の値は `true` または `false` のいずれかになります。値が `false` に設定されている場合、有効期限切れのアセットはキャンバス上で選択またはドラッグできません。 |
| *showToast* | | いいえ | | これにより、アセットセレクターで、有効期限切れのアセットに対してカスタマイズされたトーストメッセージを表示できます。 |
| *metadataSchema* | 配列 | いいえ | | ユーザーからメタデータを収集するのに指定するフィールドの配列を追加します。このプロパティを使用すると、アセットに自動的に割り当てられるが、ユーザーには表示されない非表示のメタデータも使用できます。 |
| *onMetadataFormChange* | コールバック関数 | いいえ | | これは、`property` と `value` から構成されます。`Property` は、値を更新する *metadataSchema* から渡されたフィールドの *mapToProperty* と等しくなります。一方、`value` は、入力として指定する新しい値と等しくなります。 |
| *targetUploadPath* | 文字列 |  | `"/content/dam"` | ファイルのターゲットアップロードパスで、デフォルトは、アセットリポジトリのルートです。 |
| *hideUploadButton* | ブール演算式 | | False | これは、内部アップロードボタンを非表示にするかどうかを確認します。 |
| *onUploadStart* | 関数 | いいえ |  | これは、Dropbox、OneDrive、ローカル間でアップロードソースを渡すのに使用されるコールバック関数です。構文は `(uploadInfo: UploadInfo) => void` です。 |
| *importSettings* | 関数 | | | これにより、サードパーティソースからのアセットの読み込みのサポートが有効になります。`sourceTypes` は、有効にする読み込みソースの配列を使用します。サポートされているソースは、Onedrive と Dropbox です。構文は `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }` です。 |
| *onUploadComplete* | 関数 | いいえ | | これは、成功、失敗、重複の中からファイルアップロードステータスを渡すのに使用されるコールバック関数です。構文は `(uploadStats: UploadStats) => void` です。 |
| *onFilesChange* | 関数 | いいえ | | これは、ファイルを変更した際のアップロードの動作を示すのに使用されるコールバック関数です。アップロード保留中のファイルの新しい配列とアップロードのソースタイプを渡します。エラーの場合、ソースタイプは null になることがあります。構文は `(newFiles: File[], uploadType: UploadType) => void` です。 |
| *uploadingPlaceholder* | 文字列 | | | これは、アセットのアップロードを開始した際にメタデータフォームを置き換えるプレースホルダー画像です。構文は `{ href: string; alt: string; } ` です。 |
| *uploadConfig* | オブジェクト | | | これは、アップロード用にカスタマイズされた設定を含むオブジェクトです。 |
| *featureSet* | 配列 | 文字列 | | `featureSet:[ ]` プロパティは、アセットセレクターアプリケーションで特定の機能を有効または無効にするのに使用されます。コンポーネントまたは機能を有効にするには、配列に文字列値を渡すか、配列を空のままにして、そのコンポーネントを無効にします。例えば、アセットセレクターでアップロード機能を有効にするには、構文 `featureSet:[0:"upload"]` を使用します。 |

<!--
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->
