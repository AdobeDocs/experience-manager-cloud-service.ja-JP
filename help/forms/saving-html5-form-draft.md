---
title: HTML5 フォームのドラフトでの保存
description: HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 84%

---

# HTML5 フォームのドラフトでの保存 {#saving-an-html-form-as-a-draft}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開できます。フォームポータルを使用すると、すべてのユーザーが HTML5 フォームを保存および復元できます。「ドラフトとして保存」機能を有効にするには、プロファイルのノードに次の設定を追加します。

## 「ドラフトとして保存」機能を許可するためのカスタムプロファイル {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms では初期状態で「**ドラフトとして保存**」プロファイルを使用できます。「ドラフトとして保存」プロファイルを持つフォームをレンダリングすると、HTML5 フォームのドラフト機能を有効にすることができます。**Forms Manager** で、フォームに対する HTML レンダリングプロファイルを指定できます。

既存の[カスタムプロファイル](/help/forms/custom-profile.md)に対して「ドラフトとして保存」機能を有効にするには、カスタムプロファイルのノードに次のプロパティを追加します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>文字列</td>
   <td>true</td>
   <td><p>このプロファイルの「ドラフトとして保存」機能を</p> <p>有効にします。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>文字列</td>
   <td>true</td>
   <td><p>このプロファイルと一緒に添付ファイル</p> <p>をアップロードすることを許可します。</p> </td>
  </tr>
 </tbody>
</table>

## ドラフトの保存と一覧表示 {#drafts-storage-and-listing}

フォームの「ドラフトとして保存」機能を有効にした後、フォームを保存すると、ドラフトおよび送信コンポーネントにリストされます。 ドラフトと送信コンポーネントから保存しておいたフォームを取得して入力を開始できます。

ドラフトと送信コンポーネントのフォームの一覧表示を有効にするには、プロファイルのノードに次のプロパティを追加します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>文字列</td>
   <td>true</td>
   <td>ドラフトとフォームを送信した後、<br />フォームポータルのドラフトと送信コンポーネントに一覧表示できるようにします</td>
  </tr>
 </tbody>
</table>

デフォルトでは、AEM Forms はフォームのドラフトと送信に関連付けられたユーザーデータをパブリッシュインスタンスの /content/forms/fp ノードに保存します。カスタムのストレージプロバイダーを追加できます。詳細は、[ドラフトと送信コンポーネントのカスタムストレージ](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-forms-portal/adding-custom-storage-provider-forms)を参照してください。
