---
title: Adobe Experience Manager as a Cloud Service 2020.4.0 のリリースノート
description: Experience Manager 2020.4.0 のリリースノート
translation-type: tm+mt
source-git-commit: 3dc0d1d77595f7b3e890fb4b390eef5bcf84ecd8
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 2020.4.0 のリリースノート {#release-notes}

このページでは、 [!DNL Experience Manager] as a Cloud Service 2020.4.0 の一般的なリリースノートの概要を説明します。

## リリース日 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.4.0 のリリース日は 2020 年 4 月 9 日です。

## Assets の新機能{#assets}

現在のリリースの [!DNL Experience Manager Assets] および [!DNL Dynamic Media] の新機能、機能強化、バグ修正について詳しく説明します。

* [Brand Portal](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/home.html) は、Experience Manager Assets のアセット配布使用例をサポートします。[!DNL Brand Portal] は、組織が承認済みのブランドおよび製品アセットを外部の代理店、パートナー、内部チーム、販売店などがダウンロードできるように安全に配布し、マーケティングニーズに応えるうえで役に立ちます。
   * [!DNL Brand Portal] 設定は、[!DNL Adobe I/O] コンソールを通じておこなわれます。[Brand Portal の設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)を参照してください。
   * [!DNL Brand Portal] でのアセットソーシングは、[!DNL Experience Manager] as a Cloud Service ではまだサポートされていません。

* [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) v2.0 は、[!DNL Experience Manager] as a Cloud Service として機能します。[!DNL Adobe Asset Link] は、アプリ内パネル [!DNL Asset Link] を使用して、[!DNL Experience Manager Assets] と [!DNL Creative Cloud] デスクトップアプリの [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]、[!DNL Adobe InDesign] の連携を実現し、コンテンツ作成プロセスにおいてのクリエイティブとマーケターのコラボレーションを効率化します。
   * [!DNL Experience Manager] は [!DNL Adobe Asset Link] 用に事前設定されているため、[設定が簡単](https://helpx.adobe.com/jp/enterprise/using/configure-aem-assets-for-asset-link.html)で、クリエイティブな専門家へのロールアウトが速くなります。
   * [!DNL Asset Link] クリエイティブユーザーが別の [!DNL Experience Manager] 環境に簡単に接続できる、[Experience Manager 環境の切り替えボタン](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)がサポートされました。この機能が役立つのは、異なる [!DNL Experience Manager Assets] デプロイメントを使用して複数のクライアントを扱う、エージェンシーデザイナーの場合です。

* ユーザーは、特定のフォルダー階層に対するフォルダーの「[!UICONTROL プロパティ]」ユーザーインターフェイスで、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を自動開始するように設定できます。
   * フォルダーの「[!UICONTROL プロパティ]」ユーザーインターフェイスがシンプルになり、新しい「[!UICONTROL アセット処理]」タブに、メタデータプロファイル、処理プロファイル、新しく自動開始ワークフロー設定が追加されました。

      ![処理プロファイルは、フォルダーに簡単に適用でき、フォルダーにアップロードされたすべてのアセットは、これらのプロファイルを使用して処理されます。](/help/assets/assets/asset-processing-folder-properties.png)

   * アセットの再処理オプションを使用すると、特定の処理プロファイルを選択して、サブフォルダー内のユーザーが選択したアセットを再処理できます。

      ![特定の処理プロファイルを使用して、選択したアセットを再処理する](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]：アセットをセキュリティで保護されたプレビューのみで自動公開するように、選択的公開の設定を追加。また、パブリックドメインの配信用に DMS7 に公開することなく、アセットを Experience Manager に明示的に公開できます。

### バグ修正 {#assets-bug-fixes}

* アセット処理に関する問題を修正しました。
* [!DNL Dynamic Media] の設定と [!DNL Dynamic Media] 配信サービスへのアセット公開を修正

>[!MORELIKETHIS]
>
>* [Adobe Asset Link について](https://www.adobe.com/jp/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Brand Portal の設定](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Asset Link を使用するための Experience Manager の設定](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [アセットのマイクロサービスを使用した、Experience Manager でのワークフロー作成](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Cloud Manager の新機能 {#whats-new-cloud-manager}

* 発行者の URL が、Cloud Manager UI の環境ページから利用できるようになりました。
* ナビゲーションが変更され、Cloud Manager の概要ページでユーザーがプログラムの編集、切り替え、追加が可能になりました。
* ユーザーが Cloud Manager ランディングページのプログラムカードからプログラムを編集できるように変更しました。
* 関連付けられた環境に対して、新しいパイプラインステータス「**パイプライン実行中**」が表示されます。
* パイプライン実行ページをわかりやすく改善しました。これには、パイプライン名（非実稼動パイプラインのみ）とタイプの表示、およびパイプラインのステータスが「処理中」、「キャンセル」、「失敗」のいずれであるかを示すバッジが含まれます。
* ユーザーエクスペリエンスを向上させ、「プログラム／環境」ボタンが無効になる理由を理解しやすくするためのツールヒント。
* 失敗した環境は、UI と API を使用して削除できるようになりました。
* git パスワードの生成に使用されるプロセスは、基盤となるサービス層の問題に対してより柔軟に対処できるようになりました。

### バグ修正 {#bug-fixes-cloud-manager}

* パイプライン実行の詳細ページのステージ環境へのリンクが、正しい場所に一貫してナビゲーションしていなかった。
* 環境作成プロセス内の個々のステップが、必要な時間より早くタイムアウトし、プロセスが失敗する。
* アーティファクトのメタデータをダウンロードする際のデッドロックを回避するため、ビルドコンテナで使用される Maven の設定を更新。
* 場合によっては、イメージのビルド手順で顧客パッケージを正常にダウンロードできない。
* 発生頻度の低い状況によっては、環境の削除が妨げられる場合がある。
* Experience Cloud の通知が一貫して受信されなかった。
