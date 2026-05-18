---
title: AEM Assetsのトラブルシューティング
description: アップロード、メタデータ、検索、配信など、AEM Assetsの主要な領域の記事リンクを使用して、AEM Assetsの一般的な問題をトラブルシューティングします。
hidefromtoc: true
hide: true
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: bcc0d481-4be4-4486-974b-89f89431c864
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 6%

---

# AEM Assets の問題のトラブルシューティング {#troubleshoot-aem-assets}

AEM Assets as a Cloud Service は、クラウドネイティブな PaaS ソリューションです。企業がデジタルアセット管理と Dynamic Media 操作を行うだけでなく、AI や機械学習などの次世代スマート機能を使用するうえでも役に立ちます。 これらすべては、常に最新で常に可用性が高く常に学習可能なシステム内から行います。

ただし、アセットのアップロード、メタデータ、検索、配信などのAEM Assetsの主要領域に影響を与える問題が発生する場合があります。 この記事では、AEM Assetsの一般的な問題の診断と解決に役立つトラブルシューティング手順について説明します。

<table>
  <tbody>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27140">AEMのアセットダウンロード ZIP ファイルにレンディションがありません</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">AEM Assets ライセンスに含まれていないコンテンツフラグメント </a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">読み取りアクセスに関わらず、Assets ビューでのコメントが制限されています</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715"> （Dynamic Media） スピンセットがAEM Dynamic Mediaの処理中に停止しました</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639"> デジタルアセット管理（DAM）レンディションがAEMのオリジナルファイルと一致しません</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">AEMaaCS</a>でスマート切り抜きレンディションが生成されない </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533"> （Dynamic Media）AEMでのビデオのアップロード、処理、およびレンダリングの問題を修正</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922"> （Asset Link） InDesignを使用すると、Adobe Asset Linkはリンクをアクセスできない状態のままにします</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">AEMaaCS</a>のDynamic MediaとDAM カード表示の間でビデオサムネールが一致しません </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Serviceで大きなMP4 ファイルのアセット処理に失敗しました</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">（Dynamic Media）低い環境でDynamic Media ビデオプレーヤーが機能しない</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26103">（Dynamic Media with OpenAPI） IMS ユーザーグループに基づくオープン APIを使用したDynamic Mediaへの制限付きAssets アクセスのアクティブ化</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">ZIP圧縮形式のTiff ファイルをAEM Assetsにアップロードすると、レンディションは生成されません</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEMでは、100,000個のトークンの後に、大きなPDFから抽出したテキストが切り捨てられます</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">（Dynamic Media） DM AssetsのDynamic Media URLの変更</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">AEMaaCSの管理者以外のユーザーのメタデータスキーマの表示に関する問題の解決</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">（Dynamic Media） Dynamic MediaでのTIFF画像レンディションの背景色の変更に関する問題</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">AEMaaCS アセットのローテーションの問題により、後続のローテーションが表示されない</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">（Dynamic Media）Adobe Experience Manager 6.5 Dynamic Mediaのスマート切り抜きの破損した画像の問題を解決する</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">Photoshop Firefly API統合のシングルパートアセットアップロード制限の増加</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">（Dynamic Media）PDF ファイルのAEM環境全体でDynamic Media アセット名の不一致を解決する</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">Adobe Experience Manager（AEM）as a Cloud Service - Assetでサムネールレンディションが表示されない画像がある</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">（Dynamic Media） Dynamic Mediaの一般設定ページが開かない</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">（Dynamic Media） AEMのDynamic Mediaでビデオファイルのオーディオの問題を解決する</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">AEM as a Cloud Serviceに新しくアップロードされたアセットの自動タグ付け</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">AEMでのJWTからOAuthへの移行後、スマートタグ機能が機能しない</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">AEM Managed Servicesでの共有リンクの問題の解決</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25607">（Dynamic Media） AEM Dynamic Mediaでのアセット処理のエラー</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">（Dynamic Media） Adobe Experience Manager（AEM） Dynamic Mediaでのアセット同期エラー</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">AEM as a Cloud Serviceでのビデオアセットのカスタムサムネールの更新</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">Adobe Experience Manager（AEM）Assetsでの画像メタデータの相違</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">AEM Assets Web UIへのアセットフォルダーのドラッグ&amp;ドロップに失敗する</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">（Dynamic Media） AEM as a Cloud Serviceでのアセット処理の問題の解決</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">Adobe Experience Manager as a Cloud Serviceでの大きなPDFのテキスト抽出の制限</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">（Asset Link）InDesignでのAdobe Experience Manager（AEM） Asset Link接続の問題の解決</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">（Asset Link） Adobe Asset Link Plug-In Network Error: Server is unreachable</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">（Dynamic Media） Dynamic Media同期のユーザーレコメンデーション</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">（Dynamic Media） APIを使用したDynamic Mediaからのアセットとメタデータの書き出し</a></td>
  <td></td>
</tr>

</tbody>
  <table>
