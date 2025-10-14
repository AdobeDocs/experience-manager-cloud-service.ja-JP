---
title: 早期導入者とプレリリース機能を統合するための機能切り替えを有効にします
description: 機能の切り替えは、管理者がランタイム環境で新機能を有効にできる、AEMの機能です。
feature: Adaptive Forms, Foundation Components, Core Components
role: User, Developer
source-git-commit: cc4fccc51f487170bf6c14e4b302a8d5912c33a0
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---

# Adobe Experience Software Development Kit （AEM SDK）の機能を有効にする切り替え

AEMの機能の切り替え機能を使用すると、管理者は実行時に機能を有効または無効にでき、コードを変更せずに早期導入およびプレリリース機能を管理するのに最適です。 段階的なロールアウト、A/B テスト、不安定な機能の迅速な非アクティブ化をサポートします。

ここでは、AEMのローカル SDK設定で、SDKとDispatcherを使用してAEM as a Cloud Serviceをシミュレーションする、機能の切り替えを有効にする方法について説明します。 このセットアップにより、チームは、クラウドにデプロイする前に、実稼動環境のような環境でテストを行うことができます。

## AEM SDK設定で機能の切り替えを使用する理由

AEM SDKを設定して作業する場合、機能は次のヘルプを切り替えます。

* 実験的な機能を安全にテストする

* 新しいコンポーネントを段階的にロールアウトする。

* 複数の環境で単一のコードベースを維持する。

* 導入とアップグレードの際のリスクを軽減

## 前提条件

AEM SDK設定で機能の切り替えを有効にする前に、次を確認します。

* ユーザーは `forms-users` グループのメンバーです。

* `http://<author-instance-url>:portnumber/system/console/bundles` に移動し、**（com.adobe.granite.toggle.impl.dev-1.1.2.jar）** バンドルが存在するかどうかを確認します。 存在しない場合は [&#x200B; リンクからバンドルをダウンロード &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.2%20.jar)。

  ![&#x200B; 機能切り替え &#x200B;](/help/forms/assets/aem-web-console-bundle.png)

### 機能切替スイッチの有効化

AEM SDK インスタンスで機能の切り替えを有効にするには、次の手順に従います。

1. AEM Forms インスタンスにログインします。

1. `http://author-instance-url:portnumber/system/console/configMgr` に移動します。

1. Configuration Manager で、Adobe Granite Dynamic Toggle Provider を検索します。

   ![&#x200B; 機能切り替え &#x200B;](/help/forms/assets/aem-web-console-confi.png)

1. のアイコンをクリック ✏️ ます。
1. 「有効な切り替え」セクションで、➕ をクリックします。
1. 以下の画像に示すように、機能の機能切り替え ID を追加します。
   ![&#x200B; 機能切り替え &#x200B;](/help/forms/assets/feature-toggle.png)

1. 「保存」をクリックします

>[!NOTE]
>
> 機能の切り替え ID は、早期導入者機能に固有のドキュメントで確認できます。


### 機能切り替えを無効にする

切り替えが有効になっている機能の機能の切り替えを無効にするには、次の手順に従います。

1. AEM Forms インスタンスにログインします。
1. `http://author-instance-url:portnumber/system/console/configMgr` に移動します。
1. Configuration Manager で、Adobe Granite Dynamic Toggle Provider を検索します。
1. アイコン ✏️ をクリックします。
1. 「無効な切り替え」セクションで、「➕ り替え」をクリックします。
1. 無効にする機能のトグル番号を追加します。

   ![&#x200B; 機能切り替え &#x200B;](/help/forms/assets/disable-toggle-feature.png)

### 技術的な考慮事項

機能の切り替えは実行時に管理され、開発やテストの設定に最適です。 AEM SDKの設定で、切り替えがバージョン管理されており、CI/CD と同期されていることを確認します。 変更を反映するには、ページの更新またはキャッシュのクリアが必要になる場合があります。

>[!NOTE]
>
> 実稼動環境で機能の切り替えを有効にするには、Adobe サポートチームにお問い合わせください。

