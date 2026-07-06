---
title: Content AdvisorとDynamic Mediaの統合
description: Content AdvisorとDynamic Mediaを統合して、ユーザーがアプリケーションやワークフローで使用するDynamic Media レンディションを参照、プレビュー、選択できるようにする方法について説明します。
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 8%

---

# Dynamic Mediaとの統合 {#integrate-dynamic-media}

Content AdvisorはDynamic Mediaと統合されているため、ユーザーはアプリケーションやワークフローで使用するDynamic Media レンディションを参照、プレビュー、選択できます。 ユーザーは、利用可能なレンディション、画像プリセット、スマート切り抜きから選択し、サポートされているDynamic Media修飾子を適用してアセット配信をカスタマイズできます。 次の節では、選択したレンディション情報を処理し、アプリケーションで使用するDynamic Media配信URLを生成する方法について説明します。

## selectedMediaを使用したDynamic Media URLの作成 {#build-dynamic-media-urls-selectedmedia}

ユーザーがContent Advisor Dynamic Media パネルからDynamic Media レンディションを選択すると、選択したレンディション情報が`selectedMedia` オブジェクトに返されます。 ホストアプリケーションは、この情報を使用して、適切なDynamic Media配信URLを生成する必要があります。

>[!NOTE]
>
> コンテンツアドバイザーから選択したDynamic Media レンディションを使用するには、この節で説明するURL生成ロジックをホストアプリケーションに実装する必要があります。 選択したレンディション情報はメタデータとして返され、配信URLに自動的に変換されません。

### selectedMedia オブジェクト {#selectedmedia-object}

`selectedMedia` オブジェクトは、選択したアセットに追加され、ユーザーが選択したDynamic Media レンディションに関する情報が含まれます。

```javascript
'selectedMedia': Array<{
    base?: string;
    preset?: string;
    smartcrop?: string;
    modifiers?: Array<string>;
    apiStyle?: 'scene7' | 'openapi'
}>;
```

`selectedMedia` オブジェクトには、次のプロパティが含まれています。

| プロパティ | 説明 |
|---|---|
| `base` | 選択したベースレンディション。 |
| `preset` | 選択した画像プリセット。 |
| `smartcrop` | 選択したスマート切り抜きレンディション。 |
| `modifiers` | ユーザーが追加した1つ以上のDynamic Media修飾子。 |
| `apiStyle` | 選択したレンディションがScene7 （`scene7`）またはOpenAPI （`openapi`）配信スタックを使用しているかどうかを示します。 |

例えば、ユーザーが基本レンディションを選択して`rotate=90`修飾子を適用すると、返されるオブジェクトは次のようになります。

```javascript
selectedMedia: {
    apiStyle: "scene7",
    base: "scene7company/image",
    modifiers: ["rotate=90"]
}
```

![Dynamic Media レンディションを表示](assets/content-advisor-dm-renditions.png)

### handleSelection コールバックのselectedMediaにアクセスします {#access-selectedmedia}

レンディションを選択すると、`handleSelection` コールバックによって返された`selectedAssets` ペイロード内で`selectedMedia` オブジェクトが使用可能になります。

```javascript
async function handleSelection(assets) {

    const dmUrls = [];

    assets.forEach((asset) => {

        if(asset?.selectedMedia){

            const dmUrl = createDMUrlFromSelectedMedia(
                asset.selectedMedia,
                asset
            );

            dmUrls.push({ asset, dmUrl });

        }

    });
}
```

コールバックは、選択したアセットを繰り返し処理します。 `selectedMedia` オブジェクトを含む各アセットについて、選択したレンディション情報を使用してDynamic Media URLを生成します。

## Dynamic Media URLの生成 {#generate-dynamic-media-url}

次の関数は、選択したレンディション情報を検証し、使用するDynamic Media配信スタックを決定します。

```javascript
const DM_OPENAPI_API_STYLE = 'openapi';
const DM_SCENE7_API_STYLE = 'scene7';
const ASSET_REPO_NAME_KEY = 'repo:name';
const ASSET_REPO_ID_KEY = 'repo:id';
const REPO_ID_KEY = 'repo:repositoryId';

export const createDMUrlFromSelectedMedia = (
    selectedMedia,
    repoMetadata
) => {
    if (!selectedMedia || !selectedMedia?.apiStyle) {
        throw new Error(
            'Selected media or api style is not valid'
        );
    }

    if (
        selectedMedia?.apiStyle === DM_OPENAPI_API_STYLE
    ) {
        return buildDMOpenApiUrl(
            selectedMedia,
            repoMetadata
        );
    } else if (
        selectedMedia?.apiStyle === DM_SCENE7_API_STYLE
    ) {
        return buildDMScene7Url(
            selectedMedia,
            repoMetadata
        );
    }
};
```

この関数は、次のアクションを実行します。

* 選択したレンディションに`apiStyle`値が含まれていることを検証します。
* 選択したレンディションでOpenAPI機能を備えたDynamic Mediaを使用するか、Dynamic Media Scene7を使用するかを指定します。
* 選択した配信スタックに基づいて、適切なURL生成関数を呼び出します。

### Dynamic Media OpenAPI URLの構築 {#build-openapi-url}

次の関数は、選択したレンディション情報とリポジトリメタデータを使用して、Dynamic Media OpenAPI URLを生成します。

```javascript
export const buildDMOpenApiUrl = (
    selectedMedia,
    repoMetadata
) => {
    const { base, preset, smartcrop, modifiers }
        = selectedMedia;

    const dmDomain =
        repoMetadata?.[REPO_ID_KEY]
            .replace('author-', 'delivery-');

    const assetName =
        repoMetadata?.[ASSET_REPO_NAME_KEY];

    const assetId =
        repoMetadata?.[ASSET_REPO_ID_KEY];

    const seoName =
        assetName?.split('.')[0];

    const assetFormat =
        repoMetadata?.['dc:format'];

    let dmUrl;

    if (
        assetFormat &&
        assetFormat.startsWith('video/')
    ) {

        dmUrl =
`https://${dmDomain}/adobe/assets/${assetId}/play`;

    } else {

        dmUrl =
`https://${dmDomain}/adobe/assets/${assetId}/as/${seoName}.avif`;

        if (base) {
        } else if (preset) {
            dmUrl =
`${dmUrl}?preset=${preset}`;
        } else if (smartcrop) {
            dmUrl =
`${dmUrl}?smartcrop=${smartcrop}`;
        }
    }

    if (modifiers && dmUrl) {

        const modifierString =
            getModifierString(selectedMedia);

        if(base) {
            dmUrl =
`${dmUrl}?${modifierString}`;
        } else {
            dmUrl =
`${dmUrl}&${modifierString}`;
        }
    }

    return dmUrl;
};
```

この関数：

* 配信URLの作成に必要なリポジトリ情報を取得します。
* ベースのOpenAPI配信URLを作成します。
* 選択したプリセットまたはスマート切り抜きを、該当する場合URLに追加します。
* ユーザーが選択した修飾子を追加します。
* 最終的なOpenAPI配信URLを返します。

ビデオアセットの場合、関数はDynamic Media ビデオプレーヤーのURLを生成します。

### Dynamic Media Scene7 URLの作成 {#build-scene7-url}

次の関数は、Dynamic Media Scene7 URLを生成します。

```javascript
export const buildDMScene7Url = (
    selectedMedia,
    repoMetadata
) => {

    const {
        base,
        preset,
        smartcrop,
        modifiers
    } = selectedMedia;

    let scene7Domain =
        repoMetadata?.['repo:scene7Domain'];

    const scene7File =
        repoMetadata?.['repo:scene7File'];

    if (!scene7Domain || !scene7File) {
        return null;
    }

    scene7Domain =
        scene7Domain.startsWith('http://')
        ? scene7Domain.replace(
            'http://',
            'https://'
          )
        : scene7Domain;

    scene7Domain =
        scene7Domain?.endsWith('/')
        ? scene7Domain
        : `${scene7Domain}/`;

    let dmUrl;

    if (base) {

        dmUrl =
`${scene7Domain}is/image/${base}`;

    } else if (preset) {

        dmUrl =
`${scene7Domain}is/image/${scene7File}?$${preset}$`;

    } else if (smartcrop) {

        dmUrl =
`${scene7Domain}is/image/${scene7File}:${smartcrop}`;
    }

    if (modifiers && dmUrl) {

        const modifierString =
            getModifierString(selectedMedia);

        if (preset) {
            dmUrl =
`${dmUrl}&${modifierString}`;
        } else {
            dmUrl =
`${dmUrl}?${modifierString}`;
        }
    }

    return dmUrl;
};
```

この関数：

* リポジトリメタデータからScene7 ドメインとアセット情報を取得します。
* 選択したベースレンディション、画像プリセット、スマート切り抜きのURLを作成します。
* 選択した修飾子を追加します。
* 最終的なScene7配信URLを返します。

## 修飾子文字列の生成 {#generate-modifiers-string}

次のヘルパー関数は、修飾子配列をURL互換クエリ文字列に変換します。

```javascript
export const getModifierString = (
    selectedMedia
) => {

    const { modifiers } = selectedMedia;

    if (modifiers) {

        const modifierString =
            modifiers.length > 0
                ? modifiers.join('&')
                : '';

        return modifierString;
    }

    return null;
};
```

この関数は、選択したすべての修飾子を、アンパサンド （`&`）で区切られた単一の文字列に結合します。

次に例を示します。

```javascript
[
    'rotate=90',
    'width=1200'
]
```

以下のものを返します

```text
rotate=90&width=1200
```

生成された文字列は、最終的なDynamic Media URLに追加され、アセットの配信時に選択した変換が適用されます。

**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
