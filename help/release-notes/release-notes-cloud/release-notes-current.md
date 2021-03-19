---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
translation-type: tm+mt
source-git-commit: 93ae24247ae36f44e659211f1e7ab2f0888e4ad6
workflow-type: tm+mt
source-wordcount: '1793'
ht-degree: 19%

---


# Cloud Service{#release-notes}としての[!DNL Adobe Experience Manager]の最新のリリースノート

次の節では、Cloud Serviceとしての[!DNL Experience Manager]の最新（最新）版のリリースノートの概要を説明します。

>[!NOTE]
>ここから、以前のバージョンのリリースノートに移動できます。例えば、2020年、2021年などの場合、

>[!NOTE]
>
>リリースに直接関連しないドキュメントの更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 のリリース日は 2021 年 2 月 25 日です。次のリリース(2021.3.0)は、2021年3月25日に予定されています。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[RemotePage コンポーネント](/help/implementing/developing/hybrid/remote-page.md)**：AEM 内で外部 SPA を表示および編集できるようになりました。

* **[AEM 内での外部 SPA の編集](/help/implementing/developing/hybrid/editing-external-spa.md)**：AEM インスタンスへのスタンドアロン単一ページアプリケーションのアップロード、編集可能なコンテンツセクションの追加、オーサリングの有効化が可能になりました。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] の新機能 {#what-is-new-assets}

* [!DNL Experience Manager Assets] の値 [!DNL Cloud Service] は、事前設定済み [!DNL Brand Portal] インスタンスを持つ権利が付与されます。[!DNL Cloud Manager]ユーザーは、[!DNL Experience Manager Assets]の[!DNL Brand Portal]を[!DNL Cloud Service]としてアクティベートできます。 「[ブランドポータルのアクティブ化](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en)」を参照してください。

* [!DNL Brand Portal]を使用してアセットのソースを行えるようになりました。 アセットソーシング機能は、[!DNL Brand Portal]を活用して、新しいマーケティングキャンペーン、フォトシュート、プロジェクトのソースアセットに対して、顧客がエージェンシーユーザーと関わるよう支援します。 [ [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)のアセットソーシングを参照してください。

* [!DNL Brand Portal]使用状況レポートには、アクティブなユーザーのみが表示されるようになりました。 非アクティブなユーザーは現在表示されません。 アクティブユーザーとは、[!DNL Admin Console]内の製品プロファイルにアカウントが割り当てられているユーザーです。 [[!DNL Brand Portal] レポート](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html)を参照してください。

* [!DNL Brand Portal]には、新しいダウンロード設定が導入されています。この設定を使用すると、フォルダーやコレクションなどをダウンロードする際に、アセットごとに個別のフォルダーを作成できます。 [ダウンロード設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)を参照してください。

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## [!DNL Assets] {#bug-fixes-assets}のバグ修正

* 名前の競合を解決した後に既存のアセットの新しいバージョンを作成すると、元のアセットのメタデータが上書きされます。 (CQ-4313594)
* 注釈テキストが長いアセットを印刷すると、空白がある場合でも、注釈テキストはトリミングされます。 (CQ-4314101)
* 複数のアセットを選択してプロパティを更新すると、エラーが発生したり、選択解除されたアセットのプロパティが更新されたりする場合があります。 (CQ-4316532)
* [!UICONTROL アセット管理者の検索レール]を開こうとすると、ページは空白のままになり、[!UICONTROL 編集]/[!UICONTROL 設定]をクリックするとエラーが発生します。 (CQ-4315079)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新機能 {#what-is-new-commerce}

* 製品エクスペリエンス管理：エクスペリエンスフラグメントを使用して、商品カタログページを個別に拡張する。

* 関連するコンテンツにすばやく移動するアクションなど、アセットとエクスペリエンスフラグメントのリンクを表示するための製品コンソールプロパティが拡張されました。

* 最新の CIF コアコンポーネント v1.8.0 を含んだ CIF Venia 参照サイト 2021.02.24 をリリースしました。詳しくは、[CIF Venia 参照サイト](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24)を参照してください。

* CIF コアコンポーネント v1.8.0 をリリースしました。詳しくは、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0)を参照してください。

## Cloud Manager {#cloud-manager}

この節では、AEMのCloud ManagerのリリースノートをCloud Service2021.3.0として概要を説明します。

## リリース日 {#release-date-cm-march}

AEMのCloud ManagerのCloud Service2021.3.0のリリース日は2021年3月11日です。
次回のリリースは2021年4月8日に予定されています。


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


### リリース日 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

### 新機能 {#what-is-new-cloud-manager}


* アセットのお客様は、Cloud Manager UIを使用してセルフサービスの方法でBrand Portalインスタンスをいつ、どこにデプロイするかを選択できるようになります。 アセットソリューションを使用する通常の（Sandbox以外の）プログラムの場合、Brand Portalを実稼働環境でプロビジョニングできるようになりました。 プロビジョニングは、実稼働環境で1回だけ実行できます。

* プロジェクトとサンドボックスの作成で使用されるAEMプロジェクトアーキタイプがバージョン25に更新されました。

* コードスキャン中に特定された非推奨のAPIのリストが絞り込まれ、最新Cloud ServiceのSDKリリースで非推奨となった追加のクラスとメソッドが含まれるようになりました。

* SonarQubeプロファイル（Cloud Manager用）が更新され、squid:S2142というSonarルールが削除されました。 これは、スレッド割り込みチェックと競合しなくなります。

* Cloud Manager UIは、ドメイン名を一時的に追加/更新できない可能性があるユーザーに通知します。関連付けられた環境には実行中のパイプラインが割り当てられているか、現在、承認手順を待機中です。

* sonarのプリフィックスが付いた顧客`pom.xml`ファイルに設定されたプロパティは、ビルドおよび品質スキャンの失敗を回避するために、動的に削除されるようになりました。

* Cloud Manager UIには、現在展開中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* Cloud Serviceの互換性の問題をカバーするため、コード品質ルールが追加されました。

### バグ修正 {#bug-fixes-cloud-manager}

* ドメイン名に対するSSL証明書の一致で、大文字と小文字が区別されなくなりました。

* 証明書の秘密鍵が2048ビットの制限を満たさない場合に、適切なエラーメッセージが表示されるように、Cloud Manager UIからユーザーに通知されるようになりました。

* Cloud Manager UIには、現在デプロイ中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* 場合によっては、内部の問題が原因で環境の削除が停止することがあります。

* 一部のパイプラインエラーは、誤ってパイプラインエラーとして報告されました。

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


### リリース日 {#release-date-ctt-feb}

コンテンツ転送ツールv1.2.4のリリース日は2021年2月10日です。

### バグ修正 {#bug-fixes-ctt-feb}

* 複数のユーザーをマッピングする際に、一部のユーザーのIMS IDが正しくマッピングされない問題を修正しました。 この問題が修正されました。

### リリース日 {#release-date-ctt-feb01}

コンテンツ転送ツール v1.2.2 のリリース日は 2021 年 2 月 1 日です。

### コンテンツ転送ツールの新機能{#what-is-new-ctt}

* コンテンツ転送ツールに、新しい機能および UI であるユーザーマッピングツールが追加されました。この機能は、コンテンツ移行アクティビティの一環として、既存のユーザーおよびグループをそれぞれの Adobe Identity Management System ID に自動的にマッピングします。詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)を参照してください。
* コンテンツ転送ツールは、移行セットで参照されているすべてのグループとユーザーを子も含めて移行するようになりました。
* 移行セットの作成時に、`/etc` 下の特定のパスを選択できます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.2のリリース日は2021年2月19日です。

### ベストプラクティスアナライザの新機能{#what-is-new-bpa}

* AEM FormsとAEM Formsの導入の使用を検出し、AEM Formsへの移行に関連する領域をCloud Serviceとして示す機能。
* カスタムコンポーネントとテンプレートの使用状況と数を検出し、レポートする機能。
* 使用するノードストアとデータストアの種類を検出する機能。
* Dynamic Mediaの使い方を検出する能力。
* 使用するJavaバージョンの検出機能。

## コードリファクタリングツール {#code-refactoring-tools}

### コードリファクタリングツールの新機能{#what-is-new-crt}

* AIO-CLI プラグインの新しいバージョンがリリースされました。このプラグインの最新バージョンには、Repository ModenizerとDispatcher Converterの新機能とバグ修正が含まれています。    このプラグインの詳細については、[統合エクスペリエンス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=ja#benefits)を参照してください。

* Repository Modernizerの新機能および機能強化。 [GitHubリソースを参照：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)を参照してください。
   * OSGi設定（RepoInit設定を除く）を推奨の.cfg.json形式に正規化します。
   * OSGi configフォルダの名前を指定した形式に変更します。
   * ui.apps.structureプロジェクトを生成します。
   * 分析モジュールを作成します。

* Dispatcher Converterの新機能および機能強化です。 [GitHubリソースを参照：ディスパッチャーコンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * コンテンツのライニングの代わりに、異なる挿入用に別々のファイルを作成する。
   * vhostsのフォルダーパスとvhostファイルへのパスの両方を処理できます。
   * 600件以上の範囲の大規模な顧客構成を持つファーム・ファイルの生成

## [!DNL Adobe Experience Manager] Cloud Service財団として  {#aem-as-a-cloud-service-foundation}

### 既知の問題 {#known-issues-foundation}

**Build Analyzer Pluginの問題が原因で、一部のビルドが失敗する場合があります**

`aemanalyser-maven-plugin`の実行中にプロジェクトのビルドが失敗し、次のエラーメッセージが表示される場合があります。

```
[ERROR] repoinit: Parsing error in repoinit from extension : Encountered "" at line 15, column 37.
 
Was expecting one of:
 
     
 
[ERROR] Analyser detected errors on feature
```

**対処方法**

この問題を回避するには、親`pom.xml`ファイルの`aemanalyser-maven-plugin`の最新バージョンを選択します。

```xml
<aemanalyser.version>0.9.2</aemanalyser.version>
```

