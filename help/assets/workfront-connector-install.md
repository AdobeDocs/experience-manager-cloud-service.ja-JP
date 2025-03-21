---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 96%

---

# [!DNL Workfront for Experience Manager enhanced connector] のインストール  {#assets-integration-overview}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

拡張コネクタのインストールは、[!DNL Cloud Service] として [!DNL Adobe Experience Manager] への管理者アクセス権を持つユーザーが行います。インストールする前に、プラットフォームのサポートとコネクタのその他の [前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience) を確認してください。

>[!IMPORTANT]
>
>2022年6月に、アドビは Workfront と Adobe Experience Manager Assets as a Cloud Service を接続するための新しいネイティブ統合をリリースしました。この統合は、これら 2 つのソリューションを接続するために必須の方法となりました。Workfront と AEM Assets as a Cloud Service を接続する拡張コネクタ（1.9.8 以降）の今後の新しい実装は、ブロックされます。この統合の設定方法について詳しくは、[Experience Manager Assets as a Cloud Service 統合の設定](workfront-connector-configure.md)を参照してください。

>[!IMPORTANT]
>
>* Adobeは、認定パートナーまたは [!DNL Adobe Professional Services] を介してのみ [!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと構成を必要とします。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* アドビでは、拡張コネクタバージョン 1.7.4 以降をサポートしています。以前のプレリリースバージョンやカスタムバージョンはサポートされていません。拡張コネクタのバージョンを確認するには、[拡張コネクタのインストール手順](workfront-connector-install.md)の手順 5(a) を参照してください。
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、[試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)を参照してください。

コネクタをインストールする前に、次のプリインストール手順に従います。

1. AEM as a Cloud Service プログラムで高度なネットワークを設定し、IP 許可リストへの登録を有効にしている場合は、Workfront IP をこの許可リストに追加して、イベント購読と様々な API 呼び出しが AEM に渡されるようにする必要があります。

   * [Workfront クラスター IP](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=ja#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9)。[!DNL Workfront] の IP クラスターを調べるには、**[!UICONTROL 設定]**／**[!UICONTROL システム]**／**[!UICONTROL 顧客情報]**&#x200B;に移動します。

   * [Workfront イベント購読 API の IP](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html?lang=ja)

   >[!IMPORTANT]
   >
   >* お使いのプログラム用に詳細設定がされており、IP 許可リストへの登録を使用している場合は、拡張 Workfront コネクタアーキテクチャの制限により、プログラムのエグレス IP を Cloud Manager の許可リストに追加する必要もあります。
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* プログラムの IP を見つけるには、ターミナルウィンドウを開き、次のようなコマンドを実行します。
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >    ```

1. 次のオーバーレイが [!DNL Experience Manager] リポジトリに存在しないことを確認してください。これらのパスに既にオーバーレイが存在する場合は、オーバーレイを削除するか、2 つのパス間の変更の差分を結合する必要があります。

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. このインストールを行うには、[!DNL Experience Manager] の Maven プロジェクトを [!DNL Cloud Service] として設定するための知識が必要です。次のリソースを使用して、Maven プロジェクトにサードパーティパッケージを含める方法を理解します。

   * [Maven プロジェクトにサードパーティパッケージを含める](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#including-third-party)。
   * [でのデプロイ [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja)。

アドオンを [!DNL Experience Manager] に [!DNL Cloud Service] としてインストールするには、次の手順に従います。

1. [アドビのソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)から拡張コネクタをダウンロードします。

1. Cloud Manager から AEM as a Cloud Service リポジトリーに[アクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=ja)し、クローンを作成します。

1. 任意の IDE を使用して、AEM as a Cloud Service リポジトリーのクローンを開きます。

1. 手順 1 でダウンロードした拡張コネクタの zip ファイルを次のパスに配置します。

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >`resources` フォルダーが存在しない場合は作成します。


1. `pom.xml` 依存関係を追加します。

   1. 親 `pom.xml` に依存関係を追加します。

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >依存関係を親 `pom.xml` にコピーする前に、拡張コネクタのバージョン番号を必ず更新してください。

   1. `all module pom.xml` に依存関係を追加します。

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. `pom.xml` 埋め込みを追加します。すべてのサブプロジェクトの `pom.xml` の `embeddeds` セクションに [!DNL Workfront for Experience Manager enhanced connector] パッケージを追加します。すべてのモジュール `pom.xml` に組み込む必要があります。

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   埋め込みセクションのターゲットが `/apps/<path-to-project-install-folder>/install` に設定されます。JCR パス `/apps/<path-to-project-install-folder>` を、`all/src/main/content/META-INF/vault/filter.xml` ファイルのフィルタールールに含める必要があります。リポジトリーのフィルタールールは、通常、プログラム名から派生します。フォルダーの名前を既存ルールのターゲットとして使用します。

1. 変更をリポジトリーにプッシュします。

1. パイプラインを実行して、[変更内容を Cloud Manager にデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=ja)します。

1. システムユーザー設定を作成するには、[!DNL Experience Manager] ユーザーグループに `wf-workfront-users` を作成し、権限 `jcr:all` を `/content/dam` に割り当てます。システムユーザー `workfront-tools` が自動的に作成され、必要な権限が自動的に管理されます。拡張コネクタを使用する [!DNL Workfront] のすべてのユーザーは、このグループの一員として自動的に追加されます。

以前のバージョンから最新のバージョンに [!DNL Workfront for Experience Manager enhanced connector] を更新するための情報は、[こちら](update-workfront-enhanced-connector.md)にあります。

## [!DNL Experience Manager] 間の接続を [!DNL Cloud Service] と [!DNL Workfront] のように設定します。 {#configure-connection}

[!DNL Workfront] との接続を作成するには、次の手順に従います。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Workfront ツール設定]** を選択します。 

1. 左パネルで `workfront-tools` を選択し、ページの右上の領域にある「**[!UICONTROL 作成]** 」オプションを選択します。

1. **[!UICONTROL Workfront 接続]**&#x200B;ダイアログで、[!DNL Workfront] デプロイメントの必須の詳細事項を入力して、「**[!UICONTROL Workfront に接続]**」オプションを選択します。正常に接続されると、[!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境に自動的に作成されます。

   ![[!DNL Experience Manager] と [!DNL Workfront]](/help/assets/assets/wf-connection-config.png) の接続

1. 「**[!UICONTROL 詳細]**」タブに移動し、「**[!UICONTROL Is the Server AEM as a Cloud Service]**」オプションを選択します。
