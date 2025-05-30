---
title: レコードのドキュメントテンプレートを作成するために Forms Designer をダウンロードしてインストールする方法
description: Forms Designer を使用して、レコードのドキュメントテンプレートとして機能する XDP および PDF フォームテンプレートを作成できます。
keywords: Designer のインストール、Forms Designer のインストール、Forms Designer のインストール要件
feature: Adaptive Forms, Forms Designer
role: Admin, Developer, User
exl-id: d6f1cb21-c48b-406d-8d47-482d7a1b4cc3
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 100%

---

# Forms Designer のダウンロードとインストール {#installing-and-configuring-designer}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | この記事 |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html?lang=ja) |

Designer は、XDP および PDF フォームテンプレートの作成を簡単にするポイント＆クリックによるグラフィカルフォームデザインツールです。フォームテンプレートをデザインし、そのロジックを定義して、厳密な法的要件を満たすことができます。XDP および PDF フォームは、アダプティブフォーム内のレコードのドキュメントテンプレートとして機能します。これらのフォームテンプレートは、[アダプティブフォームテンプレート](template-editor.md)とは異なります。

## 前提条件 {#pre-requisites}

最新バージョンの AEM Forms Designer 64 ビットまたは 32 ビットをインストールするには、次のソフトウェアと最小ハードウェアで Designer をインストールして設定する必要があります。

+++ 64 ビット Designer（推奨）

* [!DNL Microsoft® Windows® 2016 Server] または [!DNL Microsoft® Windows® 2019 Server]、および [!DNL Microsoft® Windows® 10]
* 最低 2 GB の RAM
* 20 GB のディスク容量
* グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
* 2.35 GB のハードディスク空き容量
* 1024 x 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC。
* Designer をインストールするための管理者権限。
* [!DNL Microsoft® Visual C++ 2019]（VC 14.28 以降）64 ビットランタイム

+++

+++ 32 ビット Designer

* [!DNL Microsoft® Windows® 2016 Server]、[!DNL Microsoft® Windows® 2019 Server] または [!DNL Microsoft® Windows® 10]
* 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
* 16 GB のディスク容量（32 ビット OS の場合）または 20 GB のディスク容量（64 ビット OS の場合）
* グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
* 2.35 GB のハードディスク空き容量
* 1024 x 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC。
* Designer をインストールするための管理者権限。
* Microsoft® Visual C++ 2019（VC 14.28 以降）32 ビットランタイム

+++

## Designer をインストール {#install-designer}

>[!NOTE]
>
> 64 ビット版の Forms Designer をインストールする前に、32 ビット版の Designer をアンインストールします。

Designer をインストールするには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)から Designer をダウンロードします。
1. setup.exe をダブルクリックし、インストーラーを実行します。
1. 先に進み、パーソナライゼーション画面で詳細を入力します。
1. 使用許諾契約に同意する場合は、「**[!UICONTROL 次へ]**」をクリックして先に進みます。
1. （オプション）デフォルトのインストールパスを変更して、選択した場所に Designer をインストールします。「**[!UICONTROL 次へ]**」をクリックします。
1. 設定を変更するには、「**[!UICONTROL 戻る]**」をクリックします。Designer をインストールするには、「**[!UICONTROL インストール]**」をクリックします。
1. インストールが完了したら、「**[!UICONTROL 完了]**」をクリックします。

## 関連トピック {#see-also}

* [カスタムフォントを使用](/help/forms/use-custom-fonts.md)
* [スタンドアロンのコアコンポーネントベースのアダプティブフォームを作成](/help/forms/creating-adaptive-form-core-components.md)
* [AEM Sites ページへのアダプティブフォームの作成または追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Forms Designer を使用して、レコードのドキュメント（DoR）のテンプレートとフォームフラグメントを作成](/help/forms/use-forms-designer.md)


<!--

>[!MORELIKETHIS]
>
>* [Use Forms Designer to create Document of Record (DoR) templates and form fragments](/help/forms/use-forms-designer.md)

-->