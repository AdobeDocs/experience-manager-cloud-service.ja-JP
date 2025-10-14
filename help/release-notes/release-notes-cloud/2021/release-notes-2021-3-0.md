---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 リリースのリリースノート。'
description: 「[!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 のリリースノート」
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 88%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>ここからは、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 のリリース日は 2021 年 3 月 25 日です。次回のリリース（2021.4.0）は、2021 年 4 月 29 日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* 簡単な設定で、[プログレッシブ web アプリ（PWA）版のサイト](/help/sites-cloud/authoring/sites-console/enable-pwa.md)がプロジェクトレベルで有効化できるようになりました。
* コンテンツフラグメントモデルの拡張 - 複数行テキストデータタイプを複数フィールドリストとして定義できるようになりました。
* コンテンツフラグメントエディターの UX の強化 - パンくずリストにネストされた子フラグメントが表示され、公開、保存、保存および終了のアクションの表示が改善されました。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] は、Connected Assets 機能を拡張して、サポートされるコアコンポーネントでの [!DNL Dynamic Media] 画像の使用をサポートします。「[Connected Assets の使用](/help/assets/use-assets-across-connected-assets-instances.md)」を参照してください。
* Experience Manager 管理者は、特定の日時に一括アセット取得のスケジュールを設定できます。また、管理者は、日時に基づいて定期的な取得のスケジュールを設定できます。「[一括アセット取得](/help/assets/add-assets.md#asset-bulk-ingestor)」を参照してください。

### [!DNL Assets] のバグ修正  {#bug-fixes-assets}

* 権限が管理された複数のアセットのダウンロードを試行している際には著作権ページが表示されません。（CQ-4314403）
* INDD ファイルの編集を選択した場合、解像度が予期せず変更されます。（CQ-4317376）
* PDF レンディションには、InDesign テンプレートの最後のページのみが含まれます。（CQ-4317305）
* ピッカーが複雑なメタデータスキーマに含まれている場合、タグピッカーが開くのに時間がかかります。（CQ-4316426）
* 既存のファイル名と同じファイル名を持つアセットをアップロードする場合、名前の競合ダイアログが表示されず、バージョンを作成するように求められます。（CQ-4315424）
* フォルダーメタデータのプロパティは、フォルダーのプロパティページのポップアップメニューから設定および保存できます。 選択内容はリポジトリに保存されている間、フォルダーメタデータプロパティを再度開いても表示されません。（CQ-4314429）
* スペースや特殊文字を含むファイル名を持つアセットは、ブラウザーを使用してアップロードされます。（CQ-4318381）

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms は、長年にわたって、優れたオンボーディングと登録のエクスペリエンスの提供で、多くの組織を支援してきました。これらのエクスペリエンスは、組織がリードを売上にコンバージョンしたり、取得した顧客データを処理したり、オーディエンスプロファイルに基づいてレスポンシブなエクスペリエンスを提供するのに役立っています。現在、AEM Forms はクラウドサービスとして提供されています。

[AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html?lang=ja) を使用して、デジタルフォームを作成したり、フォームを既存のデータソースに接続したり、フォームを Adobe Sign と統合して電子サインをフォームに追加したり、送信されたフォームを PDF ファイルとしてアーカイブするためにレコードのドキュメント（DoR）を生成したりできます。また、既存の PDF フォームをデジタルフォームに変換することもできます。このサービスは、AEM Formsの標準的な機能に加えて、自動スケーリング、アップグレードのダウンタイムゼロ、クラウドネイティブ開発環境など、いくつかのクラウドネイティブ機能を提供します。

デモが必要な場合は、アドビ担当者に問い合わせるか、サービスに登録してください。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* Adobe Commerce 2.4.2 のサポート

* 製品の詳細コンポーネントを任意のコンテンツページで使用および設定できるようになりました。

* 最新のCIF コアコンポーネント v1.9.0 を含んだCIF Venia 参照サイト 2021.03.25 をリリースしました。詳しくは、[CIF Venia 参照サイト &#x200B;](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) を参照してください。

* CIF コアコンポーネント v1.9.0 をリリースしました。詳しくは、[CIF コアコンポーネント &#x200B;](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) を参照してください。


## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.3.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-march}

AEM as a Cloud Service 2021.3.0 の Cloud Manager のリリース日は 2021 年 3 月 11 日です。
次回のリリースは 2021 年 4 月 8 日に予定されています。

### 新機能 {#what-is-new-march}

* [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)、[SSL 証明書 &#x200B;](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)、[&#x200B; カスタムドメイン名 &#x200B;](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) に既存のカスタムドメイン名がある環境のユーザーは、既存の設定に関するメッセージを確認し、ユーザーインターフェイスを介してセルフサービス方式で操作できます。

* 必要な権限を持つユーザーがプログラムを編集して、セルフサービス方式で以下を行えるようになりました。

   * Assets を使用している既存のプログラムに Sites ソリューションを追加する（およびその逆の動作）。
   * Sites と Assets の両方を使用している既存のプログラムから Sites または Assets を削除する。
   * 使用されていない 2 つ目のソリューション使用権限を既存のプログラムに追加するか、新しいプログラムとして追加する。

* *パイプラインの実行*&#x200B;画面と&#x200B;*アクティビティ*&#x200B;画面の両方に **AEM プッシュアップデート**&#x200B;ラベルが表示されるようになりました。

* 環境が休止状態になっている場合は、AEM アップデートが使用可能でも、**休止状態**&#x200B;ステータスが&#x200B;**アップデート利用可能**&#x200B;ステータスより優先されます。

* 統合シェルのユーザープロファイルアイコン（右上）に移動した後、「Cloud Manager の役割を表示」オプションを選択すると、Cloud Manager の役割が表示されるようになりました。

* **アプリケーションの承認**&#x200B;ラベルが&#x200B;**実稼動の承認**&#x200B;ラベルに変更され、意味がより明確になりました。

* 実稼動パイプラインの実行画面の&#x200B;**バージョン**&#x200B;ラベルが **Git タグ**&#x200B;ラベルに変更されました。

* 重要な指標が定義済みのしきい値を満たさない場合の動作を定義するラベルが、その実際の動作を反映するように変更されました（**ただちにキャンセルする**&#x200B;と&#x200B;**ただちに承認する**）。

* AEM Cloud Service SDK のバージョン `2021.3.4997.20210303T022849Z-210225` に基づいて、クラスとメソッドの廃止リストが更新されました。

* Cloud Manager の実稼働パイプラインに[カスタム UI テスト](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)機能が追加されました。

### バグの修正 {#bug-fixes-cm-march}

* AEM プッシュアップグレード時に、パッケージバージョン管理がスキップされる場合がありました。

* パッケージが他のパッケージに埋め込まれている場合に、品質の問題が正しく検出されないことがありました。

* プログラムを追加ダイアログを開いたときに生成されるデフォルトのプログラム名が、既存のプログラム名と重複する場合がありました。

* パイプラインの開始直後にパイプラインの実行ページから移動すると、実際には実行が開始したにもかかわらず、アクションが失敗したという内容のエラーメッセージが表示される場合がありました。

* ユーザービルドの結果、無効なパッケージが生成された場合、ビルドステップが不必要に再開されていました。

* 該当する設定がデプロイされていない場合でも、IP 許可リストの横に緑色の「アクティブ」ステータスが表示される場合がありました。

* 既存のすべての実稼動パイプラインは、エクスペリエンス監査の手順で自動的に有効になります。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.3.4 のリリース日は 2021 年 3 月 19 日です。

### バグの修正 {#bug-fixes-ctt}

* CTT が、名前が同じでも、名前にハイフンを含むフォルダーのコンテンツをスキップしていた問題を修正しました。この問題が修正されました。

### リリース日 {#release-date-ctt-march}

コンテンツ転送ツール v1.3.0 のリリース日は 2021 年 3 月 4 日です。

### コンテンツ転送ツールの新機能 {#what-is-new-ctt-march}

* コンテンツ転送ツール（CTT）は、`/libs` ではなく `/apps` にインストールされるようになりました。特定のページへのブラウザーブックマークが無効になる可能性があります。
* CTT がインストールされている場合、ユーザーはコンテンツ転送ページにアクセスするために、さらにレベルを移動する必要があります。詳しくは、[コンテンツ転送ツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja)を参照してください。

### バグの修正 {#bug-fixes-ctt-march}

* 特定のパスからコンテンツを移行する際に、CTT が無関係なリソースを取り込んでいました。この問題が修正されました。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.8 のリリース日は 2021 年 3 月 22 日です。

### ベストプラクティスアナライザーの新機能 {#what-is-new-bpa}

* ユーザーインターフェイスの BPA レポートと、CSV ファイルとして書き出されたレポートから、ACS Commons の結果を除外する機能。

## コードリファクタリングツール {#code-refactoring-tools}

### コードリファクタリングツールの新機能 {#what-is-new-crt}

* Repository Modernizer の新機能と機能強化は次のとおりです。最新バージョンについては、[GitHub リソース：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) を参照してください。
   * OSGi 設定（repoinit 設定を除く）を、推奨の .cfg.json 形式に正規化します。
   * OSGi 設定フォルダーの名前を指定の形式に変更します。
   * ui.apps.structure プロジェクトを生成します。
   * 分析モジュールを作成します。

* Dispatcher コンバーターの新機能と機能強化は次のとおりです。詳しくは、「[GitHub リソース：Dispatcher コンバーター &#x200B;](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)」を参照してください。
   * 異なるインクルージョンに対して、コンテンツをインライン化するのではなく別個のファイルを作成します。
   * vhosts のフォルダーパスと vhost ファイルのパスを両方とも処理できます。
   * 600 件以上の大規模な顧客設定を持つファームファイルを生成できます。
