---
title: カスタムエラーページ
description: AEMには、HTTPエラーを処理するための標準的なエラーハンドラが付属しており、これはカスタマイズできます。
translation-type: tm+mt
source-git-commit: d7e9bdee83f1b85436185ca57420ee178268cb33
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 39%

---


# エラーページのカスタマイズ {#customizing-error-pages}

AEMには、HTTPエラーを処理するための標準的なエラーハンドラが付属しています。例えば、次のように表示します。

![標準エラーメッセージ](assets/error-message-standard.png)

エラーに応答するために、AEMは`/libs/sling/servlet/errorhandler`の下に`404.jsp`スクリプトを提供します。

>[!TIP]
>
>AEMはApache Slingをベースにしているので、Apacheエラー処理ドキュメントの[詳細情報を](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)から入手できます。

>[!NOTE]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) がデフォルトで有効です。このフィルターは常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて常に無効になります。****

## エラーハンドラーによって表示されるページのカスタマイズ方法{#how-to-customize-pages-shown-by-the-error-handler}

エラーが発生した場合にエラーハンドラーによって表示されるページをカスタマイズする独自のスクリプトを作成できます。 これを行うには、[AEM標準のオーバーレイメカニズム](/help/implementing/developing/introduction/overlays.md)を利用して、カスタマイズしたページを`/apps`の下に作成し、`/libs`の下にあるデフォルトのページをオーバーレイします。

1. リポジトリ内で、デフォルトスクリプトをコピーします。

   * `/libs/sling/servlet/errorhandler/` から
   * を `/apps/sling/servlet/errorhandler/`

   デフォルトでは宛先パスが存在しないので、初めて作成する場合は作成する必要があります。

1. `/apps/sling/servlet/errorhandler` に移動します。次のどちらかを実行します。

   * 既存のスクリプトを編集し、必要な情報を追加します。または
   * 必要とするコード用に新しいスクリプトを作成し、編集します。

1. 変更を保存し、テストします。

>[!CAUTION]
>
>`404.jsp`スクリプトは、AEM認証に対応するように設計されています。特に、これらのエラーが発生した場合にシステムログインを許可する場合。
>
>したがって、このスクリプトの置き換えは慎重に行う必要があります。

### HTTP 500 エラーへの応答のカスタマイズ {#customizing-the-response-to-http-errors}

HTTP [500内部サーバーエラー](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)は、サーバーが予期しない状態に陥り、要求を満たさなかったなどのサーバー側エラーを示します。

要求処理の結果例外が発生した場合、Apache Slingフレームワーク(AEMが構築されているフレームワーク):

* 例外をログに記録します
* 応答の本文に戻ります。
   * HTTP応答コード500
   * 例外スタックトレース

[エラーハンドラーによって表示されるページをカスタマイズする](#how-to-customize-pages-shown-by-the-error-handler)ことで、`500.jsp` スクリプトを作成できます。ただし、`HttpServletResponse.sendError(500)`が明示的に実行された場合にのみ使用されます。例えば、例外キャッチャーから。

それ以外の場合は、応答コードは に設定されますが、`500.jsp`500.  スクリプトは実行されません。

500 エラーを処理するには、エラーハンドラースクリプトの名前を例外クラス（またはスーパークラス）と同じにする必要があります。このような例外をすべて処理するには、スクリプト`/apps/sling/servlet/errorhandler/Throwable.jsp`または`/apps/sling/servlet/errorhandler/Exception.jsp`を作成します。

>[!CAUTION]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) がデフォルトで有効です。このフィルターは常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>カスタムエラーハンドラーの場合、コード500の応答が必要なので、[CQ WCMデバッグフィルターを無効にする必要があります。](/help/implementing/deploying/configuring-osgi.md)これにより、応答コード500が返され、正しいSlingエラーハンドラーがトリガーされます。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて常に無効になります。****
