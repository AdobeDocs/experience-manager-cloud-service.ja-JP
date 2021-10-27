---
title: コンテンツ転送ツールの概要
description: コンテンツ転送ツールの概要
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: fc0628c2bfd345a7846d3d4fbd0fe11a459b10a1
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 59%

---

# コンテンツ転送ツールの概要 {#getting-started-content-transfer-tool}

## ソース環境の接続

ソースAEMインスタンスがファイアウォールの内側で動作し、許可リストに追加された特定のホストにのみ到達できる場合があります。 抽出を正常に実行するには、AEMを実行しているインスタンスから次のエンドポイントにアクセスできる必要があります。

* 対象のAEMas a Cloud Service環境：
   `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure BLOB ストレージサービス：
   `*.blob.core.windows.net`
* ユーザーマッピング IO エンドポイント：
   `usermanagement.adobe.io`

ターゲットAEMas a Cloud Service環境への接続をテストするには、ソースインスタンスのシェルから次の cURL コマンドを発行します ( `program_id`, `environment_id`、および `migration_token`):

```
 curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"
```

>[!NOTE]
>次の場合、 `HTTP/2 200` が受信された場合、AEM as a Cloud Serviceへの接続に成功しました。

## 入手方法 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="ダウンロード"
>abstract="コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="リリースノート"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="ソフトウェア配布ポータル"

コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。最新バージョンの詳細については、「[リリースノート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)」を参照してください。

>[!NOTE]
>[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からコンテンツ転送ツールをダウンロードします。

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

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. **コンテンツ移行**&#x200B;ウィザードから「**コンテンツ転送**」オプションを選択します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. 最初の移行セットを作成すると、次のコンソールが表示されます。「**移行セットを作成**」をクリックして、新しい移行セットを作成します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >既存の移行セットがある場合、コンソールには既存の移行セットのリストが表示され、現在のステータスが表示されます


1. **移行セットを作成**&#x200B;画面の各フィールドに、以下のように値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名前**：移行セットの名前を入力します。
      >[!NOTE]
      >移行セット名には特殊文字を使用できません。

   1. **クラウドサービス設定**：移行先の AEM as a Cloud Service オーサーの URL を入力します。

      >[!NOTE]
      >コンテンツ転送をおこなう際は、一度に最大 10 個の移行セットを作成し維持管理できます。
      >さらに、特定の環境（*ステージング*、*開発*、*実稼動*&#x200B;のいずれか）ごとに個別に移行セットを作成する必要があります。

   1. **アクセストークン**：アクセストークンを入力します。

      >[!NOTE]
      >「**アクセストークンを開く**」ボタンを使用してアクセストークンを取得できます。ターゲット Cloud Service インスタンスの AEM 管理者グループに属していることを確認する必要があります。

   1. **パラメーター**：移行セットを作成するには、次のパラメータを選択します。

      1. **バージョンを含める**：必要に応じて選択します。バージョンが含まれる場合、パス `/var/audit` 監査イベントを移行するために、が自動的に含まれます。

         ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >バージョンを移行セットに含める予定で、 `wipe=false`を無効にした場合、コンテンツ転送ツールの現在の制限により、バージョンのパージを無効にする必要があります。 バージョンのパージを有効にしたまま、移行セットへの追加を実行する場合は、次のように取り込みを実行する必要があります。 `wipe=true`.


      1. **含めるパス**：パスブラウザーを使用して、移行する必要があるパスを選択します。パスピッカーは、キーボード入力または選択による入力を受け付けます。

         >[!IMPORTANT]
         >移行セットの作成時には、次のパスは制限されます。
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`（`/etc` の一部のパスは CTT で選択できます）


1. クリック **保存** 次に、 **移行セットを作成** 詳細画面。

1. 移行セットが **コンテンツ転送** ウィザードに表示されます（下図を参照）。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt07.png)

   既存のすべての移行セットが **コンテンツ転送** ウィザードに現在のステータスとステータスの情報が表示されます。 以下に示すアイコンの一部が表示されます。

   * *赤い雲*&#x200B;は、抽出プロセスを完了できないことを示しています。
   * *緑色の雲*&#x200B;は、抽出プロセスを完了できることを示しています。
   * *黄色のアイコン*&#x200B;は、その既存の移行セットが同じインスタンス内の他のユーザーによって作成されたことを示しています。

1. 移行セットを選択し、「 」をクリックします。 **プロパティ** 移行セットのプロパティを表示または編集するには、次の手順に従います。 プロパティの編集中は、 **移行セット名** または **サービス URL**.

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


## 次の手順 {#whats-next}

移行セットの作成方法を学習したら、コンテンツ転送ツールでの抽出プロセスと取り込みプロセスについて学ぶ準備が整いました。 これらのプロセスを学ぶ前に、 [大きなコンテンツリポジトリの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮して、コンテンツをAEM as a Cloud Serviceに移動する。
