---
title: 組み込みの  [!DNL AEM Forms] as a Cloud Service グループ
description: すぐに使用できるユーザーグループと各グループに割り当てられた権限のリスト
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: 8ac35abd1335b4e31a6dc0d8812cc9df333e69a4
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 78%

---

# グループと権限 {#aem-forms-on-osgi-groups-and-privileges}

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
     <li>アセットのAEMインスタンスへのアップロード</li> 
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

## 関連トピック

* [Cloud Service環境へのオンボーディング](/help/forms/setup-forms-cloud-service.md)
* [ローカル開発環境のセットアップ](/help/forms/setup-local-development-environment.md)
* [AEM 6.5 FormsからCloud Serviceへの移行](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [スタンドアロンのアダプティブフォームの作成](/help/forms/creating-adaptive-form-core-components.md)
* [アダプティブフォームをAEM Sitesページに追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)



