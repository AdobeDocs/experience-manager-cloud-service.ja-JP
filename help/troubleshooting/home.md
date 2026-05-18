---
title: AEM AssetsとFormsのトラブルシューティング
description: アップロード、メタデータ、検索、配信、フォーム作成、送信、統合などの主要領域の記事リンクを使用して、AEM AssetsとFormsの一般的な問題をトラブルシューティングします。
hide: true
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
exl-id: 73ff9249-6f5a-46c1-87fe-7cb50b000927
source-git-commit: 77f7d21eed1322de768ee07e3518638f60e3ae40
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 1%

---

# AEM AssetsとFormsの問題のトラブルシューティング {#troubleshoot-aem-assets-forms}

AEM as a Cloud Serviceは、AEM Assetsを通じたデジタルアセット管理と、AEM Formsを通じた強力なフォーム作成機能のための包括的なソリューションを提供します。 どちらのサービスも、AIやマシンラーニングなどの次世代のスマート機能を備えたクラウドネイティブのPaaS ソリューションを提供します。これらはすべて、常に最新の状態で、利用可能であり、継続的に学習されるシステム内で利用できます。

しかし、複雑な企業環境では、さまざまな分野で様々な技術的課題に直面する可能性があります。

この包括的なトラブルシューティングガイドでは、AEM AssetsとFormsの両方について、体系的な診断アプローチ、分類されたソリューション、ステップバイステップの解決パスについて説明します。 各セクションには、クイックリファレンスガイド、詳細なトラブルシューティング手法、問題を効率的に解決し、AEM Cloud Service環境を最適化するのに役立つ豊富なリソースリンクが含まれています。

## AEM Assetsのトラブルシューティング {#aem-assets-troubleshooting}

AEM Assetsなら、エクスペリエンス全体でデジタルアセットを効率的に管理、整理、配信できます。 ただし、アセットのアップロード、メタデータ、統合、配信に影響を与える問題が発生する場合があります。 この記事では、AEM Assetsの一般的な問題の診断と解決に役立つトラブルシューティング手順について説明します。 このガイダンスに従うことで、ワークフローを効率的に復元し、アセットにアクセスしやすく、正確で、チャネル全体で活用できるようにすることができます。

### アセットの処理とレンディション {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>アップロードと処理</strong></td>
    <td><strong>レンディション</strong></td>
    <td><strong>PDFとテキスト抽出</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Serviceで大きなMP4 ファイルのアセット処理に失敗しました</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">DAM レンディションがオリジナルファイルと一致しない</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEMでは、100,000個のトークンの後に、大きなPDFから抽出したテキストが切り捨てられます</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">ZIP圧縮でアップロードされたTiff ファイルはレンディションを生成しません</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">AEM as a Cloud Serviceでサムネールレンディションが表示されない画像</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">AEM as a Cloud Serviceでの大きなPDFのテキスト抽出の制限</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">AEM Assets Web UIへのアセットフォルダーのドラッグ&amp;ドロップに失敗する</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">アセットの回転の問題により、後続の回転が表示されない</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">Photoshop Firefly API統合のシングルパートアセットアップロード制限の増加</a></td>
  <td></td>
  <td></td>
  </tr>
  </tbody>
</table>

### Dynamic Media {#dynamic-media-issues}

<table>
  <tbody>
  <tr>
    <td><strong>ビデオ</strong></td>
    <td><strong>スピンセットとスマート切り抜き</strong></td>
    <td><strong>配信と設定</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533">AEMでのビデオのアップロード、処理、レンダリングの問題の修正</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715">スピンセットが処理状態で停止する</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">アセットのDynamic Media URLの変更</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">Dynamic MediaとDAM カードビュー間のビデオサムネールの不一致</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">AEM as a Cloud Serviceでスマート切り抜きレンディションが生成されない</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">AEM 6.5でのスマート切り抜きに関する破損した画像の問題</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM Dynamic Mediaでのアセット処理のエラー</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">TIFF レンディションの背景色の問題</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">Dynamic Mediaの一般設定ページが開かない</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">Dynamic Mediaでビデオファイルのオーディオの問題を解決する</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">Dynamic Mediaでのアセット同期エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">環境をまたいでアセット名の不一致を解決する</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">低い環境でDynamic Media ビデオプレーヤーが機能しない</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">Dynamic Media同期のユーザーレコメンデーション</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">APIを使用したDynamic Mediaからのアセットとメタデータの書き出し</a></td>
  </tr>
  </tbody>
</table>

### メタデータ、タグ付け、共有 {#metadata-tagging-sharing-issues}

<table>
  <tbody>
  <tr>
    <td><strong>メタデータ</strong></td>
    <td><strong>スマートタグ</strong></td>
    <td><strong>アクセスと共有</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">AEM Assetsの画像メタデータの不一致</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">新しくアップロードされたアセットの自動タグ付け</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">読み取りアクセスにもかかわらず、Assets ビューでのコメントが制限される</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">管理者以外のユーザーのメタデータスキーマの表示に関する問題の解決</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">JWTからOAuthへの移行後にスマートタグが機能しない</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">AEM Managed Servicesでの共有リンクの問題の解決</a></td>
  </tr>

</tbody>
</table>

### 統合とアクセス {#integrations-access}

<table>
  <tbody>
    <tr>
      <td><strong>Asset Link</strong></td>
      <td><strong>ライセンスとカスタマイズ</strong></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922">Adobe Asset LinkでInDesignのリンクにアクセスできない</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">AEM Assets ライセンスに含まれていないコンテンツフラグメント </a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">InDesignでのAEM Asset Link接続の問題の解決</a></td>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">AEM as a Cloud Serviceでのアセット処理の問題の解決</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">Adobe Asset Link Plug-In Network Error: Server unreach</a></td>
      <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">AEM as a Cloud Serviceのビデオアセットのカスタムサムネールを更新しています</a>
      </td>
    </tr>
  </tbody>
</table>




## AEM Formsのトラブルシューティング {#aem-forms-troubleshooting}

AEM Forms as a Cloud Serviceは、強力なフォーム作成機能と管理機能を提供します。 ただし、インストール、設定、フォーム作成、または送信プロセス中に問題が発生する場合があります。 この節では、AEM Formsの一般的な問題に対する包括的なトラブルシューティングガイダンスを提供します。

### インストールと設定の問題

<table>
  <tbody>
  <tr>
    <td><strong>設定と設定</strong></td>
    <td><strong>フォーム作成の問題</strong></td>
    <td><strong>パフォーマンスとキャッシュ</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">Forms オプションはナビゲーションで使用できません</a></td>
    <td><a href="/help/forms/form-creation-failing.md">テンプレートの公開後にフォームの作成が失敗する</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">アダプティブ Formsのキャッシュに関する問題</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">パイプラインの作成エラー</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">テンプレートの公開シーケンスの問題</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Dispatcher キャッシュの無効化に関する問題</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">バンドルアクティベーションの問題</a></td>
    <td><a href="/help/forms/known-issues.md">既知のフォーム作成の制限</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">CDN キャッシュの失敗</a></td>
  </tr>
  </tbody>
</table>

### フォームの送信と統合の問題

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>カスタム送信アクション</strong></td>
    <td><strong>統合の問題</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403 フォーム送信時の禁止エラー</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">カスタム送信アクションの502 エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27434">DRM-SAML リダイレクト エラー</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">CORS設定の問題</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">未処理の例外処理</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27075">AEM Sitesで「送信」ボタンが無効になっている</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">リファラーフィルター設定</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">カスタムアクションのベストプラクティス</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26532">アップグレード後の非表示フィールドの表示</a></td>
  </tr>
  </tbody>
</table>

### Designerと開発問題

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>開発環境</strong></td>
    <td><strong>バージョンと互換性</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26558">アップグレード後にDesigner 6.5が開かない</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27089">ロケーターがJDK 8/11で開始できない</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26862">AEM Forms（AEMFD）パッケージのバージョン表示の問題</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21018">PDF Generator JPEG 2000 エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-22689">JBoss ログパス設定</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26846">Windowsのバージョン番号が正しくない</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27406">PDF出力にボタンがありません</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-18084">Configuration Managerのアップグレード エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17339">インデックス破損の回避策</a></td>
  </tr>
  </tbody>
</table>
