---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
translation-type: tm+mt
source-git-commit: affe1f0be3f3448e15787cdd831474e0a9d5de6b
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 12%

---

# Cloud Service{#release-notes}としての[!DNL Adobe Experience Manager]の最新のリリースノート

次の節では、Cloud Serviceとしての[!DNL Experience Manager]の最新（最新）版のリリースノートの概要を説明します。

>[!NOTE]
>ここから、以前のバージョンのリリースノートに移動できます。例えば、2020年、2021年などの場合、

>[!NOTE]
>
>リリースに直接関連しないドキュメントの更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

Cloud Service2021.3.0の[!DNL Adobe Experience Manager]のリリース日は2021年3月25日です。
次のリリース(2021.4.0)は、2021年4月29日にリリースされます。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* 簡単な設定で、[プログレッシブ Web アプリ（PWA）版のサイト](/help/sites-cloud/authoring/features/enable-pwa.md)がプロジェクトレベルで有効化できるようになりました。
* コンテンツフラグメントモデルの拡張機能 — 複数行テキストデータ型を複数フィールドリストとして定義できるようになりました。
* コンテンツフラグメントエディターのUX拡張 — ネストされた子フラグメントがパンくずリストに表示されるようになりました。また、公開、保存、保存および保存と終了のアクションの表示が向上しました。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] は、接続されたアセット機能を拡張して、サポートされるコアコンポーネントでの [!DNL Dynamic Media] 画像の使用をサポートします。[接続されたアセットの使用](/help/assets/use-assets-across-connected-assets-instances.md)を参照してください。
* Experience Manager管理者は、バルクアセットのインジェクションを特定の日時にスケジュールできます。 また、管理者は、日時に基づいて定期的なインジメンションをスケジュールすることもできます。 [バルクアセットの取り込み](/help/assets/add-assets.md#asset-bulk-ingestor)を参照してください。

### [!DNL Assets] {#bug-fixes-assets}のバグ修正

* 権限が付与された複数のアセットをダウンロードしようとすると、著作権ページが表示されない。 (CQ-4314403)
* INDDファイルの編集を選択した場合、解像度が予期せず変更される。 (CQ-4317376)
* PDFレンダリングには、InDesignテンプレートの最後のページのみが含まれます。 (CQ-4317305)
* ピッカーが複雑なメタデータスキーマの一部である場合、タグピッカーが開くのに時間がかかります。 (CQ-4316426)
* 既存のファイル名と同じファイル名のアセットをアップロードする場合、名前の競合ダイアログが表示されず、バージョンの作成を促すメッセージが表示されません。 (CQ-4315424)
* フォルダーのメタデータプロパティは、フォルダーのプロパティページのポップアップメニューから設定および保存できます。 選択内容がリポジトリに保存されている間は、フォルダーメタデータプロパティを再度開いても表示されません。 (CQ-4314429)
* スペースや特殊文字を含むファイル名を持つアセットは、ブラウザーを使用してアップロードされます。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] として  [!DNL Cloud Service] {#forms}

AEM Formsは、多くの組織が長年にわたって素晴らしいオンボーディングや入学経験を提供するのを助けてきた。 これらのエクスペリエンスは、組織がリードを販売に転換したり、取り込んだ顧客データを処理したり、オーディエンスプロファイルに基づいてレスポンシブなエクスペリエンスを提供するのに役立っています。 現在、AEM Formsはクラウドサービスとして利用できます。

[AEM FormsをCloud Service](https://experienceleague.corp.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)として使用して、デジタルフォームの作成、既存のデータソースへのフォームの接続、Adobe Signとのフォームの統合、フォームへの電子署名の追加、レコードのドキュメント(DoR)の生成を行い、送信済みのフォームをPDFファイルとしてアーカイブできます。 また、このサービスでは、既存のPDF formsをデジタルフォームに変換することもできます。 標準的なAEM Formsの機能に加えて、自動拡張、アップグレードのダウンタイムゼロ、クラウドネイティブの開発環境など、クラウドネイティブの機能をいくつかオファーしています。 [このブログ記事](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html)を読み、Cloud ServiceとしてのAEM Formsの能力や特徴を知る。

デモを見るか、サービスに新規登録するには、Adobeの担当者にお問い合わせください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* Magento2.4.2のサポート

* 任意のコンテンツページで、製品詳細コンポーネントを使用および設定できるようになりました。

* 最新の CIF コアコンポーネント v1.9.0 を含んだ CIF Venia 参照サイト 2021.03.25 をリリースしました。詳しくは、[CIF Venia 参照サイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25)を参照してください。

* CIF コアコンポーネント v1.9.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0)を参照してください。


## Cloud Manager {#cloud-manager}

この節では、AEMのCloud ManagerのリリースノートをCloud Service2021.4.0および2021.3.0として概要を説明します。

### リリース日 {#release-date-cm-april}

AEMのCloud ManagerのCloud Service2021.4.0のリリース日は2021年4月8日です。
次回のリリースは2021年5月6日に予定されています。

### 新機能 {#what-is-new-april}

* UIが更新され、プログラムワークフロー追加と編集がより直感的になりました。

* 必要な権限を持つユーザーが、UIを介してコマースエンドポイントを送信できるようになりました。

* 環境変数は、作成者または発行の特定のサービスに対してスコープできるようになりました。 AEMバージョン`2021.03.5104.20210328T185548Z`以上が必要です。

* パイプラインが設定されていない場合でも、**Gitを管理**&#x200B;ボタンがパイプラインカードに表示されます。

* Cloud Managerで使用されるAEMプロジェクトのアーキタイプのバージョンが、バージョン27に更新されました。

* Cloud Managerで作成されたAdobe I/Oデベロッパーコンソールのプロジェクトを誤って編集または削除できなくなりました。

* ユーザが新しい環境を追加すると、環境が作成された後は、別の領域に移動できないという通知が表示されます。

* 環境変数は、作成者または発行の特定のサービスに対してスコープできるようになりました。 AEMバージョン2021.03.5104.20210328T185548Z以上が必要です。

* 環境が削除されたときにパイプラインを開始したときのエラーメッセージが明確になりました。

* Eclipseプロジェクトで提供されるOSGiバンドルは、ルール`CQBP-84--dependencies`から除外されるようになりました。

### バグ修正 {#bug-fixes-cm-april}

* パイプラインのエクスペリエンス監査ページを編集する際に、スラッシュ`( / )`で始まる入力パスによって、ステップが保留状態のままになることはなくなりました。

* 新しい実稼動パイプラインが作成された場合、コンテンツ監査の上書きがユーザーによって追加されない場合、デフォルトのホームページは監査されませんでした。

* `CloudServiceIncompatibleWorkflowProcess`の問題は、ダウンロード可能な雑誌号CSVファイル内で誤った重大度になっていました。

* `Runmode`チェックは、非フォルダーノードで偽陽性を生み出していました。


### リリース日 {#release-date-cm-march}

AEMのCloud ManagerのCloud Service2021.3.0のリリース日は2021年3月11日です。

### 新機能 {#what-is-new-march}

* [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL証明書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)、[カスタムドメイン名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)の既存のカスタムドメイン名を設定している環境のお客様は、既存の設定に関するメッセージを表示し、UIを使用して自己提供できます。

* 必要な権限を持つユーザーは、プログラムを編集でき、セルフサービスの方法で次の操作を行うことができます。

   * ア追加セットを持つ既存のプログラムに対するサイトソリューション、またはアセットを持つ既存のに対するサイトソリューション。
   * サイトとアセットの両方を含む既存のプログラムからサイトまたはアセットを削除します。
   * 2つ目追加は、使用されていないソリューションのエンタイトルメントを既存のプログラムに対して、または新しいプログラムとして使用することです。

* **パイプライン実行画面とアクティビティ** 画面の両方にAEM Push  *Updatelabelが表示されるようにな*  ** りました。

* 環境が休止状態になっているが、AEMの更新も使用可能な場合、**Hibernated**&#x200B;ステータスは&#x200B;**Update available**&#x200B;よりも優先されます。

* 統合シェルのユーザープロファイルアイコン（右上）に移動した後、「表示Cloud Managerロール」オプションを選択すると、Cloud Managerロールを表示できるようになりました。

* ラベル&#x200B;**承認申請**&#x200B;が&#x200B;**実稼動承認**&#x200B;にラベル変更され、より明確になりました。

* **バージョン**&#x200B;ラベルが、実稼動パイプライン実行画面の&#x200B;**Gitタグ**&#x200B;に再ラベル付けされました。

* 重要な指標が定義されたしきい値を満たさない場合の動作を定義するラベルは、その真の動作を反映するために再ラベル付けされています。**すぐにキャンセル**&#x200B;と&#x200B;**すぐに承認**。

* AEMCloud ServiceSDKのバージョン`2021.3.4997.20210303T022849Z-210225`に基づいて、クラスとメソッドの非推奨リストが更新されました。

* Cloud Manager実稼動パイプラインに、[カスタムUIテスト](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)機能が追加されました。

### バグ修正 {#bug-fixes-cm-march}

* AEMのプッシュアップグレード中に、パッケージのバージョン管理がスキップされる場合がありました。

* 他のパッケージにパッケージが埋め込まれた場合に、品質の問題が正しく検出されない場合がありました。

* 不明確な状況では、プログラムダイアログを開いたときに生成される追加デフォルトのプログラム名は、既存のプログラム名の重複の場合があります。

* 場合によっては、パイプラインの開始直後にパイプラインの実行ページから移動すると、実際に実行が開始したにもかかわらず、アクションが失敗したことを示すエラーメッセージが表示されます。

* お客様のビルドで無効なパッケージが生成された場合、ビルド手順が不必要に再開されました。

* 場合によっては、IP許可リストの横に緑色の「アクティブ」ステータスが表示される場合があります。このステータスは、その設定が展開されていない場合でも表示されます。

* 「エクスペリエンス監査」ステップで既存のすべての実稼働パイプラインが自動的に有効になります。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

コンテンツ転送ツールv1.3.4のリリース日は2021年3月20日です。

### バグ修正 {#bug-fixes-ctt}

* CTTが、同じ名前で名前にハイフンが含まれるフォルダーからコンテンツをスキップしていました。 この問題が修正されました。

### リリース日 {#release-date-ctt-march}

コンテンツ転送ツールv1.3.0のリリース日は2021年3月4日です。

### コンテンツ転送ツールの新機能{#what-is-new-ctt-march}

* CTTは、`/libs`の代わりに`/apps`にインストールされるようになりました。特定のページへのブラウザーのブックマークが無効になる場合があります。
* CTTがインストールされている場合、ユーザーはコンテンツ転送ページに移動するために別のレベルに移動する必要があります。 詳しくは、[コンテンツ転送ツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html)を参照してください。

### バグ修正 {#bug-fixes-ctt-march}

* 特定のパスからコンテンツを移行する際に、CTTは関連のないリソースを取り込んでいました。 修正済み

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.12のリリース日は2021年4月12日です。

### バグ修正 {#bug-fixes-bpa-april}

* BPAレポートで重複行が見つかりました。 この問題が修正されました。
* AEMバージョン6.4.2のBPA UIで、「レポートの生成」ボタンを無効にしていたJSエラーが発生していました。 修正済み


## コードリファクタリングツール {#code-refactoring-tools}

### コードリファクタリングツールの新機能{#what-is-new-crt}

* Repository Modernizerの新機能および機能強化。 [GitHubリソースを参照：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)を参照してください。
   * OSGi設定（RepoInit設定を除く）を推奨の.cfg.json形式に正規化します。
   * OSGi configフォルダの名前を指定した形式に変更します。
   * ui.apps.structureプロジェクトを生成します。
   * 分析モジュールを作成します。

* Dispatcher Converterの新機能および機能強化です。 [GitHubリソースを参照：ディスパッチャーコンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * コンテンツのライニングの代わりに、異なる挿入用に別々のファイルを作成する。
   * vhostsのフォルダーパスとvhostファイルへのパスの両方を処理できます。
   * 600件以上の範囲の大規模な顧客構成を持つファーム・ファイルの生成
