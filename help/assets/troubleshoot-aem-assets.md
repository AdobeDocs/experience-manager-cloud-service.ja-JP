---
title: AEM Assetsのトラブルシューティング
description: アップロード、メタデータ、検索、配信など、AEM Assetsの主要な領域に関する記事リンクを使用して、AEM Assetsの一般的な問題をトラブルシューティングします。
hidefromtoc: true
hide: true
source-git-commit: c8f1c40e4300b26141cc394a9208641769da1f1e
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# AEM Assetsの問題のトラブルシューティング {#troubleshoot-aem-assets}

AEM Assets as a Cloud Serviceは、デジタルアセット管理や Dynamic Media の運用を行うためだけでなく、AI や ML などの次世代スマート機能を使用する企業向けに、クラウドネイティブの PaaS ソリューションを提供します。 常に最新、常に利用可能、常に学習可能なシステム内からすべて。

ただし、アセットのアップロード、メタデータ、検索、配信など、AEM Assetsの主要な領域に影響を与える問題が発生する場合があります。 この記事では、AEM Assetsの一般的な問題を診断および解決するのに役立つトラブルシューティング手順を説明します。

<table>
  <tbody>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27140">AEMのアセットダウンロード ZIP ファイルにレンディションが見つからない </a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">AEM Assets ライセンスに含まれていないコンテンツフラグメント </a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928"> 読み取りアクセス権にもかかわらず、Assetsビューでコメントが制限される </a> </td> 
    </tr>
    <tr>
    <td>AEM Dynamic Media で <a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715"> （Dynamic Media）スピンセットが処理中ステータスでスタックする </a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">AEMの元のファイルと一致しない Digital Asset Management （DAM）レンディション </a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">AEMaaCS でスマート切り抜きレンディションが生成されない </a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533"> （Dynamic Media）AEMでのビデオのアップロード、処理、レンダリングの問題を修正しました </a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922"> （Asset Link） InDesignを使用すると、Adobe Asset Link でリンクがアクセス不能な状態になる </a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">AEMaaCS の Dynamic Media と DAM カードビューでビデオサムネールが一致しない </a> </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Serviceでの大きな MP4 ファイルのアセット処理が失敗しました</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">（Dynamic Media） Dynamic Media ビデオプレーヤーが下位の環境で機能しない</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26103">（Dynamic Media と OpenAPI） IMS ユーザーグループに基づく Open API を使用して、Dynamic Media への制限付きAssets アクセスを有効化します</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">ZIP 圧縮形式の Tiff ファイルをAEM Assetsにアップロードすると、レンディションが生成されません</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEMでは、大きな PDF から抽出されたテキストを 100,000 個のトークンの後で切り捨てます</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">（Dynamic Media） DM Assetsの Dynamic Media URL の変更</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">AEMaaCS の管理者以外のユーザーに対するメタデータスキーマの表示の問題の解決</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">（Dynamic Media） Dynamic Media でのTIFF画像レンディションの背景色の変更の問題</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">AEMaaCS アセットの回転の問題により、後続の回転が非表示になる</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">（Dynamic Media）Adobe Experience Manager 6.5 Dynamic Media でのスマート切り抜きに関する画像の破損の問題の解決</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">Photoshop Firefly API 統合のシングルパートアセットのアップロード制限を引き上げる</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">（Dynamic Media）PDF ファイルに関するAEM環境全体での Dynamic Media アセット名の不一致を解決します</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">Adobe Experience Manager（AEM）as a Cloud Service - Asset で、特定の画像のサムネールのレンディションが表示されない</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">（Dynamic Media） Dynamic Media 一般設定ページが開かない</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">（Dynamic Media）AEMの Dynamic Media でビデオファイルのオーディオの問題を解決します</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">AEM as a Cloud Serviceに新しくアップロードされたアセットの自動タグ付け</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">AEMで JWT から OAuth に移行した後、スマートタグ機能が機能しない</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">AEM Managed Servicesでの共有リンクの問題の解決</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25607">（Dynamic Media）AEM Dynamic Media でのアセット処理エラー</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">Adobe Experience Manager（AEM） Dynamic Media での（Dynamic Media）アセット同期の失敗</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">AEM as a Cloud Serviceのビデオアセットのカスタムサムネールの更新</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">Adobe Experience Manager（AEM）Assetsにおける画像メタデータの不一致</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">アセットのフォルダーのAEM Assets Web UI へのドラッグ&amp;ドロップに失敗する</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">（Dynamic Media）AEM as a Cloud Serviceでのアセット処理の問題の解決</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">Adobe Experience Manager as a Cloud Serviceでの大きな PDF のテキスト抽出の制限</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">（Asset Link）InDesignでのAdobe Experience Manager（AEM） asset link 接続の問題の解決</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">（Asset Link）Adobe Asset Link プラグインのネットワークエラー：サーバーに到達できません</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">（Dynamic Media） Dynamic Media 同期のユーザーレコメンデーション</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">（Dynamic Media） API を使用した Dynamic Media からのアセットとメタデータの書き出し</a></td>
  <td></td>
</tr>

</tbody>
  <table>


