---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 リリースのリリースノート。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 のリリースノート。'
source-git-commit: 63b7c11683425cc20851ee5a16ee099511429b17
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 14%

---


# Cloud Service{#release-notes}としての[!DNL Adobe Experience Manager]の最新のリリースノート

以下の節では、[!DNL Experience Manager]の最新（最新）バージョンの一般的なリリースノートの概要をCloud Serviceとして説明します。

>[!NOTE]
>ここから、以前のバージョンのリリースノートに移動できます。例えば、2020、2021などの場合、

>[!NOTE]
>
>リリースと直接関係のないドキュメントの更新について詳しくは、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager]のCloud Service2021.3.0のリリース日は2021年3月25日です。
次のリリース(2021.4.0)は、2021年4月30日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* 簡単な設定で、[プログレッシブ Web アプリ（PWA）版のサイト](/help/sites-cloud/authoring/features/enable-pwa.md)がプロジェクトレベルで有効化できるようになりました。
* コンテンツフラグメントモデルの拡張 — 複数行テキストデータタイプを複数フィールドリストとして定義できるようになりました。
* コンテンツフラグメントエディターのUXの強化 — パンくずリストにネストされた子フラグメントが表示され、公開、保存、保存および終了のアクションの表示が改善されました

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] は、Connected Assets機能を拡張して、サポートされるコアコンポーネ [!DNL Dynamic Media] ントでの画像の使用をサポートします。[Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md)の使用を参照してください。
* Experience Manager管理者は、特定の日時に一括アセット取り込みのスケジュールを設定できます。 また、管理者は、日時に基づいて定期的な取り込みのスケジュールを設定できます。 [一括アセット取り込み](/help/assets/add-assets.md#asset-bulk-ingestor)を参照してください。

### [!DNL Assets] {#bug-fixes-assets}のバグ修正

* 著作権ページは、権限が管理された複数のアセットをダウンロードしようとしても表示されません。 (CQ-4314403)
* INDDファイルの編集を選択した場合、解像度が予期せず変更されます。 (CQ-4317376)
* PDFレンディションには、InDesignテンプレートの最後のページのみが含まれます。 (CQ-4317305)
* ピッカーが複雑なメタデータスキーマに含まれている場合、タグピッカーが開くのに時間がかかります。 (CQ-4316426)
* 既存のファイル名と同じファイル名を持つアセットをアップロードする場合、名前の競合ダイアログが表示されず、バージョンを作成するように求められます。 (CQ-4315424)
* フォルダーメタデータのプロパティは、フォルダーのプロパティページのポップアップメニューから設定および保存できます。 選択内容はリポジトリに保存されている間、フォルダーメタデータプロパティを再度開いても表示されません。 (CQ-4314429)
* スペースや特殊文字を含むファイル名を持つアセットは、ブラウザーを使用してアップロードされます。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] として  [!DNL Cloud Service] {#forms}

AEM Formsは、多くの組織が長年にわたって素晴らしいオンボーディングと登録の経験を提供するのを支援してきました。 これらのエクスペリエンスは、組織がリードを販売に変換し、取り込んだ顧客データを処理し、オーディエンスプロファイルに基づいてレスポンシブなエクスペリエンスを提供するのに役立ちました。 現在、AEM Formsはas a Cloud Serviceとして使用できます。

[AEM FormsをCloud Service](https://experienceleague.corp.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)として使用して、デジタルフォームの作成、既存のデータソースへのフォームの接続、Adobe Signとのフォームの統合、フォームへの電子署名の追加、レコードのドキュメント(DoR)の生成を行い、送信されたフォームをPDFファイルとしてアーカイブできます。 また、変換サービスを使用して、既存のPDF formsをデジタルフォームに変換することもできます。 このサービスは、AEM Formsの標準的な機能に加えて、自動スケーリング、アップグレードのダウンタイムなし、クラウドネイティブ開発環境など、いくつかのクラウドネイティブ機能を提供します。 AEM Forms as aCloud Serviceの機能については、[このブログ記事](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html)を参照してください。

デモを受ける場合は、Adobe担当者に問い合わせるか、サービスに新規登録してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* Magento2.4.2のサポート

* 製品の詳細コンポーネントを任意のコンテンツページで使用および設定できるようになりました。

* 最新の CIF コアコンポーネント v1.9.0 を含んだ CIF Venia 参照サイト 2021.03.25 をリリースしました。詳しくは、[CIF Venia 参照サイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25)を参照してください。

* CIF コアコンポーネント v1.9.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0)を参照してください。


## Cloud Manager {#cloud-manager}

この節では、AEM as aCloud Service2021.3.0のCloud Managerのリリースノートの概要を説明します。

## リリース日 {#release-date-cm-march}

AEM as aCloud Service2021.3.0のCloud Managerのリリース日は2021年3月11日です。
次回のリリースは2021年4月8日に予定されています。

### 新機能 {#what-is-new-march}

* [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL証明書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)および[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)の既存の環境のお客様には、既存の設定に関するメッセージが表示され、UIを介して自己提供できます。

* 必要な権限を持つユーザーがプログラムを編集でき、セルフサービス方式で次の操作を実行できるようになりました。

   * Assetsを使用する既存のプログラムにSitesソリューションを追加する（またはその逆）。
   * SitesとAssetsの両方を含む既存のプログラムからSitesまたはAssetsを削除します。
   * 2つ目の未使用のソリューション権利を既存のプログラムまたは新しいプログラムに追加します。

* **パイプライン実** 行とアクティビティ画面の両方に対して、AEM Push  *Updatelabel* が表示されるように ** なりました。

* 環境が休止状態になっていて、AEMの更新も使用可能な場合は、**Hevernated**&#x200B;ステータスが&#x200B;**Update available**&#x200B;よりも優先されます。

* ユーザーは、統合シェルのユーザープロファイルアイコン（右上）に移動した後、「Cloud Managerの役割を表示」オプションを選択することで、Cloud Managerの役割を表示できるようになりました。

* ラベル&#x200B;**承認の申請**&#x200B;が&#x200B;**実稼動の承認**&#x200B;に変更され、より明確になりました。

* 実稼動パイプラインの実行画面で、**Version**&#x200B;ラベルが&#x200B;**Gitタグ**&#x200B;にリラベルされました。

* 重要な指標が定義されたしきい値を満たさない場合の動作を定義するラベルが、実際の動作を反映するように再ラベル付けされました。**直ちにキャンセル**&#x200B;および&#x200B;**直ちに承認**&#x200B;します。

* クラスおよびメソッドの廃止リストは、AEMCloud ServiceSDKのバージョン`2021.3.4997.20210303T022849Z-210225`に基づいて更新されました。

* Cloud Managerの実稼動パイプラインに、[カスタムUIテスト](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)機能が含まれるようになりました。

### バグ修正 {#bug-fixes-cm-march}

* AEMのプッシュアップグレード中に、パッケージのバージョン管理がスキップされることがありました。

* 他のパッケージにパッケージが埋め込まれた場合に、品質の問題が正しく検出されない場合がありました。

* 難しい状況では、プログラムの追加ダイアログを開いたときに生成されるデフォルトのプログラム名が、既存のプログラム名と重複している可能性があります。

* 場合によっては、ユーザーがパイプラインの開始直後にパイプライン実行ページから離れると、実際に実行が開始するにもかかわらず、アクションが失敗したことを示すエラーメッセージが表示されます。

* 顧客のビルドで無効なパッケージが生成された場合、ビルド手順が不必要に再開されました。

* 場合によっては、その設定がデプロイされていない場合で許可リストも、IPの横に緑色の「アクティブ」ステータスが表示されることがあります。

* 「エクスペリエンス監査」ステップで既存のすべての実稼働パイプラインが自動的に有効になります。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

コンテンツ転送ツールv1.3.4のリリース日は2021年3月20日です。

### バグ修正 {#bug-fixes-ctt}

* CTTが、同じ名前で名前にハイフンを含むフォルダーのコンテンツをスキップしていた問題を修正しました。 この問題が修正されました。

### リリース日 {#release-date-ctt-march}

コンテンツ転送ツールv1.3.0のリリース日は2021年3月4日です。

### コンテンツ転送ツールの新機能{#what-is-new-ctt-march}

* CTTは、`/libs`の代わりに`/apps`にインストールするようになりました。特定のページへのブラウザーブックマークが有効でなくなる場合があります。
* CTTがインストールされている場合、ユーザーは追加のレベルに移動して、コンテンツ転送ページに移動する必要があります。 詳しくは、[コンテンツ転送ツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html)を参照してください。

### バグ修正 {#bug-fixes-ctt-march}

* 特定のパスからコンテンツを移行する際、CTTは関連のないリソースを取り込んでいました。 この問題は修正されました

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.8のリリース日は2021年3月23日です。

### ベストプラクティスアナライザー{#what-is-new-bpa}の新機能

* UIのBPAレポートと、CSVファイルとしてエクスポートされたレポートから、ACS Commonsの結果を除外する機能。

## コードリファクタリングツール {#code-refactoring-tools}

### コードリファクタリングツールの新機能{#what-is-new-crt}

* Repository Modernizerの新機能と機能強化。 [GitHubリソースを参照してください。最新バージョンのRepository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * OSGi設定（RepoInit設定を除く）を推奨の.cfg.json形式に正規化します。
   * OSGi設定フォルダーの名前を指定した形式に変更します。
   * ui.apps.structureプロジェクトを生成します。
   * 分析モジュールを作成します。

* Dispatcherコンバーターの新機能と機能強化。 [GitHubリソースを参照してください。Dispatcherコンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * コンテンツのラインではなく、異なるインクルージョン用に別々のファイルを作成する。
   * vhostsのフォルダーパスとvhostファイルへのパスの両方を処理できます。
   * 600以上の範囲の大規模な顧客構成を持つファームファイルの生成。
