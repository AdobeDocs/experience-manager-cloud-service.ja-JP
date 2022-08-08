---
title: コンテンツ転送ツールの基本を学ぶ（レガシー）
description: コンテンツ転送ツールの基本を学ぶ
hide: true
hidefromtoc: true
exl-id: a6ee6996-510e-42d7-9a7c-f64732764f97
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# コンテンツ転送ツールの基本を学ぶ（レガシー） {#getting-started-content-transfer-tool}


## 入手方法 {#availability}

コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)を使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。最新バージョンの詳細については、「[リリースノート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)」を参照してください。

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

   1. **Cloud Service 設定**：移行先の AEM as a Cloud Service オーサーの URL を入力します。

      >[!NOTE]
      >コンテンツ転送を行う際は、一度に最大 10 個の移行セットを作成し維持管理できます。
      >さらに、特定の環境（*ステージング*、*開発*、*実稼動*&#x200B;のいずれか）ごとに個別に移行セットを作成する必要があります。

   1. **アクセストークン**：アクセストークンを入力します。

      >[!NOTE]
      >「**アクセストークンを開く**」ボタンを使用してアクセストークンを取得できます。ターゲット Cloud Service インスタンスの「管理者」グループに属していることを確認する必要があります。

   1. **パラメーター**： 移行セットを作成するには、次のパラメータを選択します。

      1. **バージョンを含める**： 必要に応じて選択します。バージョンが含まれる場合は、監査イベントを移行するために、パス `/var/audit` が自動的に含まれます。

         ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >バージョンを移行セットの一部に含める予定で、`wipe=false` を指定して追加を行う場合、コンテンツ転送ツールの現在の制限事項により、バージョンのパージを無効にする必要があります。バージョンのパージを有効にしたまま、移行セットへの追加を行う場合は、`wipe=true` を指定して取り込みを実行する必要があります。


      1. **含めるパス**： パスブラウザーを使用して、移行する必要があるパスを選択します。パスピッカーは、キーボード入力または選択による入力を受け付けます。

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

### 移行セットのサイズとディスク容量の決定 {#migration-set-size}

移行セットを作成した後、抽出プロセスを開始する前に、移行セットに対してサイズ確認を実行することを強くお勧めします。移行セットに対してサイズ確認を実行すると、以下が可能になります。
* 抽出を正常に完了できるだけの十分なディスク容量が `crx-quickstart` サブディレクトリにあるかどうかを確認します。
* 移行セットのサイズが製品の制限内に収まるかどうかを判断し、コンテンツの取り込みに失敗しないようにします。

サイズ確認を実行するには、次の手順に従います。

1. 移行セットを選択し、「**サイズを確認**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. **移行セットサイズを確認**&#x200B;ダイアログが開きます。

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. 「**サイズを確認**」をクリックして、プロセスを開始します。移行セットリスト表示に戻り、**サイズ確認**&#x200B;が実行中であることを示すメッセージが表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. **サイズ確認**&#x200B;プロセスが完了したら、ステータスが&#x200B;**完了**&#x200B;に変わります。同じ移行セットを選択し、「**サイズを確認**」をクリックして結果を表示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   以下は、警告を含まない&#x200B;**サイズ確認**&#x200B;結果の例です。

   ![画像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. **サイズ確認**&#x200B;の結果、空きディスク容量が不足しているか、移行セットが製品の制限を超えていることがわかった場合は、**警告**&#x200B;ステータスが表示されます。

![画像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

以下は、警告を含んだ&#x200B;**サイズ確認**&#x200B;結果の例です。

![画像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## 次の手順 {#whats-next}

移行セットの作成方法を理解したら、コンテンツ転送ツールでの抽出プロセスと取り込みプロセスについて学ぶ準備が整います。これらのプロセスを学ぶ前に、コンテンツを AEM as a Cloud Service に移行するコンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮する[大規模なコンテンツリポジトリーの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja)を参照する必要があります。
