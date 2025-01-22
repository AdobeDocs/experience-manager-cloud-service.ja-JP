---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.1.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2025.1.0 のリリースについて説明します。
feature: Release Information
role: Admin
source-git-commit: bf12306969581723e4e9ce1517a8f0d445f26521
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 22%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2025.1.0 のリリースノート {#release-notes}

AEM（Adobe Experience Manager）as a Cloud Service の Cloud Manager 2025.1.0 のリリースについて説明します。

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service の最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## リリース日 {#release-date}

AEM as a Cloud ServiceのCloud Manager 2025.1.0 のリリース日は 2025 年 1 月 22 日（水）です。

次回のリリース予定は 2025年2月13日（PT）です。


## 新機能 {#what-is-new}

* **コード品質ルール：** Cloud Managerのコード品質ステップは、2025 年 2 月 13 日木曜日（PT）に予定されているCloud Manager 2025.2.0 リリースで SonarQube Server 9.9 の使用を開始します。

準備のために、更新された SonarQube ルールが [ コード品質ルール ](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) で利用できるようになりました。

次のパイプラインテキスト変数を設定して、新しいルールを「アーリーチェック」できます。

`CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

さらに、次の変数を設定して、コード品質ステップが同じコミットに対して実行されるようにします（通常、同じコ `commitId` ットに対してスキップされます）。

`CM_DISABLE_BUILD_REUSE` = `true`

![ 変数設定ページ ](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobeでは、メインの実稼動パイプラインと同じブランチに設定された新しい CI/CD コード品質パイプラインを作成することをお勧めします。 2025 年 2 月 13 日（PT）リリースより前に *適切な変数を設定し、新しく適用されたルールにブロッカーが導入されないことを検証します*。

* **Java 17 および Java 21 ビルドサポート：** お客様は、Java 17 または Java 21 を使用してビルドできるようになり、パフォーマンスの強化や新しい言語機能にアクセスできます。 Maven プロジェクトおよびライブラリのバージョンの更新など、設定手順については、[ ビルド環境 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) を参照してください。 ビルドバージョンが Java 17 または Java 21 に設定されている場合、デプロイされるランタイムは Java 21 です。

   * **機能の有効化**
      * この機能は、2025 年 2 月 13 日木曜日（PT）に、新しい SonarQube バージョンのデフォルトのロールアウトと同時に、すべてのお客様に対して有効になります。
      * お客様は、上記の 2 つの変数設定を設定して *すぐに* 有効にし、SonarQube 9.9 バージョンをアップグレードできます。

   * **Java 21 ランタイムのデプロイメント**
      * Java 21 ランタイムは、Java 17 または Java 21 でビルドする場合にデプロイされます。
      * すべてのCloud Manager環境への段階的なロールアウトは 2 月にサンドボックスと開発環境で始まり、4 月に実稼動環境に拡張されます。
      * Java 21 ランタイム *以前* の導入を希望するお客様は、Adobe（[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) までお問い合わせください。


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
