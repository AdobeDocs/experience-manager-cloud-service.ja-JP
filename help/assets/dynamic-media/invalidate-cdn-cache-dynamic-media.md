---
title: ダイナミックメディアを使用したCDNキャッシュの無効化
description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
translation-type: tm+mt
source-git-commit: aae3dcb0f44ef8e8d1401274fbf1fd47ea718b09
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 4%

---


# ダイナミックメディアを使用したCDNキャッシュの無効化 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Mediaアセットは、顧客との配信を高速化するために、CDN(コンテンツ配信ネットワーク)によってキャッシュされます。 ただし、これらのアセットを更新する場合は、その変更をWebサイトに即座に反映させることができます。 CDNキャッシュの削除または無効化を行うと、ダイナミックメディアによって配信されるアセットをすばやく更新できます。 TTL(Time To Live)値（デフォルトは10時間）を使用してキャッシュの有効期限が切れるのを待つ代わりに、ダイナミックメディアユーザーインターフェイスから要求を送信し、キャッシュの有効期限を数分で設定できます。

>[!IMPORTANT]
>
>次の手順は、Cloud ServiceとしてAEM上のダイナミックメディアにのみ適用されます。 また、AEMダイナミックメディアに組み込まれている、標準搭載されたCDNを使用する必要もあります。 この機能では、その他のカスタムCDNはサポートされません。 <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

ダイナミックメディアの [キャッシュの概要も参照してください](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**ダイナミックメディアを使用してCDNキャッシュを無効にするには**

*パート1:CDN無効化テンプレートの作成*

1. AEMで、Cloud Serviceとして **[!UICONTROL ツール/アセット/CDN無効化テンプレートをタップします。]**

   ![CDN検証機能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. 「 **[!UICONTROL CDN無効化テンプレート]** 」ページで、シナリオに基づいて次のいずれかのオプションを実行します。

   | シナリオ | オプション |
   | --- | --- |
   | Dynamic Media Classicを使用して、以前にCDN無効化テンプレートを作成したことがあります。 | 「テンプレート **[!UICONTROL を作成]** 」テキストフィールドには、テンプレートデータが事前に入力されています。 この場合は、テンプレートを編集するか、次の手順に進むことができます。 |
   | テンプレートを作成する必要があります。 何を入れる？ | 「テンプレート **[!UICONTROL を作成]** 」テキストフィールドに、特定の画像IDではなく、を参照する画像URL（画像プリセットまたは修飾子を含む）を入力します。 `<ID>`例：テンプレートに含める<br><br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br><br>`<ID>``https://<publishserver_name>/is/image``<publishserver_name>``ID` だけの場合は、Dynamic MediaはPublish Serverの名前を入力し、アセットを検証します。<br><br>テンプレートに基づいて自動形成で `/is/image`きるのは、画像のみです。 例え `/is/content/`ば、アセットピッカーを使用してビデオやPDFなどのアセットを追加しても、URLが自動生成されません。 代わりに、CDN無効化テンプレートでそのようなアセットを指定するか、 *パート2でこのようなアセットにURLを手動で追加する必要があります。CDN無効化オプションの設定を参照*。<br>ダイナミックメディアでサポートされているアセット形式は、無効化の対象となります。 PowerPointsやプレーンテキストファイルなどのアセットは、CDNの無効化ではサポートされていません。<br>テンプレートを作成する際は、構文と入力ミスに注意する必要があります。ダイナミックメディアでは、テンプレートの検証は行われません。<br>次のテンプレートの例は、説明用です。 |

   ![CDN無効化テンプレート — 作成](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. CDN無効化テンプレートページの右上隅にある「 **[!UICONTROL 保存]**」をタップし、「 **[!UICONTROL OK]**」をタップします。<br>

   ***パート2:CDN無効化オプションの設定***
<br>

1. AEMで、Cloud Serviceとして **[!UICONTROL ツール/アセット/CDNの無効化をタップします。]**

   ![CDN検証機能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 「 **[!UICONTROL CDN無効化]** - **[!UICONTROL 追加詳細]** 」ページで、CDN無効化のアセットを選択します。

   ![CDNの無効化 —追加詳細](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >「CDN内のアセットに関連付けられた画像プリセットを **[!UICONTROL 無効にする]** 」 *および「テンプレートに基づいて無効にする***** 」をオフにしたままにすると、選択したアセットのベースURLが無効に設定されます。 このオプションは、画像に対してのみ使用してください。


   | オプション | 説明 |
   | --- | --- |
   | **[!UICONTROL CDN でアセット関連の画像プリセットを無効化します]** | （オプション）このオプションを選択すると、MIMEタイプに関係なく、1つ以上のダイナミックメディアアセットを選択し、キャッシュの無効化に関連付けられた画像プリセットを選択できます。<br>アセットと、それに関連付けられた事前定義のプリセットURLは、無効化のために自動形成されます。 このオプションは、画像<br>アセットに対してのみ機能します。アセットを含む1つ以上のフォルダーを選択できますが、Adobeではこの方法をお勧めしません。 代わりに、個々のアセットファイルを選択する必要があります。 |
   | **[!UICONTROL テンプレートに基づく無効化]** | （オプション）URL生成に定義済みのテンプレートのみを使用する場合は、このオプションを選択します。 |
   | **[!UICONTROL アセットを追加]** | アセット選択を使用して、無効にするアセットを選択します。 公開済みまたは非公開のアセットを選択できます。<br>アセットを追加すると、空白のリストが表示される場合があります。 ダイナミックメディアは、CDN無効化テンプレートを使用して、URLを自動的に作成し、CDNを無効にします。 CDN無効化テンプレートが作成されていない場合は、空白のリストが表示されます。<br>CDNでのキャッシュは、アセットベースではなくURLベースです。 したがって、Webサイト上の完全なURLを認識する必要があります。 これらのURLを決定したら、それらをテンプレートに追加します。次に、これらのアセットを選択して追加し、URLを無効にする作業を1つの手順で行います。 もう1つの方法は、CDN無効化リストにURLを追加することです。 この方法を使用する場合は、「 **[!UICONTROL 次へ]** 」をタップし、無効化のために「 **[!UICONTROL 送信]** 」をタップする前に、アセットを選択して追加する必要はありません。<br>このオプションは、CDNの「関連する画像プリセットを **[!UICONTROL 無効にする」または「テンプレートに基づく]**&#x200B;無効化 **[!UICONTROL 」と組み合わせて使用します]**。 |
   | **[!UICONTROL URL を追加]** | CDNキャッシュを無効にするダイナミックメディアアセットに、完全なURLパスを手動で追加または貼り付けます。 パート1でCDN無効化テンプレートを作成しなかった場合は、このオプションを使用し ***ます。CDN無効化テンプレートの操作***。無効にするアセットは数個だけです。<br> |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next]**.
1. **[!UICONTROL CDN無効化]** - **[!UICONTROL 確認]** ページの「URL **** リスト」ボックスに、前の手順で作成したCDN無効化テンプレートから生成された1つ以上のURLと、先ほど追加したアセットのリストが表示されます。

   例えば、CDN無効化テンプレートが以前に作成された状態で、という名前の単一のアセットを追加したと `spinset`します。 **[!UICONTROL ツール/アセット/CDNの無効化をタップすると]** 、 **[!UICONTROL CDNの無効化 — 確認]** ユーザーインターフェイスで以下の5つの生成されたURLが生成されます。

   ![CDNの無効化 — 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   必要に応じて、URLの右側の **X** をタップして、URLを無効化プロセスから削除します。 一度に1,000個までのURLを設定できます。

1. ページの右上隅近くにある「 **[!UICONTROL 送信]** 」をタップして、CDN無効化プロセスを開始します。

## CDN無効化エラーのトラブルシューティング

* この機能を使用すると、一度に最大1000個のURLを無効にできます。 1000を超える数値を指定すると、 **[!UICONTROL CDN無効化 — 確認]** ページのURLを削除することで解決できるエラーが発生します。
* いずれの場合も、バッチ全体が無効化のために処理されるか、バッチ全体が失敗します。

| エラー | 説明 |
| --- | --- |
| *選択されたアセットのURLを取得できませんでした。* | 次のいずれかのシナリオが満たされた場合に発生します。<br>— ダイナミックメディア設定が見つかりません。<br>— ダイナミックメディア設定の読み取りに使用するサービスユーザーの取得中に例外が発生しました。<br>- URLの形成に使用する発行サーバまたは会社ルートがダイナミックメディアの設定にありません。 |
| *一部のURLが正しく定義されていません。 訂正して再送信してください。* | IPS CDNキャッシュ無効化APIが、URLが別の会社を参照しているというエラーを返す場合、またはIPS cdnCacheInvalidation APIが実行した検証に従ってURLが有効でない場合に発生します。 |
| *CDNキャッシュを無効にできませんでした。* | CDNキャッシュの無効化要求が他の理由で失敗した場合に発生します。 |
| *無効にするURLが入力されていません。* | CDN無効化 — 確認ページにURLが存在しない場合に発生し **[!UICONTROL 、「]**&#x200B;送信」をタップしたとき ****。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->