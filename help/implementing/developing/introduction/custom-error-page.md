---
title: カスタムエラーページ
description: AEM には、HTTP エラーを処理するための標準的なエラーハンドラーが付属しており、これはカスタマイズできます。
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: db997127c6cbba434b86990852d1ba590d5f12a5
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 87%

---

# エラーページのカスタマイズ {#customizing-error-pages}

AEM には、HTTP エラーを処理するための標準的なエラーハンドラーが付属しています。例えば、次のようなメッセージが表示されます。

![標準的なエラーメッセージ](assets/error-message-standard.png)

エラーに応答するために、AEM では `/libs/sling/servlet/errorhandler` の下に `404.jsp` スクリプトが用意されています。

>[!TIP]
>
>AEM は Apache Sling をベースにしているので、詳しくは、[Apache のエラー処理に関するドキュメント](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)を参照してください。

>[!NOTE]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) がデフォルトで有効です。このフィルターは常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて&#x200B;**常に**&#x200B;無効になります。

## エラーハンドラーで表示されるページのカスタマイズ方法 {#how-to-customize-pages-shown-by-the-error-handler}

独自のスクリプトを作成して、エラーの発生時にエラーハンドラーで表示されるページをカスタマイズできます。それには、[AEM の標準的なオーバーレイメカニズム](/help/implementing/developing/introduction/overlays.md)を利用して、カスタマイズしたページが `/apps` 下に作成され `/libs` 下のデフォルトページをオーバーレイするようにします。

1. リポジトリー内で、デフォルトスクリプトを次のようにコピーします。

   * コピー元：`/libs/sling/servlet/errorhandler/`
   * コピー先：`/apps/sling/servlet/errorhandler/`

   コピー先のパスはデフォルトでは存在しないので、この操作を初めて行う際は作成する必要があります。

1. `/apps/sling/servlet/errorhandler` に移動します。次のどちらかを実行します。

   * 該当する既存のスクリプトを編集し、必要な情報を追加します。または
   * 必要とするコード用に新しいスクリプトを作成し、編集します。

1. 変更を保存し、テストします。

>[!CAUTION]
>
>`404.jsp` スクリプトは、AEM 認証に合わせて設計されています。特に、これらのエラーの発生時にシステムログインができるようになっています。
>
>そのため、このスクリプトを置き換える際には十分に気をつけて作業してください。

### HTTP 500 エラーへの応答のカスタマイズ {#customizing-the-response-to-http-errors}

HTTP [500 内部サーバーエラー](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)は、サーバーで予期しない状況が発生したのでリクエストを処理できないといった、サーバーサイドエラーを示しています。

リクエストの処理で例外が発生した場合、Apache Sling フレームワーク（AEM の基盤）は以下を行います。

* 例外をログに記録します。
* 応答の本文で次のものを返します。
   * HTTP 応答コード 500
   * 例外スタックトレース

[エラーハンドラーで表示されるページをカスタマイズする](#how-to-customize-pages-shown-by-the-error-handler)ことで、`500.jsp` スクリプトを作成できます。ただし、このスクリプトが使用されるのは、`HttpServletResponse.sendError(500)` が明示的に（例外キャッチャーから）実行される場合に限ります。

それ以外の場合は、応答コードは 500 に設定されますが、`500.jsp` スクリプトは実行されません。

500 エラーを処理するには、エラーハンドラースクリプトのファイル名を例外クラス（またはスーパークラス）と同じにする必要があります。このような例外をすべて処理するには、スクリプト `/apps/sling/servlet/errorhandler/Throwable.jsp` または `/apps/sling/servlet/errorhandler/Exception.jsp` を作成します。

>[!NOTE]
>
>AEM as aCloud Serviceでは、CDN は、バックエンドから 5XX エラーを受け取るたびに、汎用エラーページを提供します。 バックエンドの実際の応答がを通過できるようにするには、応答に次のヘッダーを追加する必要があります。
>`x-aem-error-pass: true`
>これは、AEMまたは Apache/Dispatcher レイヤーからの応答に対してのみ機能します。 中間インフラストラクチャレイヤーから発生したその他の予期しないエラーは、一般的なエラーページに表示されます。

>[!CAUTION]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) がデフォルトで有効です。このフィルターは常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>カスタムエラーハンドラーの場合、コード 500 を含んだ応答が必要です。そのため、[CQ WCM Debug Filter を無効にする必要があります](/help/implementing/deploying/configuring-osgi.md)。それにより、応答コード 500 が返され、その結果、正しい Sling エラーハンドラーがトリガーされるようになります。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて&#x200B;**常に**&#x200B;無効になります。
