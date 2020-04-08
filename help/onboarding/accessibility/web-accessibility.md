---
title: クラウドサービスとしてのAdobe Experience ManagerとWebアクセシビリティのガイドライン
seo-title: クラウドサービスとしてのAdobe Experience ManagerとWebアクセシビリティのガイドライン
translation-type: tm+mt
source-git-commit: 6f86ad4feae9c4a1e9dc1defa8aaa930e632a0ef

---


# クラウドサービスとしてのAdobe Experience ManagerとWebアクセシビリティのガイドライン{#aem-and-the-web-accessibility-guidelines}

Web コンテンツは、身体的障碍や制限の有無に関係なく、対象読者ができるだけアクセスしやすくなるように設計すべきとして、様々な社会的、経済的、法的動機が生まれています。そのため、優れた Web デザインの一側面として、Web アクセシビリティの重要性が高まってきています。

クラウドサービスとしてのAdobe Experience Managerは、 [World Wide Web Consortiumが提供するガイドラインと連携します。 WCAG 2.1は、レベルAとレベルAAの準拠レベルの成功基準のリストを提供するガイドラインの現在のバージョンです。](#world-wide-web-consortium-and-wcag)

AEMをクラウドサービスとして使用して、アクセシブルなWebサイトやコンテンツを作成すると、次のような影響が生じます。

* 管理者は、Adobe Experience Manager（AEM）の設定を通して、アクセシビリティ機能が正しく有効化されるようにする必要があります。

* これらの機能を使用してアクセシブルなWebサイトを作成する作成者。

   * アクセシブルなコンテンツの作成はプロセスです。 AEM には各種機能が用意されていますが、コンテンツ作成者は、アクセスしやすいコンテンツを作成するために必要な手法に従う必要があります。

* テンプレート開発者も同様に、Web サイトデザインを実装する際に、こうした問題を認識する必要があります。

## WCAG 2.1およびクラウドサービスとしてのAEM {#wcag-aem-cloud-service}

次のAEMのクラウドサービスドキュメントのページとセクションで、情報とガイドラインを説明します。

<!--
* [Configuring the Rich Text Editor for Producing Accessible Sites](/help/sites-administering/rte-accessible-content.md)
 
  Guidelines on how administrators can configure AEM for producing accessible content.
-->

* [アクセス可能なコンテンツ（WCAG 2.1 適合）の作成 ](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

   WCAG 2.1ガイドラインは、レベルAとレベルAAの準拠レベルの成功基準のリストを示しています。 このページでは、AEM がカバーしている達成基準を詳しく取り上げるとともに、コンテンツ生成時にそれらの達成基準を満たす方法について説明しています。

* [WCAG 2.1のクイックガイド](/help/onboarding/accessibility/quick-guide-wcag.md)

   WCAG 2.1に関する背景情報です。

<!--
* [Creating Accessible Adaptive Forms](/help/forms/using/creating-accessible-adaptive-forms.md)
 
  Adobe Experience Manager (AEM) includes a number of features and capabilities that enhance the usability of adaptive forms for users with different abilities. The solution also assists form authors in creating accessible adaptive forms.
-->

## World Wide Web Consortium および WCAG 2.1 {#world-wide-web-consortium-and-wcag}

[World Wide Web Consortium（W3C）](https://www.w3.org/)は、Web 標準の策定を専門とする国際コミュニティです。To help web designers and developers produce accessible web sites the [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/) published the [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/) in June 2018.

>[!NOTE]
> 
> WCAG 2.1は、2008年の以前のバージョンWCAG 2.0を更新しました。 WCAG 2.1 - WCAG 2.0との比較を参照してください [](https://www.w3.org/TR/WCAG21/#comparison-with-wcag-2-0)。

<!--
> The original version, [WCAG 1.0](https://www.w3.org/TR/WCAG10/), was published in 1999.
-->

>[!NOTE]
> 
>An [updated version of the guidelines](https://www.w3.org/TR/WCAG22/) is currently in development, but will not be considered at this point in time.

Adobe Experience Manager を使用すると、コンテンツ作成者や Web サイトの所有者は、WCAG 2.1 レベル A およびレベル AA の達成基準を満たす Web コンテンツを作成できます。

[WCAG 2.1 クイックガイド](/help/onboarding/accessibility/quick-guide-wcag.md)で WCAG 2.1 の特定の側面を取り上げています。

### WCAG 2.1 アクセシビリティ適合レベル {#wcag-accessibility-conformance-levels}

WCAG 2.1 には、[該当するアクセシビリティレベルをカバーするガイドライン（および関連する達成基準）](https://www.w3.org/TR/WCAG/#conformance)が規定されています。

These, as they relate to AEM, are covered under [Level A and AA Conformance](/help/sites-cloud/authoring/fundamentals/accessible-content.md). サイトを作成する際は、サイトの全体的なレベルを特定する必要があります。

>[!NOTE]
> 
>特定のタイプのコンテンツでは、レベル AAA のすべての達成基準を満たすことはできないので、適合すべきレベルとしてお勧めすることはできません。

## Adobe におけるアクセシビリティ {#accessibility-at-adobe}

For additional information, please visit the [Adobe Accessibility Resource Center](https://www.adobe.com/accessibility/).


