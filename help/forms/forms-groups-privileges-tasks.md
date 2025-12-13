---
title: AEM Forms as a Cloud Serviceでは、どのユーザーグループを標準で使用できますか？
description: すぐに使用できるユーザーグループと各グループに割り当てられた権限のリスト
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 81%

---

# グループと権限 {#aem-forms-on-osgi-groups-and-privileges}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

[グループを作成し](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=ja#accessing)、そのグループにポリシーと[ユーザー](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=ja#accessing)を割り当てることができます。これらのポリシーは、グループに含まれるユーザーの権限を制御します。

[!DNL AEM Forms] as a Cloud Service を設定すると、次の表に示すグループ（[!DNL forms-users]、forms-power-user など）を自動的に割り当てることができます。

<table>
 <tbody>
  <tr>
   <td>グループ</td> 
   <td>権限</td> 
  </tr>
  <tr>
   <td>[!DNL forms-users] <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームを作成、プレビュー、公開、送信する</li> 
    <!-- <li>Create, preview, and publish interactive communications and document fragments</li> -->
     <li>AEM インスタンスにアセットをアップロード</li> 
     <li>テーマを作成</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>[!DNL forms-power-user]</td> 
   <td>
    <ul> 
     <li>Create, preview, publish, and submit Adaptive Forms</li> 
     <li>Create, preview, and publish interactive communications and document fragments</li> 
     <li>Create scripts for Adaptive Forms using code editor</li> 
     <li>Upload assets including scripts</li> 
     <li>Create themes</li> 
     <li>Import packages containing XDP</li> 
    </ul> </td> 
  </tr>
 <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Review submissions</li> 
     <li>Approve or reject submissions</li> 
    </ul> </td> 
  </tr> -->
  <tr>
   <td>[!DNL template-authors] <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォーム <!-- or interactive communications --> テンプレートの作成とプレビュー</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>[!DNL fdm-authors]</p> </td> 
   <td>
    <ul> 
     <li>フォームデータモデルを作成および変更する</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Access Correspondence Management letters or interactive communications using Agent UI</li> 
    </ul> </td> 
  </tr> --> 
  <!-- <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> -->
    <!-- <li>Create an inbox application</li>  -->
    <!-- <li>Create a workflow model</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL workflow-users]</td> 
   <td>
    <ul> 
     <li>Use AEM inbox applications<br /> -->
     <!-- 
     <strong>Note: </strong>You must have cm-agent-users and [!DNL workflow-users] group assignments to access Interactive Communications Agent UI in AEM inbox.</li>  -->
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL fd-administrators]</td> 
   <td>
    <ul> 
     <!-- <li>Configure PDF Generator</li> --> 
     <!-- <li>Configure Watched folder</li> -->
     <li>ワークフローアプリケーションを管理する</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

## 適用性とユースケース

### 保険

## AEM Formsは保険業務に対してエンタープライズグレードですか？

はい。AEM Formsは、大規模な保険業務に必要な、役割ベースのアクセス制御、監査証跡、ワークフローの調整、ドキュメントの作成、柔軟な導入などのエンタープライズ機能を提供します。

## 関連トピック

* [Cloud Service 環境へのオンボード](/help/forms/setup-forms-cloud-service.md)
* [ローカル開発環境を設定](/help/forms/setup-local-development-environment.md)
* [AEM 6.5 Forms から Cloud Service への移行](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [スタンドアロンのアダプティブフォームを作成](/help/forms/creating-adaptive-form-core-components.md)
* [AEM Sites ページへ AEM アダプティブフォームを追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

<!--

>[!MORELIKETHIS]
>
>* [Use AEM Forms workflow for business process automation](/help/forms/aem-forms-workflow.md)

-->
