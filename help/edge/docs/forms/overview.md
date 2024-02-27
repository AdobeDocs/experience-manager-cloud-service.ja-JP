---
title: AEM Forms Edge Delivery Service の概要
description: AEM Forms Edge Delivery Service は、効率化されたデータ収集とユーザーエンゲージメントの将来を想定できるように、最高のパフォーマンス向けに構築されています。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---


# AEM Forms Edge Delivery Service {#aem-forms-edge-delivery-service-overview}

AEM Forms Edge Delivery Service は、Adobeが提供する合成可能なサービスで、影響が大きく、パフォーマンスの高い Web フォームを作成して配信できます。 サービスを使用して以下のことが行えます。

* **見事なフォームを持つCaptivateユーザー**：事前に作成されたコンポーネントのライブラリを使用して、複雑で魅力的なフォームを簡単に作成できます。 reCAPTCHA の統合、電子メールへの直接の送信、シームレスなファイルアップロードを可能にし、SharePoint、Azure Storage、Amazon S3 などのセキュリティで保護されたストレージソリューションを実現します。 独自のカスタムフォームコンポーネントを作成して、独自のビジョンを生み出すこともできます。

  ![登録フォーム](/help/edge/assets/enrollment-form.png)

* **完璧な Lighthouse スコアを持つフォームの作成**：低速なインターネット接続でも、すばやく読み込んでレンダリングするフォームを構築します。 読み込み時間の短縮と最適化されたユーザーエクスペリエンスは、フォームの完了率の向上とコンバージョン率の向上に貢献します。

  ![フォームに最適な Lighthouse スコア](/help/edge/assets/lighthouse-forms.png)

* **お好みのツールでデジタル登録エクスペリエンスを作成**：コンテンツソースを分離することで、オーサリングの効率を向上させます。 標準では、AEM オーサリングとドキュメントベースのオーサリングの両方を使用できます。そのため、同じ Web サイト上で複数のコンテンツソースを操作し、Microsoft Excel、Googleシート、AEMエディターなどの好みのオーサリングツールを使用できます。

  ![Edge 配信フォームオーサリングツール](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## 基本事項から始めます

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="eds フォームを使用したフォームの作成" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Google Sheet またはMicrosoft Excel を使用したフォームの作成</b>
        </a>
        <p>モバイルデバイスで読み込んで自動的にレンダリングするフォームを作成します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="フォームを送信" alt="EDS フォームでのフォームフラグメントの使用" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フォームをスプレッドシートに送信</b>
        </a>
        <p>フォームをMicrosoft Excel またはGoogleシートに直接送信する。</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="スタイルまたはテーマを eds フォームに適用する" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">テーマのカスタマイズ</b>
        </a>
        <p>同じテーマを複数のフォームに適用して、一貫したブランドイメージを作成します。</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="フォームフィールドに検証機能を追加する" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フィールド検証を適用</b>
        </a>
        <p>フォーム入力で適切な形式を確認することで、エラーと不満を減らすことができます。</p>
    </div> 
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="EDS フォームの翻訳" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フォームの翻訳</b>
        </a>
        <p>コストを抑えながら、フォームのリーチを拡大します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="EDS フォームでのフォームフラグメントの使用" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">フォームフラグメントの作成</b>
        </a>
        <p>複数のフォーム間で事前設定済みのフラグメントを再利用する。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="EDS フォームに繰り返し可能なセクションを追加" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">繰り返し可能なセクションの追加</b>
        </a>
        <p>繰り返し可能なセクションを容易に作成し、フォームに追加できます。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="標準の JavaScript と CSS を使用したカスタムフォームコンポーネントの作成"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">カスタムコンポーネントの作成</b>
        </a>
        <p>標準の JavaScript と CSS を使用して、コンポーネントとテーマを作成します。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="EDS フォームでの reCAPTCHA の使用" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">reCAPTCHA を使用</b>
        </a>
        <p>堅牢なスパムとボット保護に、OOTB reCAPTCHA 統合を使用します。</p>
    </div>

</div>


</br>









