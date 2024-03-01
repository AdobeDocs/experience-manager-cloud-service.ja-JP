---
title: AEM Forms Edge 配信 サービス 概要
description: AEM Forms Edge 配信 サービス最高のパフォーマンスを実現するように構築されており、合理化されたデータ収集とユーザーエンゲージメントの未来を想像することができます。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1c6e44fd6652d93ba73bc2eb3604cd08eae7a33c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 3%

---


# AEM Forms Edge 配信 サービス

Adobe Systems の AEM Forms Edge 配信 サービスでフォーム作成を合理化し、完了率（ビジネスを）推進するを高めます。 この強力で構成可能なサービスにより、優れたパフォーマンスと視覚的な魅力を備えたエンタープライズグレードのフォームビルドことができます。 AEMは、ユーザーエクスペリエンスとビジネス目標の両方を優先し、超高速の読み込み時間とフォームの完了率の向上を保証します。

サービスを使用して以下のことが行えます。

* **見事なフォーム**&#x200B;でユーザーを魅了する: 事前定義済みコンポーネントのライブラリを使用して、複雑で魅力的なフォームを簡単にビルドできます。 reCAPTCHA を簡単に統合し、フォームを電子メールに直接送信し、シームレスなファイル アップロードを可能にして、Sharepoint、Azure Storage、Amazon S3 などの ストレージ ソリューションを保護します。 独自のカスタムフォームコンポーネントを作成して、独自のビジョンを実現することもできます。

* **選択した**&#x200B;ツールでデジタル登録エクスペリエンス作成: 内容ソースを分離することで、オーサリングの効率を高めます。 デフォルトでは、ドキュメントベースのオーサリング (Microsoft 365 と Google ワークスペース) とAEMオーサリング (AEM エディター) の両方を使用できます。 そのため、同じウェブサイトで複数の内容ソースを操作し、Microsoft Excel、Googleスプレッドシート、アダプティブFormsエディタなどのお好みのオーサリングツールを使用できます。

* **Lighthouse**&#x200B;スコアが完璧なビルドフォーム:低速のインターネット接続均等、すばやく読み込まれてレンダリングされるビルドフォーム。 読み込み時間の短縮とユーザーエクスペリエンスの最適化により、フォームの完了率が向上し、コンバージョン率が向上します。

  <div>
    <style>
    .image-container {
    width: 80%;
    text-align: center; 
    }
    .image-container img {
        width: 70%; /* Set image width to 70% of the container */
        border: .5px solid; /* Maintain the border style */
        padding: 15px; /* Maintain the padding */
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Forms 主な機能">
    </div>


</div>
&lt;!-- &gt;
**見事なフォームでユーザーを魅了する**:
事前定義済みコンポーネントのライブラリを使用して、複雑で魅力的なフォームを簡単にビルドできます。 reCAPTCHA を簡単に統合し、フォームを電子メールに直接送信し、シームレスなファイル アップロードを可能にして、Sharepoint、Azure Storage、Amazon S3 などの ストレージ ソリューションを保護します。 独自のカスタムフォームコンポーネントを作成して、独自のビジョンを実現することもできます。

    ![入学フォーム](/help/edge/アセット/enrollment-form.png)

* **灯台スコア**&#x200B;が完璧なビルドフォーム:低速のインターネット接続均等、すばやく読み込まれてレンダリングされるビルドフォーム。 読み込み時間の短縮とユーザーエクスペリエンスの最適化により、フォームの完了率が向上し、コンバージョン率が向上します。

  ![あなたのフォームにぴったりの灯台スコア](/help/edge/assets/lighthouse-forms.png)

* **選択した**&#x200B;ツールでデジタル登録エクスペリエンス作成: 内容ソースを分離することで、オーサリングの効率を高めます。 標準では、AEM オーサリングとドキュメントベースのオーサリングの両方を使用できます。そのため、同じWebサイトで複数の内容ソースを操作し、Microsoft Excel、Googleスプレッドシート、AEMエディターなどのお好みのオーサリングツールを使用できます。

  ![Edge 配信 フォームオーサリングツール](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## フォーム作成開始

<div>

<style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="EDS フォームを使用したフォーム作成" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Google シートまたは Microsoft Excel を使用したフォーム作成
            </b>
        </a>
        <p>作成 フォームの読み込みとレンダリングが、モバイル デバイス 上で迅速かつ自動的にリフローするフォームです。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="フォームを送信" alt="EDS フォームでのフラグメントフォームの使用" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">スプレッドシートへのフォームの送信
            </b>
        </a>
        <p>Microsoft Excel または Google スプレッドシートにフォームを直接送信します。</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="スタイルまたは EDS フォームへのテーマ適用" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">テーマをカスタマイズする
            </b>
        </a>
        <p>フォーム全体に同じテーマを適用することで、統一されたブランド画像作成ことができます。</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="フォームフィールドへの追加検証" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">適用フィールドの検証
            </b>
        </a>
        <p>フォーム入力が適切に書式設定されているかをチェックすることで、エラーやフラストレーションを軽減します。</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="ルールを使用してフォームに動的な動作を追加する" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">ルールを使用してフォームに動的な動作を追加する
            </b>
        </a>
        <p>事前設定されたフラグメントを複数のフォームで再利用します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="EDS フォームの翻訳" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">フォームを翻訳する
            </b>
        </a>
        <p>コストを抑えながらフォームの範囲を延ばします。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="繰り返し可能なセクションをEDSフォームに追加" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">繰り返し可能なセクション追加
            </b>
        </a>
        <p>繰り返し可能なセクションを簡単に作成し、フォームに追加できます。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="標準 JavaScript および CSS を使用したカスタムフォームコンポーネントの作成"  style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">カスタムコンポーネント作成
            </b>
        </a>
        <p>標準の JavaScript と CSS を使用してコンポーネントとテーマを作成します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="EDS フォームでの reCAPTCHA の使用" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">reCAPTCHA の使用
            </b>
        </a>
        <p>堅牢なスパムおよびボット保護のために、OOTB reCAPTCHA 統合を使用します。</p>
    </div>


</div>


</br>









