---
title: Dynamic Media を使用した CDN キャッシュの無効化
description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
translation-type: tm+mt
source-git-commit: 77e270b354e7e99aa2e7ab88ddc8528ad0c4ade0
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 97%

---


# Dynamic Media を使用した CDN キャッシュの無効化 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Media アセットは、顧客との配信を高速化するために、CDN（コンテンツ配信ネットワーク）によってキャッシュされます。ただし、これらのアセットを更新する場合に、その変更を Web サイトに即座に反映させたいことがあります。CDN キャッシュの削除または無効化をおこなうと、Dynamic Media によって配信されるアセットをすばやく更新できます。TTL（有効期限）の値（デフォルトは 10 時間）を使用してキャッシュの有効期限が切れるのを待つ代わりに、Dynamic Media ユーザーインターフェイスからリクエストを送信し、キャッシュの有効期限を数分に設定できます。

>[!IMPORTANT]
>
>この機能を使用するには、AEMDynamic Mediaに組み込まれている標準搭載のCDNを使用する必要があります。その他のカスタムCDNはサポートされていません。<!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

[Dynamic Media のキャッシュの概要](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)も参照してください。

**Dynamic Media経由でCDNキャッシュを無効にするには**

*パート 1 / 2：CDN 無効化テンプレートの作成*

1. AEM as a Cloud Service で、**[!UICONTROL ツール／アセット／CDN 無効化テンプレート]**&#x200B;をタップします。

   ![CDN 検証機能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. **[!UICONTROL CDN 無効化テンプレート]**&#x200B;ページで、シナリオに応じて次のいずれかのオプションを実行します。

   | シナリオ | オプション |
   | --- | --- |
   | Dynamic Media Classic を使用して、以前に CDN 無効化テンプレートを作成したことがある。 | 「**[!UICONTROL テンプレートを作成]**」テキストフィールドに、テンプレートデータが事前に入力されています。この場合は、テンプレートを編集するか、続行して次の手順に進みます。 |
   | テンプレートを作成する必要がある。入力する値 | 「**[!UICONTROL テンプレートを作成]**」テキストフィールドには、特定の画像 ID ではなく、次の例のように、`<ID>` を参照する画像 URL（画像プリセットまたは修飾子を含む）を入力します。<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>テンプレートに `<ID>` のみが含まれる場合、Dynamic Media が `https://<publishserver_name>/is/image/<company_name>/<ID>` 部分を埋めます。ここで、`<publishserver_name>` は、Dynamic Media Classic の「一般設定」で定義されているパブリッシュサーバー名で、`<company_name>` は、この AEM インスタンスに関連付けられている自社のルート名で、`<ID>` は、無効にするアセット選択を介して選択されたアセットです。<br>プリセット／修飾子の post `<ID>` は、そのまま URL 定義内にコピーされます。<br>テンプレートに基づいて自動形成できるのは画像のみ、すなわち `/is/image` のみです。<br>`/is/content/` の場合、アセットピッカーを使用してビデオや PDF などのアセットを追加しても、URL は自動生成されません。代わりに、CDN 無効化テンプレートでそのようなアセットを指定するか、*パート 2 / 2 CDN 無効化オプションの設定*&#x200B;で、URL を手動で追加する必要があります。<br>**例：**<br>&#x200B;最初の例では、無効化テンプレートに `<ID>` と、`/is/content` を持つアセット URL が含まれます。例えば、`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>` のようになります。Dynamic Media は、これに基づいて URL を作成し、`<ID>` は、アセットピッカーを使用して選択された、無効にするアセットとなります。<br>2 つ目の例では、無効化テンプレートに、`/is/content` が用いられ、Web プロパティで使用されるアセットの完全な URL が含まれます（アセットピッカーに依存しません）。例えば、`http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` の backpack はアセット ID です。<br>Dynamic Media でサポートされているアセット形式は、無効化の対象となります。CDN の無効化で&#x200B;*サポートされない*&#x200B;アセットファイルタイプには、Postscript、Encapsulated Postscript、Adobe Illustrator、Adobe InDesign、Microsoft PowerPoint、Microsoft Excel、Microsoft Word、リッチテキスト形式などがあります。<br>テンプレートを作成する際は、構文と入力ミスに注意する必要があります。Dynamic Media では、テンプレートの検証はおこなわれません。<br>画像スマートトリミングの URL は、この CDN 無効化テンプレート、またはパート 2：CDN 無効化オプションの設定の「**[!UICONTROL URL を追加]**」テキストフィールドのいずれかで指定する必要があります&#x200B;*。*<br>**重要：** CDN 無効化テンプレートの各エントリは、それぞれ別の行にする必要があります。<br>*次のテンプレートの例は説明用です。* |

   ![CDN 無効化テンプレート - 作成](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 「**[!UICONTROL CDN 無効化テンプレート]**」ページの右上隅にある「**[!UICONTROL 保存]**」をタップし、「**[!UICONTROL OK]**<br>」をタップします。

   *パート 2 / 2：CDN 無効化オプションの設定*
   <br>

1. AEM as a Cloud Service で、**[!UICONTROL ツール／アセット／CDN 無効化]**&#x200B;をタップします。

   ![CDN 検証機能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. **[!UICONTROL CDN 無効化]** - **[!UICONTROL 追加詳細]**&#x200B;ページで、CDN を無効化にするアセットを選択します。

   ![CDN 無効化 - 追加詳細](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >「**[!UICONTROL CDN でアセット関連の画像プリセットを無効にする]**」*および*「**[!UICONTROL テンプレートに基づいて無効にする]**」をオフにしたままにすると、選択したアセットのベース URL が無効に設定されます。このオプションは、画像に対してのみ使用します。


   | オプション | 説明 |
   | --- | --- |
   | **[!UICONTROL CDN でアセット関連の画像プリセットを無効化する]** | （オプション）このオプションを選択すると、選択したアセットとそれに関連するすべての画像プリセット URL が、キャッシュの無効化のために自動作成されます。<br>アセットと、それに関連付けられた事前定義のプリセット URL は、無効化のために自動作成されます。このオプションは、画像アセットに対してのみ機能します。 |
   | **[!UICONTROL テンプレートに基づいて無効化]** | （オプション）URL 作成に定義済みのテンプレートのみを使用する場合は、このオプションを選択します。 |
   | **[!UICONTROL アセットを追加]** | アセットピッカーを使用して、無効にするアセットを選択します。公開済みまたは非公開のアセットを選択できます。<br>CDN でのキャッシュは、アセットベースではなく URL ベースです。したがって、Web サイト上での完全な URL を認識しておく必要があります。これらの URL を決定したら、テンプレートに追加できます。それから、アセットを選択して追加し、ワンステップで URL を無効にできます。<br>このオプションは、「**[!UICONTROL CDN でアセット関連の画像プリセットを無効化する]**」、または「**[!UICONTROL テンプレートに基づいて無効化]**」、あるいはその両方と組み合わせて使用します。 |
   | **[!UICONTROL URL を追加]** | CDN キャッシュを無効にする Dynamic Media セットに、完全な URL パスを手動で追加または貼り付けます。***パート 1 / 2：CDN 無効化テンプレートの作成***&#x200B;で CDN 無効化テンプレートを作成しておらず、無効にするアセットが数個の場合にこのオプションを使用します。<br>**重要：**&#x200B;追加する各 URL は、それぞれ別の行に記述する必要があります。<br>一度に 1000 個までの URL を無効にできます。「**[!UICONTROL URL を追加]**」テキストフィールドの URL 数が 1000 を超える場合、「**[!UICONTROL 次へ]**」をタップできません。その場合、選択したアセットの右側の **[!UICONTROL X]** をタップするか、手動で追加した URL をタップして、アセットを無効化リストから削除する必要があります。<br>画像スマートトリミングの URL は、CDN 無効化テンプレートまたはこの **[!UICONTROL URL を追加]**&#x200B;テキストフィールドのいずれかで指定する必要があります。 |

1. ページの右上隅にある「**[!UICONTROL 次へ]**」をタップします。
1. **[!UICONTROL CDN 無効化]** - **[!UICONTROL 確認]**&#x200B;ページの **[!UICONTROL URL]** リストボックスに、前の手順で作成した CDN 無効化テンプレートから生成された 1 つ以上の URL と、先ほど追加したアセットのリストが表示されます。

   例えば、前の手順で示した CDN 無効化テンプレートの例を使用して、`spinset` という名前のアセットを 1 つ追加したとします。**[!UICONTROL ツール／アセット／CDN 無効化をタップすると]**、**[!UICONTROL CDN 無効化 - 確認]**&#x200B;ユーザーインターフェイスで以下の 5 つの URL が生成されます。

   ![CDN 無効化 - 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   必要に応じて、URL の右側の **X** をタップして、URL を無効化プロセスから削除します。

1. ページの右上隅近くにある「**[!UICONTROL 送信]**」をタップして、CDN 無効化プロセスを開始します。

## CDN 無効化エラーのトラブルシューティング

いずれの場合も、無効にするバッチ全体が処理されるか、バッチ全体が失敗します。

| エラー | 説明 |
| --- | --- |
| *選択されたアセットの URL を取得できませんでした。* | 次のいずれかのシナリオが満たされた場合に発生します：<br> - Dynamic Media 設定が見つかりません。<br> - Dynamic Media 設定の読み取りに使用するサービスユーザーの取得中に例外が発生しました。<br> - URL の形成に使用するパブリッシュサーバーまたは会社ルートが Dynamic Media の設定にありません。 |
| *一部の URL が正しく定義されていません。訂正して再送信してください。* | IPS CDN キャッシュ無効化 API が、URL が別の会社を参照しているというエラーを返す場合、または IPS cdnCacheInvalidation API が実行した検証に従って URL が有効ではない場合に発生します。 |
| *CDN キャッシュを無効にできませんでした。* | CDN キャッシュの無効化リクエストがその他の理由で失敗した場合に発生します。 |
| *無効にする URL が入力されていません。* | **[!UICONTROL CDN 無効化]** - **[!UICONTROL 確認]**&#x200B;ページに URL が存在せず、「**[!UICONTROL 送信]**」をタップした場合に発生します。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
