---
title: MSM およびライブコピーを使用したコンテンツフラグメントの再利用
description: MSM のライブコピー機能を使用して、ソースコンテンツと同期しながら、同じまたは類似のコンテンツフラグメントコンテンツを複数の場所で使用する方法について説明します。
exl-id: f050b2d1-856c-4cdb-ac74-bc78016f144a
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 100%

---

# MSM を使用したコンテンツフラグメントの再利用 {#reuse-content-fragments-using-msm}

マルチサイトマネージャー（MSM）とライブコピー機能を使用すると、ソースコンテンツと同期しながら、複数の場所で同じコンテンツを使用できます。

* MSM ライブコピーを使用すると、次のことができます。
   * コンテンツを 1 回作成してから
   * このコンテンツを、同じサイトまたは他のサイトの他の領域か、同じアプリケーションまたは他のアプリケーションの他の領域で再利用する。
* その後、MSM は次の目的でソースコンテンツとライブコピーの間のライブ関係を維持します。
   * ソースコンテンツを変更すると、ソースコピーとライブコピーが同期されます。
   * 個々のサブページやコンポーネントのライブ関係を解除して、ライブコピーのコンテンツのみを調整できます。

MSM の概念の詳細な概要については、[コンテンツの再利用：マルチサイトマネージャーとライブコピー](/help/sites-cloud/administering/msm/overview.md)を参照してください。

>[!NOTE]
>
>Adobe Experience Manager の[マルチサイトマネージャー（MSM）](/help/sites-cloud/administering/msm/overview.md)機能を使用すると、一度作成したコンテンツを複数の Web サイトで再利用できます。

MSM for Content Fragments を使用すると、次のことができます。

* コンテンツフラグメントを 1 回作成してから、これらのフラグメントの（リンクされた）コピーを作成して、サイトまたはアプリケーションの他の領域で再利用する。
* ソースコピーを 1 回更新してから、変更を（ライブ）コピーにプッシュして、複数のコピーの同期を維持する。
* 親フラグメントと子フラグメントの間のリンクを完全に、またはそのバリエーションやフィールドに関して、一時的または永続的に休止し、ローカルに変更を行う。

MSM for Content Fragments をコンテンツフラグメントエディター内の機能と組み合わせると、フィールドレベルで継承を解除および復元できます。

>[!CAUTION]
>
>MSM for Content Fragments は、**Assets** コンソールからコンテンツフラグメントを使用している際にのみ使用できます。
>
>MSM の機能は、**コンテンツフラグメント**&#x200B;コンソールを使用している際は&#x200B;*使用できません*。

## 方法 {#how-to}

MSM for Content Fragments の使用方法について詳しくは、次のドキュメントを参照してください（Assets にも適用可能）。

* [MSM for Content Fragments（および Assets）](/help/assets/reuse-assets-using-msm.md)の使用方法

* [ライブコピーの作成](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >コンテンツフラグメントのコピーを作成する MSM を使用する場合は、それぞれの[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)で使用されているすべてのデータタイプから&#x200B;**一意**&#x200B;の制約を削除する必要があります。

* [ソースおよびライブコピーのプロパティとステータスの表示](/help/assets/reuse-assets-using-msm.md#properties)
* [ソースからライブコピーへの変更の伝達](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* 次の継承のキャンセルと復元：
   * [コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md#inheritance)のフィールドとバリエーション
   * [関連アセットのメタデータ](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [関係の休止と再開](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [ライブ関係の削除](/help/assets/reuse-assets-using-msm.md#detach)
* [MSM for Content Fragments（および Assets）と MSM for Sites の比較](/help/assets/reuse-assets-using-msm.md#comparison)

## 制限事項 {#limitations}

* 変更時のトリガーと関連するロールアウト設定は、コンテンツフラグメントには存在しません。
