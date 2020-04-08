---
title: リリース2020.4.0のリリースノート
description: リリース2020.4.0のリリースノート
translation-type: tm+mt
source-git-commit: c6c0e93d881762a2b501abb3d8c8356046a5f082

---


# Release Notes for AEM as a Cloud Service 2020.4.0 {#release-notes}

次の節では、Experience Managerのクラウドサービス2020.4.0の一般的なリリースノートの概要を説明します。

## リリース日 {#release-date}

Experience Managerのクラウドサービス2020.4.0のリリース日は2020年4月10日です。

## アセット {#assets}

この節では、AEMのクラウドサービスリリース2020.4.0としてのExperience Manager Assetsとダイナミックメディアの新機能および更新点について説明します。

### 最新情報 {#assets-what-is-new}

* [Brand Portalは](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 、AEMのクラウドサービスアセットとして利用でき、アセットの配布の使用例をサポートします。 Brand Portal は、組織が承認済みのブランドおよび製品アセットを外部の代理店、パートナー、内部チーム、販売店などにダウンロードで安全に配布してマーケティングニーズに応えるうえで役に立ちます。
   * Brand Portalの設定は、Adobe I/Oコンソールを通じて行われます。
   * Brand Portalでのアセットソーシングは、AEMをクラウドサービスとして使用する場合はまだサポートされていません
* Adobe Asset Link [](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) 2.0の新しいリリースは、AEMをクラウドサービスとして使用できます。 Adobe Asset Linkは、AEM Assetsをアプリ内アセットリンクパネルを使用してPhotoshop、IllustratorおよびInDesignのCreative Cloudデスクトップアプリケーションと接続することで、コンテンツ作成プロセスのクリエイティブとマーケティング担当者とのコラボレーションを効率化します。
   * クラウドサービスとしてのAEMは、Adobe Asset Link用に事前に設定されているので、設定がシンプル [になります](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)。
   * アセットリンクで [AEM環境切り替え機能がサポートされ](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)、クリエイティブユーザーが様々なAEM環境（例：AEM Assetsを使用して複数のクライアントを使用するエージェンシーデザイナーの場合）に簡単に接続できるようになりました。
* 後処理ワークフロー [の自動開始は](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 、特定のフォルダ階層のフォルダプロパティUIで設定できます。
   * フォルダのプロパティUIがシンプル化され、新しい「アセット処理」タブにメタデータプロファイル、処理プロファイル、新しい自動開始ワークフローの設定が追加されました。
* アセットの再処理ダイアログでは、特定の処理プロファイルを選択し、サブフォルダーで再処理を決定できます。
* ダイナミックメディア：一部のみの発行の設定が追加され、アセットは安全なプレビューのためにのみ自動公開され、パブリックドメインの配信用にDMS7に公開することなく、AEMに明示的に公開できるようになりました。

### バグ修正  {#assets-bug-fixes}

* アセット処理の修正点
* ダイナミックメディアの設定とダイナミックメディア配信サービスへのアセットの公開に関する修正
