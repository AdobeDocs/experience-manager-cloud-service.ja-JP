---
title: ルールセットを使用した URL の変換
description: Dynamic Media でルールセットをデプロイして、URL を変換できます。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# ルールセットを使用したURLの変換 {#using-rulesets-to-transform-urls}

Dynamic Media でルールセットをデプロイして、URL を変換できます。ルールセットはスクリプティング言語（JavaScript など）で記述された命令セットで、XML データを評価して、そのデータが特定の条件を満たす場合に特定のアクションを実行します。各ルールは、1 つ以上の条件と 1 つ以上のアクションで構成されます。ルールは XML データを条件に対して評価し、条件を満たしている場合は適切なアクションを実行します。ルールセットの例としては、次のようなものがあります。

* MIME タイプのサフィックスの付加。Many services and websites require image suffixes, such as adding `.jpg` to a URL.
* SEO（検索エンジン最適化）のための URL へのフォルダーパスの作成。

   [Adobe Scene7 Publishing System による SEO のサポート](/help/assets/dynamic-media/assets/s7_seo.pdf)を参照してください。

* SEO（検索エンジン最適化）のための URL へのメタデータの付加。

   [Adobe Scene7 Publishing System による SEO のサポート](/help/assets/dynamic-media/assets/s7_seo.pdf)を参照してください。

* ダウンロードを開始するためのコンテンツ処理方法の設定。
* パーソナライゼーションのための画像サービングテンプレーティング URL の簡略化。例えば、RTF対応 `rgb{XX,YY,ZZ}` ファイルに変換します。 `\redXX\greenYY\blueZZ`

* Request certain characters to be encoded such as `$`, `{`, and `}`, and certain characters to be decoded toward ImageServer. 例えば、Facebook は特殊文字を含む URL では正しく機能しません。

   [URL からの特殊文字の削除](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)を参照してください。

Dynamic Media のコンテキストで、XML ベースのシステムを使用してアセット情報を管理する Web サイトは、XML ファイルを Dynamic Media にアップロードできます。これらのファイルのいずれかを、Dynamic Media のアセットを処理するための前処理ルールセットファイルとして指定できます。このファイルは、Dynamic Media と統合するシステムのビジネスロジックを満たすよう、標準 URL プロトコル形式を再構成します。XML ファイルをルールセット定義ファイルのパスとして指定します。

>[!CAUTION]
>
>ルールセットを使用する場合は注意が必要です。ダイナミックメディアコンテンツがWebサイトに表示されないようにすることができます。

用意されているサンプルルールセットを使用して、独自のルールセットを作成できます。[ルールセットのリファレンス](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/c_rule_set_reference.html)を参照してください。

すべてのルールセットの作成と同様に、xmlvalid などの XML バリデータープログラムを使用して、XML ファイルが有効であることを確認してからアップロードしてください。[ルールセットのトラブルシューティング](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)も参照してください。

また、最初は実稼動環境に影響を与えないステージング環境でルールセットをテストしてください。通常、実稼動環境とステージング環境では異なるログイン情報が必要となります。

* **NAステージング環境** ログインページ：https://s7sps1-staging.scene7.com/IpsWeb/ [](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEAステージング環境** :https://s7sps3-staging.scene7.com/IpsWeb/ [](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPACステージング環境** :https://s7sps5-staging.scene7.com/IpsWeb/ [](https://s7sps5-staging.scene7.com/IpsWeb/)

[ルールセットでの &#39;is&#39; イメージに代わる &#39;asset&#39; の使用](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)も参照してください。

**XML ルールセットをデプロイするには：**

1. Dynamic Media Classicアカウントにログオンします。

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   資格情報とログオンは、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. 次の手順を実行して、ルールセットファイルをアップロードします。

   * グローバルナビゲーションバーの「**[!UICONTROL アップロード]**」をクリックします。
   * On the **[!UICONTROL Upload]** page, near the upper-left corner, click **[!UICONTROL Browse]**.
   * In the **[!UICONTROL Open]** dialog box, browse to your rule set file (XML).
   * ファイルを選択して、「**[!UICONTROL 開く]**」をクリックします。
   * On the right side of the **[!UICONTROL Upload]** page, select a destination folder for the rule set file.
   * ページ下部付近の「**[!UICONTROL アップロード後に公開]**」が選択されていることを確認します。
   * ページの右下隅の「**[!UICONTROL アップロードを送信]**」をクリックします。
   * グローバルナビゲーションバーの「**[!UICONTROL ジョブ]**」をクリックして、アップロードジョブのステータスを確認します。When the **[!UICONTROL Status]** column on the **[!UICONTROL Job]** page says Upload Done, continue to the next steps.

1. On the navigation bar near the top of the page, click **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]**.
1. On the **[!UICONTROL Image Server Publish]** page, under the **[!UICONTROL Catalog Management]** group, locate **[!UICONTROL Rule Set Definition File Path]**, then click **[!UICONTROL Select]**.
1. On the **[!UICONTROL Select Rule Set Definition File (XML)]** page, browse to your rule set file, then in the lower-right corner of the page, click **[!UICONTROL Select]**.
1. 設定ページの右下隅の「**[!UICONTROL 閉じる]**」をクリックします。
1. Image Server 公開ジョブを実行します。

   ルールセットの条件が現在の Dynamic Media の Image Server へのリクエストに適用されます。

   ルールセットファイルを変更した場合、変更したルールセットファイルを再アップロードして再公開すると、変更内容がただちに適用されます。

