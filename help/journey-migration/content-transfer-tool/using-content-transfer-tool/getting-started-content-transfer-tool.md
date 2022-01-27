---
title: コンテンツ転送ツールの基本を学ぶ
description: コンテンツ転送ツールの基本を学ぶ
source-git-commit: bec7e01a6f192a9b65a038b2e990c2c285743793
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 96%

---

# コンテンツ転送ツールの基本を学ぶ {#getting-started-content-transfer-tool}


## 入手方法 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="ダウンロード"
>abstract="コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="リリースノート"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="ソフトウェア配布ポータル"

コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージは、 [パッケージマネージャー](/help/implementing/developing/tools/package-manager.md) をソースAdobe Experience Manager(AEM) インスタンス上に置きます。 最新バージョンをダウンロードしてください。最新バージョンの詳細については、「[リリースノート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)」を参照してください。

>[!NOTE]
>[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からコンテンツ転送ツールをダウンロードします。

## ソース環境の接続性 {#source-environment-connectivity}

ソース AEM インスタンスがファイアウォールの内側で動作していて、許可リストに追加された特定のホストにしか到達できない場合があります。抽出を正常に実行するには、AEM を実行しているインスタンスから、次のエンドポイントにアクセスできる必要があります。

* ターゲット AEM as a Cloud Service 環境：`author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure BLOB ストレージサービス：`*.blob.core.windows.net`
* ユーザーマッピング IO エンドポイント：`usermanagement.adobe.io`

ターゲット AEM as a Cloud Service 環境への接続をテストするには、ソースインスタンスのシェルから次の cURL コマンドを発行します（`program_id`、`environment_id` および `migration_token` を実際の値に置き換えてください）。

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>`HTTP/2 200` を受け取った場合は、AEM as a Cloud Service への接続に成功しました。

## コンテンツ転送ツールの実行 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="コンテンツ転送ツールの実行"
>abstract="この節では、コンテンツ転送ツールを使用してコンテンツを AEM as a Cloud Service（オーサー／パブリッシュ）に移行する方法について説明します。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" デモを見る"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=ja#migration" text="チュートリアル - コンテンツ転送ツールの使用"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


この節では、コンテンツ転送ツールを使用してコンテンツを AEM as a Cloud Service（オーサー／パブリッシュ）に移行する方法について説明します。

1. Adobe Experience Manager を選択し、ツール／**運営**／**コンテンツ移行**&#x200B;に移動します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. **コンテンツ移行**&#x200B;ウィザードから「**コンテンツ転送**」オプションを選択します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. 最初の移行セットを作成すると、次のコンソールが表示されます。「**移行セットを作成**」をクリックして、新しい移行セットを作成します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >既存の移行セットがある場合、コンソールには既存の移行セットのリストが表示され、現在のステータスが表示されます


1. **移行セットを作成**&#x200B;画面の各フィールドに、以下のように値を入力します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名前**：移行セットの名前を入力します。
      >[!NOTE]
      >移行セット名には特殊文字を使用できません。

   1. **クラウドサービス設定**：移行先の AEM as a Cloud Service オーサーの URL を入力します。

      >[!NOTE]
      >コンテンツ転送を行う際は、一度に最大 10 個の移行セットを作成し維持管理できます。
      >さらに、特定の環境（*ステージング*、*開発*、*実稼動*&#x200B;のいずれか）ごとに個別に移行セットを作成する必要があります。

   1. **アクセストークン**：アクセストークンを入力します。

      >[!NOTE]
      >「**アクセストークンを開く**」ボタンを使用してアクセストークンを取得できます。ターゲットCloud Serviceインスタンスの「管理者」グループに属していることを確認する必要があります。

   1. **パラメーター**：移行セットを作成するには、次のパラメータを選択します。

      1. **バージョンを含める**：必要に応じて選択します。バージョンが含まれる場合は、監査イベントを移行するために、パス `/var/audit` が自動的に含まれます。

         ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >バージョンを移行セットの一部に含める予定で、`wipe=false` を指定して追加を行う場合、コンテンツ転送ツールの現在の制限事項により、バージョンのパージを無効にする必要があります。バージョンのパージを有効にしたまま、移行セットへの追加を行う場合は、`wipe=true` を指定して取り込みを実行する必要があります。


      1. **含めるパス**：パスブラウザーを使用して、移行する必要があるパスを選択します。パスピッカーは、キーボード入力または選択による入力を受け付けます。

         >[!IMPORTANT]
         >移行セットの作成時には、次のパスは制限されます。
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`（`/etc` の一部のパスは CTT で選択できます）


1. **移行セットを作成**&#x200B;画面のすべてのフィールドに値を入力したら、「**保存**」をクリックします。

1. 移行セットが&#x200B;**コンテンツ転送**&#x200B;ウィザードに表示されます（下図を参照）。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   既存のすべての移行セットが、現在のステータスなどのステータス情報と共に&#x200B;**コンテンツ転送**&#x200B;ウィザードに表示されます。以下に示すアイコンの一部が表示されます。

   * *赤い雲*&#x200B;は、抽出プロセスを完了できないことを示しています。
   * *緑色の雲*&#x200B;は、抽出プロセスを完了できることを示しています。
   * *黄色のアイコン*&#x200B;は、その既存の移行セットが同じインスタンス内の他のユーザーによって作成されたことを示しています。

1. 移行セットを選択し、「**プロパティ**」をクリックして、移行セットのプロパティを表示または編集します。プロパティの編集中は、「**移行セット名**」や「**サービス URL**」を変更できません。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)


## 次のステップ {#whats-next}

移行セットの作成方法を理解したら、コンテンツ転送ツールでの抽出プロセスと取り込みプロセスについて学ぶ準備が整います。これらのプロセスを学ぶ前に、コンテンツを AEM as a Cloud Service に移行するコンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮する[大規模なコンテンツリポジトリーの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja)を参照する必要があります。
