---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.7.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.7.0 リリースのリリースノート。'
exl-id: 7866d94c-e54c-4bb2-aaa6-66c019e46336
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 47%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.7.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.7.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.7.0) は 2023 年 7 月 27 日です。 次の機能リリース (2023.8.0) は、2023 年 8 月 31 日に予定されています。

## リリースビデオ {#release-video}

2023.7.0 リリースに追加された機能の概要については、 2023 年 7 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] {#sites-features}

* MSM for Content フラグメント。 コンテンツフラグメントでAEMマルチサイトマネージャーを使用できるようになり、コンテンツフラグメントのライブコピーを作成して一括コンテンツ配布が可能になりました。 詳細な継承コントロールは、コンテンツフラグメント要素とバリエーションレベルまで使用できます。

### [!DNL Experience Manager Sites] プレリリースの新機能 {#prerelease-sites}

* The [コンテンツフラグメントコンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=ja) では、タグを表示し、メタデータとしてコンテンツフラグメントに適用されたタグで検索できるようになりました。 この機能で Assets UI に切り替える必要がなくなり、コンテキストの切り替えが減り、効率が向上します。

![コンテンツフラグメントコンソールでのタグ付け](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセットビューの新機能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**画像スマートタグ用の人工知能フレームワークの改善**

Experience Manager Assets は、画像スマートタグ用に改善された人工知能フレームワークを使用するようになりました。このコンテンツインテリジェンスにより、取り込み時にすべての画像アセットで使用できるスマートタグの関連性と精度が向上します。

**アセットのリスト表示の列表示の設定**

Assets Essentials では、ステータス、形式、ディメンション、サイズなど、アセット のリスト表示に表示する列を選択できるようになりました。

![列を設定](/help/release-notes/assets/configure-columns.png)

**関連性に基づいた検索結果の並べ替え**

Assets Essentials では、デフォルトで、関連性に基づいて検索結果を並べ替えるようになりました。検索したアセットを、`Name`、`Relevance`、`Size`、`Modified` および `Created` の昇順または降順に並べ替えることができます。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-forms-channel}

* [**標準のテーマ**](/help/forms/using-themes-in-core-components.md) **およびテンプレート**：経験豊富な専門家や新しいフォーム作成者の皆様に役立つようにカスタマイズされた、すぐに使える OOTB のテーマとテンプレートを使用して、フォーム作成プロセスを開始します。 アダプティブFormsのコアコンポーネントを使用してシームレスに構築され、細心の注意を払って厳選されたテーマとテンプレートを使用すれば、一般的な使用例に合わせてすばやくフォームの作成を開始できます。

* **[ヘッドレスForms用 React コンポーネント](https://github.com/adobe/aem-forms-headless-components/tree/main/packages/react-vanilla-components)**：すぐに使用できる React コンポーネントを使用して、ヘッドレスアダプティブフォームのレンディションをプレビューし、カスタマイズできるようになりました。 これらのコンポーネントは、アダプティブFormsコアコンポーネントの BEM クラスをスタイル設定に活用するので、特定の要件に従って外観を簡単にカスタマイズできます。

* [**繰り返し可能なセクションでのアダプティブFormsの作成**](/help/forms/create-forms-repeatable-sections.md): [アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=ja), [ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=ja), [パネル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html?lang=ja)、および [水平タブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=ja) 複数のデータレコードをキャプチャする場合に繰り返し可能な、コンポーネントベースのアダプティブフォーム。  これらの繰り返し可能なセクションを使用すると、複数のデータエントリを簡単に指定できます。 これは、必要なデータインスタンスがあらかじめ不明な場合に役立ちます。フォームの入力者はセクションを簡単に追加または削除でき、フォームを様々なデータ入力シナリオに対応でき、同じデータレコードの複数回のオカレンスの収集を簡単にします。


### で使用可能なリリース前機能 [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA エンタープライズサポート**](/help/forms/captcha-adaptive-forms.md)：アダプティブフォームでGoogle reCAPTCHA Enterprise を使用して、不正なアクティビティやスパムに対する保護を強化し、より安全なユーザーエクスペリエンスを提供します。 高度なリスク分析とシームレスな統合により、本物のユーザーは、ボットを効果的にブロックしながらフォームを簡単に送信できます。

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

[ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp)を使用すると、開発者は、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Forms の機能を活用

ご自身の公式メール ID から `aem-forms-headless@adobe.com` にメールを送信して、早期導入者プログラムにご参加ください。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### アクションセンター {#actions-center}

重大なインシデントが発生した際に即座に対応する必要が生じた場合に警告する電子メール通知を購読し、また、サイトを最適化するためのパーソナライズされたレコメンデーションを提供します。 [アクションセンター](/help/operations/actions-center.md) は、ブロックされたレプリケーションキューや資格情報の期限切れなど、これらのアラートを確認し、解決済みとしてマークできるハブとして機能します。

![アクションセンターのスクリーンショット](/help/assets/assets/actions-center.png)

### CDN および WAF ルールのアーリーアダプタープログラム {#waf-early-adopter}

CDN でのトラフィックのフィルタリング基準：
* ヘッダーとプロパティのリクエスト（IP アドレスなど）
* 悪意のあるトラフィックに関連付けられていると知られているトラフィックパターン

この機能を試して、フィードバックを共有したい場合は、 電子メールの送信先 **aemcs-waf-adopter@adobe.com** アーリーアダプタープログラムの詳細については、公式電子メール ID を参照してください。 スペースは制限されています。

この機能の詳細については、この記事を参照してください。 [ここ](/help/security/traffic-filter-rules-including-waf.md).

### Foundation のその他の変更 {#other-foundation-changes}

* 8 月 7 日の週に、AEMインスタンスへのリクエストが正常なレベルを超えると、AEMはエラーコード 503 ではなく 429 を返します。 [詳細情報](/help/implementing/developing/introduction/development-guidelines.md)。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
