---
title: ルールセットを使用した URL の変換
description: Dynamic Media でルールセットをデプロイして、URL を変換する方法を説明します。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。
contentOwner: Rick Brough
feature: Rulesets,Troubleshooting,Upload,Best Practices
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: a495178529a0a4229095ea3a11f52b376c81715b
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 92%

---

# ルールセットを使用した URL の変換 {#using-rulesets-to-transform-urls}

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

Dynamic Media でルールセットをデプロイして、URL を変換できます。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。各ルールは、1 つ以上の条件と 1 つ以上のアクションで構成されます。ルールは、XML データを条件に対して評価し、条件が満たされている場合は適切なアクションを実行します。ルールセットの例には、次のようなものがあります。

* MIME タイプのサフィックスの追加。多くのサービスや Web サイトでは、`.jpg` を URL に付加するなど、画像のサフィックスが必要です。
* SEO（検索エンジン最適化）のための URL へのフォルダーパスの作成。

  「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/dynamic-media/assets/s7_seo.pdf)」を参照してください。

* SEO（検索エンジン最適化）のための URL へのメタデータの付加。

  「[Adobe Dynamic Media Classic が SEO をサポートする方法](/help/assets/dynamic-media/assets/s7_seo.pdf)」を参照してください。

* ダウンロードを開始するための Content Disposition の設定。
* パーソナライゼーションのための画像サービングテンプレート URL の簡略化。例えば、`rgb{XX,YY,ZZ}` を RTF 対応の `\redXX\greenYY\blueZZ` に変換します。

* `$`、`{`、`}` などの特定の文字のエンコードと、ImageServer への特定の文字のデコードのリクエスト。例えば、Facebook は特殊文字を含む URL では正しく機能しません。

Dynamic Media のコンテキストで、XML ベースのシステムを使用してアセット情報を管理する web サイトは、XML ファイルを Dynamic Media にアップロードできます。これらのファイルのいずれかを、Dynamic Media のアセットを処理するための前処理ルールセットファイルとして指定できます。このファイルは、Dynamic Media と統合するシステムの会社ロジックを満たすよう、標準 URL プロトコル形式を再構成します。XML ファイルをルールセット定義ファイルのパスとして指定します。

>[!CAUTION]
>
>ルールセットを使用する場合は、Dynamic Media のコンテンツが Web サイトに表示されなくなる可能性があるので、注意してください。

用意されているサンプルルールセットを使用して、独自のルールセットを作成できます。[ルールセットのリファレンス](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference)を参照してください。

すべてのルールセットの作成と同様に、xmlvalid などの XML バリデータープログラムを使用して XML ファイルをアップロードする前に、XML ファイルが有効であることを確認します。

また、最初は実稼動環境に影響を与えないステージング環境でルールセットをテストしてください。通常、実稼動環境とステージング環境では異なるログイン情報が必要となります。

ログイン情報については、[Adobe Dynamic Media Classic へのログイン](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out)を参照してください。

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->



## XML ルールセットのデプロイ {#deploy-xml-rule-sets}

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、カスタマーサポートにお問い合わせください。

1. 次の手順を実行して、ルールセットファイルをアップロードします。

   * グローバルナビゲーションバーの「**[!UICONTROL アップロード]**」を選択します。
   * **[!UICONTROL アップロード]**&#x200B;ページで、左上隅付近の「**[!UICONTROL 参照]**」を選択します。
   * **[!UICONTROL 開く]**&#x200B;ダイアログボックスで、ルールセットファイル（XML）を参照します。
   * ファイルを選択して、「**[!UICONTROL 開く]**」を選択します。
   * **[!UICONTROL アップロード]**&#x200B;ページの右側で、ルールセットファイルの公開先フォルダーを選択します。
   * ページ下部付近の「アップロード後に公開」が選択されていることを確認します。
   * ページの右下隅の「**[!UICONTROL アップロードを送信]**」を選択します。
   * グローバルナビゲーションバーの「**[!UICONTROL ジョブ]**」を選択して、アップロードジョブのステータスを確認します。**[!UICONTROL ジョブ]**&#x200B;ページの「**[!UICONTROL ステータス]**」列に「アップロード完了」と表示されたら、次のステップに進みます。

1. ページ上部付近のナビゲーションバーで、**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 公開設定]**／**[!UICONTROL Image Server]** に移動します。
1. **[!UICONTROL Image Server 公開]**&#x200B;ページの「**[!UICONTROL カタログ管理]**」グループで、**[!UICONTROL ルールセット定義ファイルのパス]**&#x200B;を探し、「**[!UICONTROL 選択]**」を選択します。
1. **[!UICONTROL ルールセット定義ファイル（XML）を選択]**&#x200B;ページでルールセットファイルを参照し、ページ右下隅の「**[!UICONTROL 選択]**」を選択します。
1. セットアップページの右下隅にある「**[!UICONTROL 閉じる]**」を選択します。
1. Image Server 公開ジョブを実行します。

   ルールセットの条件が、現在の Dynamic Media の Image Server へのリクエストに適用されます。

   ルールセットファイルを変更した場合、変更したルールセットファイルを再アップロードして再公開すると、変更内容が直ちに適用されます。
