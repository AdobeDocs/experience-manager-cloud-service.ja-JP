---
title: 2020.4.0のクラウドサービスリリースノートとしてのAdobe Experience Manager
description: 2020.4.0向けExperience Managerリリースノート
translation-type: tm+mt
source-git-commit: 57df03fe198564a6c02e54e19ef059e46064d163

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

次の節では、クラウドサービス2020.4.0 [!DNL Experience Manager] の一般的なリリースノートの概要を説明します。

## リリース日 {#release-date}

クラウドサー [!DNL Experience Manager] ビス2020.4.0のリリース日は2020年4月9日です。

## What&#39;s New in Assets {#assets}

および現在のリリースの新機能、機能強化、バグ修正に [!DNL Experience Manager Assets] つい [!DNL Dynamic Media] て詳しく説明します。

* [Brand Portalは](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 、Experience Manager Assetsのアセット配布の使用例をサポートします。 [!DNL Brand Portal] は、組織が承認済みのブランドおよび製品アセットを外部の代理店、パートナー、内部チーム、販売店などに安全に配布してマーケティングニーズに応えるうえで役に立ちます。
   * [!DNL Brand Portal] 設定は、コンソールを通じて行 [!DNL Adobe I/O] われます。
   * でのアセットソーシ [!DNL Brand Portal] ングは、Experience Managerをクラウドサ [!DNLEービスとして使用する場合] 、まだサポートされていません。

* [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) v2.0は、クラウドサービスと [!DNL Experience Manager] して機能します。 [!DNL Adobe Asset Link] デスクトップアプリ、アプリ内パネルを使用して、コンテンツ作成プロセスでのクリエイティブとマーケ [!DNL Experience Manager Assets] ターのコラボレ [!DNL Creative Cloud] ーションを [!DNL Adobe Photoshop]効率化し、デス [!DNL Adobe Illustrator]クトップアプリとの連携を [!DNL Adobe InDesign] 実現し [!DNL Asset Link] ます。
   * [!DNL Experience Manager] はに事前設定されており、 [!DNL Adobe Asset Link]設定が簡単で、ク [リエイティブな](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) 専門家に対する展開が速くなります。
   * [!DNL Asset Link] クリエイティブユーザーが [別の環境に簡単に接続できる](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 、 [!DNL Experience Manager] Experience Managerの環境切り替えボタンをサポートするようになりました。 この機能が役立つのは、異なるデプロイメントを使用して複数のクライアントを扱うエージェンシーデザイナーの [!DNL Experience Manager Assets] 場合です。

* ユーザーは、特定のフ [ォルダー階層のフォルダー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) Propertiesユーザーインターフェイスで、後処理ワークフローを自動 [!UICONTROL 開始に設定できます] 。
   * フォルダのプロ [!UICONTROL パティ] (Properties  )のユーザーインターフェイスがシンプルになり、新しい「アセット処理」タブにメタデータプロファイル、処理プロファイル、新しい自動開始ワークフローの設定が追加されました。
   * アセットの再処理ダイアログでは、特定の処理プロファイルを選択し、サブフォルダーで再処理を決定できます。
   * [!DNL Dynamic Media]:アセットをセキュリティで保護されたプレビューのみのために自動公開するように、選択的公開設定を追加。 また、パブリックドメイン内の配信用にDMS7に公開することなく、アセットをExperience Managerに明示的に公開できます。

* 次の問題に対処しました。
   * アセットの処理に関する問題を修正しました。
   * アセットの設定 [!DNL Dynamic Media] と公開に関する修正を [!DNL Dynamic Media] 配信サービスに

>[!MORELIKETHIS]
>
>* [Adobe Assetリンクについて](https://www.adobe.com/jp/creativecloud/business/enterprise/adobe-asset-link.html)
>* [ブランドポータルの設定](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Experience Managerを設定して、アセットリンクを使用する](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [アセットのマイクロサービスを使用して、Experience Managerでワークフローを作成する](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)

