---
title: 専用のテスト環境の追加
description: Cloud Managerのスペシャライズドテスト環境で、ストレステストや高度なプレデプロイメントチェックに最適な、ほぼ実稼動環境で機能を検証するための専用スペースを提供する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 815fb5c3-a171-4531-8727-b79183d85f06
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 33%

---

# 専用のテスト環境の追加{#add-special-test-enviro}

<!--
 badge: label="Private beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
-->

>[!NOTE]
>
>専用のテスト環境が購入可能になりました。 Adobeの担当者に連絡して注文してください。


Specialized Testing Environmentは、新しいタイプのCloud Manager環境です。 これは、ユーザー受け入れテスト（UAT）やパフォーマンス検証などの高度なユースケースをサポートするように設計されています。 従来の開発、高速開発、ステージング環境とは異なり、専用テスト環境は実稼動デプロイメントパイプラインの外で動作します。 そのため、厳格な分離を維持しながら柔軟性を高め、制作ワークフローへの干渉を防ぐことができます。

専用テスト環境は、一般的なステージング環境のサイズ、スケーラビリティ、設定をミラーリングするように構築されています。 このアプローチにより、専用テスト環境で実行されたテストによって、実稼動環境でのコードとコンテンツのパフォーマンスに関する現実的なインサイトを得ることができます。 この環境では、実稼動環境またはステージから直接コンテンツをコピーすることもできます。 また、デプロイメントワークフロー、アクセス制御、ネットワーク設定の面で、開発環境との整合性も維持します。

## 専用テスト環境の主な機能と構成 {#key-features}

| カテゴリ | 動作 |
| --- | --- |
| 目的 | UATとパフォーマンステスト： |
| パイプラインタイプ | パイプラインにありません。 |
| 環境サイズ | ステージング環境に一致します。 |
| 分離 | 他の環境から完全に隔離されています。 |
| コードパイプライン | 開発環境（検証、ビルド、デプロイ）と同じです。 |
| コンテンツをコピー | 実稼動環境、ステージング環境、または専用のテスト環境から許可されます。 |
| コンテンツ復元 | 開発環境と同じです。 |
| アクセスログ | 開発環境と同じです。 |
| Developer Console | 開発環境と同じです。 |
| `IP Allow List` | 開発環境と同じです。 |
| ネットワーク | 開発環境（サービス、ドメイン名、SSL証明書、高度なネットワーク）と同じです。 |

詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)も参照してください。

## 専用のテスト環境の追加 {#add-specialized-testing-environment}

環境を追加または編集するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;の役割のメンバーである必要があります。

**特殊なテスト環境を追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、環境を追加するプログラムをクリックします。

1. 次のいずれかの操作を行います。

   * **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールの&#x200B;**環境** カードで、**環境を追加**をクリックします。
「**環境を追加**」オプションがグレー表示（無効）になっている場合は、権限が不足しているか、ライセンス済みリソースに依存している場合があります。

     ![環境カード](assets/no-environments.png)

   * 左側のサイドパネルで、![データアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)「**環境**」をクリックし、環境ページの右上隅近くにある「**環境を追加**」をクリックします。

     ![「環境」タブ](assets/environments-tab.png)

1. **環境を追加**&#x200B;ダイアログボックスで、次の操作を行います。

   * **特殊テスト環境**&#x200B;をクリックします。
   * 環境の&#x200B;**名前**&#x200B;を入力します。環境名は、環境の作成後に変更できません。
   * （オプション）環境に&#x200B;**説明**&#x200B;を指定します。
   * ドロップダウンリストから&#x200B;**プライマリリージョン**&#x200B;を選択します。 作成すると、スペシャライズド・テスト環境のプライマリ領域（例：*英国（南）*）はロックされ、変更できません。

     ![「専用のテスト環境」ラジオボタンが選択された「環境を追加」ダイアログボックス](assets/specialized-test-environment.png)

1. 「**保存**」をクリックします。

   これで、**概要**&#x200B;ページの&#x200B;**環境**&#x200B;カードに新しい環境が表示されるようになりました。新しい環境にパイプラインを設定できるようになりました。

## その他のリソース {#additional-resources}

* ビデオ：[AEM Cloud Managerの環境タイプについて](https://experienceleague.adobe.com/en/perspectives/cloud-manager-environment-types)
* [環境の管理](/help/implementing/cloud-manager/manage-environments.md)

