---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 5995c416328e6f340285004ec2e723cc9279dabd
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 27%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、2021 年や 2022 年など、以前のバージョンのリリースノートに移動できます。
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

* The [コンテンツフラグメントコンソール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en) では、タグを表示し、メタデータとしてコンテンツフラグメントに適用されたタグで検索できるようになりました。 この機能で Assets UI に切り替える必要がなくなり、コンテキストの切り替えが減り、効率が向上します。

![コンテンツフラグメントコンソールでのタグ付け](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Assets ビューの新機能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**画像スマートタグ用の人工知能フレームワークの改善**

Experience Manager Assets は、画像スマートタグ用に改善された人工知能フレームワークを使用するようになりました。 このコンテンツインテリジェンスにより、取り込み時にすべての画像アセットで使用できるスマートタグの関連性と精度が向上します。 

**アセットのリスト表示の列表示の設定**

Assets Essentialsでは、アセットのリスト表示に表示する列 ( ステータス、形式、Dimension、サイズなど ) を選択できるようになりました。

![列を設定](/help/release-notes/assets/configure-columns.png)

**関連性に基づいて検索結果を並べ替える**

Assets Essentialsは、デフォルトで、「関連性」に基づいて検索結果を並べ替えるようになりました。 検索したアセットを、`Name`、`Relevance`、`Size`、`Modified` および `Created` の昇順または降順に並べ替えることができます。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-forms-channel}

* [**標準のテーマ**](/help/forms/using-themes-in-core-components.md) **およびテンプレート**：経験豊富な専門家や新しいフォーム作成者の皆様に役立つようにカスタマイズされた、すぐに使える OOTB のテーマとテンプレートを使用して、フォーム作成プロセスを開始します。 アダプティブFormsのコアコンポーネントを使用してシームレスに構築され、細心の注意を払って厳選されたテーマとテンプレートを使用すれば、一般的な使用例に合わせてすばやくフォームの作成を開始できます。

  ![標準テンプレート](/help/forms/assets/form-templates-ootb.png)

* **ヘッドレスForms用 React コンポーネント**：すぐに使用できる React コンポーネントを使用して、ヘッドレスアダプティブフォームのレンディションをプレビューし、カスタマイズできるようになりました。 これらのコンポーネントは、アダプティブFormsコアコンポーネントの BEM クラスをスタイル設定に活用するので、特定の要件に従って外観を簡単にカスタマイズできます。

* [**繰り返し可能なセクションでのアダプティブFormsの作成**](/help/forms/create-forms-repeatable-sections.md): [アコーディオン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [ウィザード](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html), [パネル](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)、および [水平タブ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) 複数のデータレコードをキャプチャする場合に繰り返し可能な、コンポーネントベースのアダプティブフォーム。  これらの繰り返し可能なセクションを使用すると、複数のデータエントリを簡単に指定できます。 これは、必要なデータインスタンスが事前に不明な場合に役立ちます。 フォームの入力者はセクションを簡単に追加または削除でき、フォームを様々なデータ入力シナリオに対応でき、同じデータレコードの複数回のオカレンスの収集を簡単にします。


### で使用可能なリリース前機能 [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA エンタープライズサポート**](/help/forms/captcha-adaptive-forms.md)：アダプティブフォームでGoogle reCAPTCHA Enterprise を使用して、不正なアクティビティやスパムに対する保護を強化し、より安全なユーザーエクスペリエンスを提供します。 高度なリスク分析とシームレスな統合により、本物のユーザーは、ボットを効果的にブロックしながらフォームを簡単に送信できます。

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

用途 [ヘッドレスアダプティブForms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=jp) 開発者が、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できるようにする。 ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Formsの力を使う

電子メールを `aem-forms-headless@adobe.com` アーリーアダプタープログラムに参加するための公式電子メール ID から

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### アクションセンター {#actions-center}

重大なインシデントが発生した際に即座に対応する必要が生じた場合に警告する電子メール通知を購読し、また、サイトを最適化するためのパーソナライズされたレコメンデーションを提供します。 [アクションセンター](/help/operations/actions-center.md) は、ブロックされたレプリケーションキューや資格情報の期限切れなど、これらのアラートを確認し、解決済みとしてマークできるハブとして機能します。

![アクションセンターのスクリーンショット](/help/assets/assets/actions-center.png)

### CDN および WAF ルールのアーリーアダプタープログラム {#waf-early-adopter}

CDN でのトラフィックのフィルタリング基準：
* リクエストヘッダーとプロパティ（IP アドレスなど）
* 悪意のあるトラフィックに関連付けられていると知られているトラフィックパターン

この機能を試して、フィードバックを共有したい場合は、 電子メールの送信先 **aemcs-waf-adopter@adobe.com** アーリーアダプタープログラムの詳細については、公式電子メール ID を参照してください。 スペースは制限されています。

この機能の詳細については、この記事を参照してください。 [ここ](/help/security/cdn-and-waf-rules.md).

### Foundation のその他の変更 {#other-foundation-changes}

* 8 月 7 日の週に、AEMインスタンスへのリクエストが正常なレベルを超えると、AEMはエラーコード 503 ではなく 429 を返します。 [詳細情報](/help/implementing/developing/introduction/development-guidelines.md)。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
