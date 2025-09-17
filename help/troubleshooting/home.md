---
title: AEM AssetsとFormsのトラブルシューティング
description: アップロード、メタデータ、検索、配信、フォームの作成、送信、統合などの主要な領域に関する記事リンクを使用して、AEM AssetsとFormsに関する一般的な問題のトラブルシューティングを行います。
hidefromtoc: true
hide: true
source-git-commit: 5074e777c68c51955b9ad8f055e04067163b9596
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 2%

---


# AEM AssetsとFormsの問題のトラブルシューティング {#troubleshoot-aem-assets-forms}

AEM as a Cloud Serviceは、AEM Assetsを通じたデジタルアセット管理およびAEM Formsを通じた強力なフォーム作成機能のための包括的なソリューションを提供しています。 どちらのサービスも、AI/ML などの次世代スマート機能を備えたクラウドネイティブな PaaS ソリューションを、常に最新、常に利用可能、常に学習可能なシステム内で提供します。

ただし、複雑なエンタープライズ環境では、様々な領域にわたる様々な技術的な課題に直面する可能性があります。

この包括的なトラブルシューティングガイドでは、AEM AssetsとFormsの両方に対して、体系的な診断アプローチ、分類されたソリューション、段階的な解決パスを提供します。 各セクションには、クイックリファレンスガイド、詳細なトラブルシューティング方法、問題を効率的に解決し AEM Cloud Service 環境を最適化するのに役立つ広範なリソースリンクが含まれています。

## AEM Assetsのトラブルシューティング {#aem-assets-troubleshooting}

AEM Assetsを使用すると、様々なエクスペリエンスをまたいでデジタルアセットを管理、整理、配信する方法が合理化されます。 ただし、アセットのアップロード、メタデータ、統合または配信に影響を与える問題が発生する場合があります。 この記事では、AEM Assetsに関する一般的な問題を診断して解決するのに役立つトラブルシューティング手順を説明します。 こちらのガイダンスに従うと、ワークフローを効率的に復元し、アセットがチャネル間でアクセス可能で正確かつ使用可能な状態を維持できます。

### アセットの処理とレンディション {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>アップロードと処理</strong></td>
    <td><strong>レンディション</strong></td>
    <td><strong>PDFとテキスト抽出</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Serviceでの大きな MP4 ファイルのアセット処理が失敗しました</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26639">DAM レンディションが元のファイルと一致しない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26785">AEMでは、大きな PDF から抽出されたテキストを 100,000 個のトークンの後で切り捨てます</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23916">ZIP 圧縮をアップロードした TIFF ファイルでレンディションが生成されない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26233">AEM as a Cloud Serviceのサムネールのレンディションが画像に表示されない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25518">AEM as a Cloud Serviceでの大きな PDF のテキスト抽出の制限</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-21865">アセットのフォルダーのAEM Assets Web UI へのドラッグ&amp;ドロップに失敗する</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26528">アセットの回転の問題により、後続の回転が見えなくなる</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26450">Photoshop Firefly API 統合のシングルパートアセットのアップロード制限を引き上げる</a></td>
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
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26533">AEMでのビデオのアップロード、処理、レンダリングの問題を修正しました</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26715">スピンセットが処理中の状態でスタックしています</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-17628">アセットの Dynamic Media URL の変更</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26677">Dynamic Media と DAM カード表示の間でビデオサムネールが一致しない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26873">AEM as a Cloud Serviceでスマート切り抜きレンディションが生成されない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26367">AEM 6.5 のスマート切り抜きに関する画像破損の問題</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM Dynamic Media でのアセット処理エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26637">TIFF レンディションの背景色の問題</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25294">Dynamic Media 一般設定ページが開かない</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26197">Dynamic Media を使用したビデオファイルのオーディオの問題の解決</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25885">Dynamic Media でのアセット同期の失敗</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26461">環境間でのアセット名の不一致の解決</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26871">下位の環境で Dynamic Media ビデオプレーヤーが機能しない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25471">Dynamic Media 同期のユーザーレコメンデーション</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26902">API を使用した Dynamic Media からのアセットとメタデータのエクスポート</a></td>
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
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25828">AEM Assetsの画像メタデータの不一致</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25925">新しくアップロードされたアセットの自動タグ付け</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26928">読み取りアクセス権にもかかわらずAssets ビューでコメントが制限される</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26655">管理者以外のユーザーに対するメタデータスキーマの表示の問題の解決</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25889">JWT から OAuth に移行した後、スマートタグが機能しない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25903">AEM Managed Servicesでの共有リンクの問題の解決</a></td>
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
      <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26922">Adobe Asset Link により、InDesignでリンクにアクセスできなくなる</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26616">AEM Assets ライセンスに含まれていないコンテンツフラグメント </a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25562">InDesignでのAEM Asset Link 接続の問題の解決</a></td>
      <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25525">AEM as a Cloud Serviceでのアセット処理の問題の解決</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25506">Adobe Asset Link プラグインのネットワークエラー：サーバーに到達できません</a></td>
      <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-25829">AEM as a Cloud Serviceのビデオアセットのカスタムサムネールの更新 </a>
      </td>
    </tr>
  </tbody>
</table>




## AEM Formsのトラブルシューティング {#aem-forms-troubleshooting}

AEM Forms as a Cloud Serviceは、フォームの強力な作成および管理機能を提供します。 ただし、インストール、設定、フォームの作成または送信プロセス中に問題が発生する場合があります。 このセクションでは、AEM Formsの一般的な問題に対する包括的なトラブルシューティングガイダンスを提供します。

### インストールと設定の問題

<table>
  <tbody>
  <tr>
    <td><strong>セットアップと設定</strong></td>
    <td><strong>フォーム作成の問題</strong></td>
    <td><strong>パフォーマンスとキャッシュ</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">ナビゲーションで「Forms」オプションを使用できない</a></td>
    <td><a href="/help/forms/form-creation-failing.md">テンプレートの公開後、フォームの作成に失敗する</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">アダプティブ Formsのキャッシュの問題</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">ビルドパイプラインのエラー</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">テンプレート公開シーケンスの問題</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Dispatcher キャッシュの無効化の問題</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">バンドルの有効化の問題</a></td>
    <td><a href="/help/forms/known-issues.md">既知のフォーム作成制限</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">CDN キャッシュエラー</a></td>
  </tr>
  </tbody>
</table>

### フォームの送信と統合に関する問題

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>カスタム送信アクション</strong></td>
    <td><strong>統合に関する問題</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403 フォーム送信での禁止エラー</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">カスタム送信アクションの 502 エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27434">DRM-SAML リダイレクト エラー</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">CORS 設定の問題</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">未処理の例外処理</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27075">AEM Sitesで「送信」ボタンが無効になる</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">リファラーフィルターの設定</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">カスタムアクションのベストプラクティス</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26532">アップグレード後の非表示フィールドの表示</a></td>
  </tr>
  </tbody>
</table>

### Designerと開発の問題

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>開発環境</strong></td>
    <td><strong>バージョンと互換性</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26558">アップグレード後にDesigner 6.5 が開かない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27089">ロケーターが JDK 8/11 で起動できない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26862">AEM Forms（AEMFD）パッケージバージョンの表示の問題</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-21018">PDF Generator JPEG 2000 エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-22689">JBoss ログパスの設定</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-26846">Windows のバージョン番号が正しくない</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-27406">PDF出力にボタンが表示されない</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-18084">Configuration Manager のアップグレード エラー</a></td>
    <td><a href="https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-17339">インデックスの破損の回避策</a></td>
  </tr>
  </tbody>
</table>



