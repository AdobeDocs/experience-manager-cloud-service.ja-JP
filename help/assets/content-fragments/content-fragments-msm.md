---
title: MSM およびライブコピーを使用したコンテンツフラグメントの再利用
description: MSM のライブコピー機能を使用して、ソースコンテンツと同期しながら、同じ（または類似した）コンテンツフラグメントコンテンツを複数の場所で使用する方法について説明します。
source-git-commit: 3ce1a982055c2f9c900edbd88e079deb6d3a036a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 20%

---

# MSM を使用したコンテンツフラグメントの再利用 {#reuse-content-fragments-using-msm}

マルチサイトマネージャー (MSM) とライブコピー機能を使用すると、同じコンテンツを複数の場所で使用しながら、ソースコンテンツと同期することができます。

* MSM ライブコピーを使用すると、次のことが可能になります。
   * コンテンツを 1 回作成し、
   * 同じサイト、他のサイト、またはアプリケーションの他の領域で、このコンテンツを再利用します。
* その後、MSM は次の目的でソースコンテンツとライブコピーの間のライブ関係を維持します。
   * ソースコンテンツを変更すると、ソースコピーとライブコピーが同期されます。
   * 個々のサブページやコンポーネントのライブ関係を解除することで、ライブコピーを微調整できます。

MSM の概念について詳しくは、 [コンテンツの再利用：マルチサイトマネージャーとライブコピー](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[マルチサイトマネージャ (MSM)](/help/sites-cloud/administering/msm/overview.md) Adobe Experience Managerの機能を使用すると、一度作成して複数の Web サイトで再利用したコンテンツを再利用できます。

MSM for Content Fragments を使用すると、次のことが可能になります。

* コンテンツフラグメントを 1 回作成してから、それらのフラグメントの（リンクされた）コピーを作成し、サイトやアプリケーションの他の領域で再利用します。
* 複数のコピーを同期したままにするには、ソースコピーを 1 回更新してから、変更を（ライブ）コピーにプッシュします。
* 親フラグメントと子フラグメントの間のリンクを一時的に、または恒久的に休止して、ローカルに変更を加えます。完全に休止するか、バリエーションやフィールドに変更を加えます。

MSM for Content Fragments とコンテンツフラグメントエディター内の機能を組み合わせると、フィールドレベルで継承を解除および復元できます。

>[!CAUTION]
>
>MSM for Content Fragments は、**Assets** コンソールからコンテンツフラグメントを使用している際にのみ使用できます。
>
>MSM の機能は、**コンテンツフラグメント**&#x200B;コンソールを使用している際は&#x200B;*使用できません*。

## 使い方 {#how-to}

MSM for Content Fragments(MSM for Content) の使用方法について詳しくは、次のドキュメントを参照してください (MSM for Content Fragments（AEM Assets にも適用可能）。

* 使用方法 [MSM for Content Fragments（および Assets）](/help/assets/reuse-assets-using-msm.md)

* [ライブコピーの作成](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >MSM を使用してコンテンツフラグメントのコピーを作成する場合は、 **ユニーク** 制約は、それぞれの [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md).

* [ソースとライブコピーのプロパティとステータスの表示](/help/assets/reuse-assets-using-msm.md#properties)
* [ソースからライブコピーに変更を反映](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* 次の継承のキャンセルと復元：
   * フィールドとバリエーション [コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [関連アセットのメタデータ](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [関係を休止して再開する](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [ライブ関係を削除](/help/assets/reuse-assets-using-msm.md#detach)
* [MSM for Content Fragments （および Assets）と MSM for Sites の比較](/help/assets/reuse-assets-using-msm.md#comparison)

## 制限事項 {#limitations}

* 変更時のトリガーと関連するロールアウト設定は、コンテンツフラグメントには存在しません。