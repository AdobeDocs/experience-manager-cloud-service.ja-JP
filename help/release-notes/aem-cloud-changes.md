---
title: Adobe Experience Manager (AEM) as a Cloud Service の主な変更点
description: Adobe Experience Manager (AEM) as a Cloud Service の主な変更点
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 100%

---


# Adobe Experience Manager (AEM) as a Cloud Service の主な変更点 {#notable-changes-aem-cloud}

AEM as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。ただし、AEM as a Cloud Service と、オンプレミスまたは Adobe Managed Services の AEM Sites を比較すると、両者には数々の違いがあります。ここでは、重要な相違点について重点的に説明します。

>[!NOTE]
>このドキュメントでは、AEM as a Cloud Service 全体の主な変更点について重点的に説明します。ソリューションごとの変更点については、以下を参照してください。
>
>* [AEM Sites as a Cloud Service の主な変更点](/help/sites-cloud/sites-cloud-changes.md)
>* [AEM Assets as a Cloud Service の主な変更点](/help/assets/assets-cloud-changes.md)


主な違いは次の点にあります。

* [/apps と /libs が実行時に不変](#apps-libs-immutable)
* [OSGi バンドルおよび設定はリポジトリベース](#osgi)
* [パブリッシュリポジトリに対する変更は禁止](#changes-to-publish-repo)
* [カスタム実行モードは禁止](#custom-runmodes)
* [レプリケーションエージェントの削除](#replication-agents)
* [クラシック UI の削除](#classic-ui)
* [パブリッシュ側の配信](#publish-side-delivery)
* [アセットの操作と配信](#asset-handling)

## /apps と /libs が実行時に不変 {#apps-libs-immutable}

`/apps` および `/libs` 内のコンテンツとサブフォルダーはすべて読み取り専用です。それらの変更が必要な機能やカスタムコードは、変更に失敗します。コンテンツが読み取り専用である、または書き込み操作を完了できなかったというエラーが返されます。これは、次のように、AEM の様々な領域に影響を及ぼします。

* `/libs` では変更は一切できません。
   * これは新しいルールではありませんが、以前のオンプレミスバージョンの AEM では適用されていませんでした。
* `/libs` 内のオーバーレイ可能な領域のオーバーレイについては、`/apps` 内では引き続き可能です。
   * このようなオーバーレイは、CI/CD パイプラインを通じて Git から取得する必要があります。
* `/apps` に保存されている静的テンプレートデザイン情報は、UI では編集できません。
   * 代わりに、編集可能なテンプレートを利用することをお勧めします。
   * 静的テンプレートが引き続き必要な場合は、CI/CD パイプラインを通じて Git から設定情報を取得する必要があります。
* MSM ブループリントおよびカスタム MSM ロールアウト設定は、CI/CD パイプラインを通じて Git からインストールする必要があります。
* 多言語翻訳の変更は、CI/CD パイプラインを通じて Git から提供される必要があります。

## OSGi バンドルおよび設定はリポジトリベース {#osgi}

以前のバージョンの AEM で OSGi 設定の変更に使用されていた Web コンソールは、AEM as a Cloud Service では使用できません。したがって、OSGi の変更は CI/CD パイプラインを通じて導入する必要があります。

* OSGi 設定の変更は、JCR ベースの OSGi 設定として Git 永続性機能を通じてのみ取得できます。
* 新規または更新済みの OSGi バンドルは、CI/CD パイプラインのビルドプロセスの一環として Git を通じて導入する必要があります。

## パブリッシュリポジトリに対する変更は禁止 {#changes-to-publish-repo}

AEM as a Cloud Service では、パブリッシュリポジトリを直接変更することはできません。オンプレミス AEM または AMS 上の AEM の以前のバージョンでは、パブリッシュリポジトリ内のコードを直接変更して、例えばユーザーの作成、ユーザープロファイルの更新、ノードの作成などをおこなうことができました。この操作はおこなえなくなりましたが、代わりに次の方法を使用できます。

* コンテンツおよびコンテンツベースの設定については、オーサーインスタンス上で変更をおこなって公開します。
* コードと設定については、Git リポジトリ内で変更をおこない、CI/CD パイプラインを実行して変更をロールアウトします。
* フォーム送信やプロファイルデータなどのユーザー関連データについては、Experience Cloud プラットフォームまたは他のサードパーティ製セッション対応ストアの統一プロファイルサービスを利用します。

## カスタム実行モードは禁止 {#custom-runmodes}

AEM as a Cloud Service には、次の実行モードが標準で用意されています。

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

AEM as a Cloud Service では、追加またはカスタムの実行モードは使用できません。

## レプリケーションエージェントの削除 {#replication-agents}

AEM as a Cloud Service では、[Sling コンテンツ配布](https://sling.apache.org/documentation/bundles/content-distribution.html)を使用してコンテンツが公開されます。以前のバージョンの AEM で使用されていたレプリケーションエージェントは、使用も提供もされなくなりました。その結果、既存の AEM プロジェクトの次の領域に影響が出る可能性があります。

* 例えば、プレビューサーバーのレプリケーションエージェントにコンテンツをプッシュするカスタムワークフロー。
* レプリケーションエージェントのカスタマイズによるコンテンツの変換
* リバースレプリケーションを使用した、パブリッシュからオーサーへのコンテンツの返却

## クラシック UI の削除 {#classic-ui}

AEM as a Cloud Service ではクラシック UI が使用できなくなりました。

## パブリッシュ側の配信 {#publish-side-delivery}

AEM as a Cloud Service では、CDN やオーサーおよびパブリッシュサービスのトラフィック管理などの HTTP アクセラレーションがデフォルトで提供されます。

AMS 上やオンプレミスでのインストールからプロジェクトを移行する場合は、組み込みの CDN を利用することを強くお勧めします。AEM as a Cloud Service の機能は標準提供の CDN に最適化されているからです。

## アセットの操作と配信 {#asset-handling}

AEM as a Cloud Service では、アセットのアップロード、処理、ダウンロードが最適化されて効率がアップし、拡張性とアップロード／ダウンロード速度が向上しました。ただし、これによって、一部の既存カスタムコードが影響を受ける可能性があります。

* 以前のバージョンの AEM に用意されていたデフォルトの **DAM アセットの更新**&#x200B;ワークフローは使用できなくなりました。
* **変換をおこなわずに**&#x200B;バイナリを配信する Web サイトコンポーネントでは、直接ダウンロードを使用する必要があります。
   * Sling Get サーブレットは、デフォルトで直接ダウンロードをおこなうように変更されました。
* （サーブレットを介したサイズ変更などの）**変換をおこなって**&#x200B;バイナリを配信する Web サイトコンポーネントは、引き続きそのまま動作します。
* パッケージマネージャーで取り込まれたアセットについては、Assets インターフェイスの「**アセットを再処理**」アクションを使用して、手動で再処理する必要があります。
