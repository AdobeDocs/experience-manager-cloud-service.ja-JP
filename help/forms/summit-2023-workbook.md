---
title: コアコンポーネントとヘッドレスを使用して魅力的なFormsを構築
seo-title: Build Engaging Forms Using Core Components and Headless
description: コアコンポーネントとヘッドレスを使用して魅力的なFormsを構築
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: 26a4450c8b722fd4ca074abb3c260983c1ae0c64
workflow-type: tm+mt
source-wordcount: '3411'
ht-degree: 3%

---


# コアコンポーネントとヘッドレスを使用して魅力的なFormsを構築

## ラボの概要

この実践ラボでは、次のことを学習します。

AEM Formsを使用してAEM Sitesと一貫性のある最新のコアコンポーネントを簡単にアダプティブフォームを作成する方法。アダプティブフォームをヘッドレスフォームとして Web、モバイル、チャットに配信することで、オムニチャネルのデータ取得機能を有効にします。 また、スタイル設定、カスタマイズ、フロントエンド開発に関するベストプラクティスについても学習します。

## 重要な留意点

* **ビジネスの俊敏性**:ビジネスユーザーは、複数のチャネル用のフォームエクスペリエンスを簡単に作成できます。

* **フロントエンド開発者に対するパワー**:フロントエンド開発者は、ヘッドレスフォームを使用してエンドユーザーエクスペリエンスを制御できます。

* **開発者の速度**:開発者は、 Sites コンポーネントとFormsコンポーネントを簡単かつ一貫してカスタマイズできます。

## 前提条件


+++AEM FormsをCloud Serviceサンドボックスとして



<table>
        <thead>
            <tr><th>name</th><th>オーサーインスタンス URL</th><th>パブリッシュインスタンス URL</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## レッスン 1

### 目的

AEM Forms as a Cloud Service環境の理解。

### レッスンのコンテキスト

このレッスンでは、ユーザーインターフェイスを移動して、 AEM Formsas a Cloud Serviceの環境について理解します。

### 演習

1. ブラウザーを開き、ブラウザーオーサー環境の URL をCloud Serviceします。 次に例を示します。
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Cloud Serviceオーサー環境にログインします。 ラボでは、オーサー環境のログイン資格情報が共有されます。

1. ログインした後、AEM Forms UI に移動します。 クリック **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. クリック **Forms &amp; Documents**. 環境設定や情報に関連するポップアップを解除します。

   ![](/help/forms/assets/screenshot2028113929.png)

   使用可能なすべてのフォームが表示されます。

   ![](/help/forms/assets/screenshot2028114029.png)

## レッスン 2

### 目的

最新のコアコンポーネントを使用してアダプティブフォームを作成し、フォームを設定して送信します。

### レッスンのコンテキスト

このレッスンでは、ビジネスユーザーとして、データ取得用の標準化された OOTB コアコンポーネントを使用したアダプティブフォームオーサリングを使用して、Web、モバイル、チャットなど複数のチャネル用のアダプティブフォームを作成します。

### 演習

1. フォームの送信エンドポイントを作成します。

   1. 開く <https://requestbin.com/> をクリックします。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. クリック **公開 bin の作成** エンドポイント URL をコピーします。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. ウィザードインターフェイスを使用してアダプティブフォームを作成するには、次の手順を実行します。

   1. レッスン 1 で使用するブラウザータブで、 AEM Forms as aCloud ServiceWeb インターフェイスに移動し、 Formsとドキュメントに移動します。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. クリック **作成** 「アダプティブフォーム」を選択します。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. を選択します。 **コアコンポーネントで空白** テンプレートを選択画面から選択します（下図を参照）。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 次をクリック： **スタイル** 」タブで「 **wknd-theme** テーマを次に示します。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 次をクリック： **送信** 」タブで「 **REST エンドポイントに送信** カードを選択し、
      **POST要求の URL** フィールドには次のように表示されます。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 「**作成**」をクリックします。フォームの名前とタイトルを指定します。 例： **接触**. 「**作成**」をクリックします。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. アダプティブフォームエディターが開きます。 ポップアップまたはダイアログを閉じて、環境設定や情報を表示します。 左側のパネルでコンポーネントブラウザーをクリックし、 **フッター** コンポーネントを空白のフォームの下部に配置します。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. ヘッダーは、アダプティブフォームテンプレートの一部です。 これにより、すべてのアダプティブフォームで一貫したヘッダー/フッターを簡単に提供できます。 または、次の手順のフッターコンポーネントで見るように、フォーム内で編集可能な状態を保つこともできます。

   1. を追加します。 **タイトル** コンポーネントをフォームの中央に配置します。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. を追加します。 **テキスト入力** コンポーネントをタイトルコンポーネントの後に追加します。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. を追加します。 **数値入力** コンポーネント。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. を追加します。 **送信ボタン** コンポーネントをフォームに追加します。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. 次をクリック： **タイトル** そのような要素 **ポップアップメニュー** が表示されます。 次をクリック： **編集アイコン** をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. 入力 `Contact Us` をタイトルテキストとして使用します。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. 次をクリック： **テキスト入力** コンポーネントを使用してポップアップメニューを表示します。 次をクリック： **編集アイコン** をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. 入力 **氏名** をフィールドラベルとして使用します。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. 次をクリック： **数値入力** コンポーネントを使用してポップアップメニューを表示します。 次をクリック： **編集アイコン** をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. 次を入力します。 **電話番号** をフィールドラベルとして使用します。
      ![](/help/forms/assets/screenshot2028123829.png)


1. フォームに検証機能を追加：

   1. 次をクリック： **電話番号** コンポーネントを使用してポップアップメニューを表示します。 次をクリック： **レンチアイコン** をクリックして、フィールドを設定します。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. を開きます。 **「検証」タブ**、フィールドに **必須**&#x200B;をクリックし、 **完了**. 成功メッセージが表示されます。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. クリック **プレビュー** をクリックして、エンドユーザーの観点からフォームをプレビューします。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. ダミーデータでフォームに入力
      ![](/help/forms/assets/screenshot2028125629.png)

   1. フォームを送信
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 「 Request bin 」タブで、送信されたデータを確認します。
      ![](/help/forms/assets/screenshot2028125829.png)

ここで、残りの練習では、事前に作成した登録フォームを使用します。

1. AEM Forms管理インターフェイスを開きます。例： `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`をクリックし、登録フォームを選択します。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 「**公開する**」をクリックします。

   ![](/help/forms/assets/screenshot2028115629.png)

   成功メッセージが表示されます。

   ![](/help/forms/assets/screenshot2028115729.png)

   フォームの発行 URL は、次のようになります。 `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. 公開されたフォームを表示するには、上記の URL のプログラム ID(pXXXXXX) と環境 ID(eXXXXXX) を、お使いの環境の ID に置き換えます。

## レッスン 3

### 目的

フロントエンド開発のベストプラクティスを使用してスタイルを更新します。

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者が、以前に作成したアダプティブフォームのスタイル設定を簡単に更新する方法を学習します。

### 演習

テーマのローカルリポジトリを設定します。

1. 管理者権限でコマンドプロンプトまたはシェルを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)

1. コマンドプロンプトで、次のコマンドを使用してに移動します。 **c:\git** フォルダー

   ```Shell
   cd c:\git
   ```

1. 次のコマンドを使用して、テーマのフロントエンドコードを複製します。

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 次のコマンドをリストに表示された順序で使用して、 **aem-forms-theme-canvas** ディレクトリに移動し、Visual Studio Code を開きます。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 選択 **親フォルダー内のすべてのファイルの作成者を信頼する** をクリックし、 **はい、私は著者を信頼しています**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. クラウドサービスのパブリッシュ環境でホストされているフォームをレンダリングするには、 `env_template` ファイル。  ファイル名を変更するには、 **env_template** ファイルを開き、 **名前を変更** オプション。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. .env ファイルの変数に次の値を設定して、ファイルを保存します。

   * **AEM_URL**:クラウドサービスのパブリッシュ環境を指定します。 例：`https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**:フォームのパスを指定します。 例えば、フォームのパスが `/content/forms/af/registration`の場合、この変数の値は次のようになります。 `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. [ コマンドプロンプト ] ウィンドウで、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * を使用して npm を更新するように求めるメッセージが表示された場合、 `npm notice Run npm nstall -g npm@9.6.0`コマンドを使用して、メッセージを無視します。
   > * ワークブックでの指示がない限り、他の npm コマンドを実行しないでください。


1. 次のコマンドを実行して、フォームをプレビューします。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   上記のコマンドを実行したら、 `webpack compiled` メッセージ。 フォームがブラウザータブに表示されます。

   >[!NOTE]
   >
   >を実行した後、ブラウザーで空白の画面が表示される場合、 `npm run live` 3 ～ 4 分以上のコマンド、変更 `localhost` （ブラウザー URL が 127.0.0.1 に達し、を押します） **入力**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. Visual Studio Code で、 `PROJECT\src\site\_variables.scss` ファイル。 注意： `$error` 色は赤の影です。

   ![](/help/forms/assets/screenshot2028120729.png)

1. ブラウザーで、フォームを送信し、 **名** フィールドに入力します。

   ![](/help/forms/assets/screenshot2028120829.png)

1. を **$error** 色付け **#5736eb** ファイルを保存します。

   ![](/help/forms/assets/screenshot2028120729.png)

1. ブラウザーを更新し、フォームを送信します。 名フィールドのエラー色は、それに応じて変更されています。

   ![](/help/forms/assets/screenshot2028121129.png)

1. コマンドプロンプトで、 **Ctrl + C**&#x200B;を入力して、 **Y**&#x200B;を押し、 **入力** npm プロセスを終了するためのキー。 次の一連の演習と競合しないように、npm サーバーを停止することが重要です。
1. Visual Studio の [ コード ] ウィンドウと [ コマンドプロンプト ] ウィンドウを閉じます。

## レッスン 4

### 目的

フォームをヘッドレスフォームとして Web/モバイルおよび他のインターフェイスにレンダリングします。

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者として、React スペクトルデザインフレームワークを使用して、前にヘッドレスフォームとして作成したアダプティブフォームをレンダリングする方法を学びます。

### 演習

React スタータープロジェクトを使用してローカルリポジトリを設定する：

1. 管理者権限を使用してコマンドプロンプトを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)

1. コマンドプロンプトで、次のコマンドを使用してに移動します。 **c:\git** フォルダー

   ```Shell
   cd c:\git
   ```

1. 次のコマンドを使用して、アダプティブフォームの React スタータープロジェクトを複製します。

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 次のコマンドをリストに表示された順序で使用して、 **react-starter-kit-aem-headless-forms** ディレクトリに移動し、Visual Studio Code を開きます。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   「Visual Studio Code」ウィンドウが開きます。

   ![](/help/forms/assets/screenshot2028117429.png)

クラウドサービスのパブリッシュ環境でホストされるフォームをレンダリングするには：

1. env_template ファイルの名前を.env ファイルに変更します。 名前を変更するには、 **env_template** ファイルを開き、 **名前を変更** オプション。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. .env ファイル内の変数に次の値を設定します。 変数を更新したら、ファイルを保存します。

   * **AEM_URL**:クラウドサービスパブリッシュ環境の URL を指定します。 例：`https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**:前のレッスンで作成したアダプティブフォームのパスを指定します。 例：`/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. コマンドウィンドウを開き、 react-starter-kit-aem-headless-forms ディレクトリに移動し、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. [ コマンドプロンプト ] ウィンドウで、次のコマンドを実行します。

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上記のコマンドは、react-spectrum フロントエンドローカル開発を使用して、AEMから取得したフォーム定義をヘッドレス方式でレンダリングするライブラリサーバーを起動します。

   >[!NOTE]
   >
   > 
   > を実行した後、ブラウザーで空白の画面が表示される場合、 `npm start` 3 ～ 4 分以上のコマンド、変更 `localhost` （ブラウザー URL が 127.0.0.1 に達し、を押します） **入力**.

   ![](/help/forms/assets/screenshot2028118229.png)

このヘッドレスフォームでのルールの実行を確認しましょう。

1. を選択します。 **チェックボックスをオンにして 5%オフにします** オプション。 クレジットカードを適用する後続のオプションは無効になります。

   ![](/help/forms/assets/screenshot2028126229.png)

1. オフ **チェックボックスをオンにして 5%オフにします** をクリックして、クレジットカードオプションを有効にします。

   ![](/help/forms/assets/screenshot2028126329.png)

サーバー上のフォームをビジネスユーザーとして変更し、ヘッドレスフォームに自動的に反映された変更を表示します。

1. ブラウザーでAEM Forms管理インターフェイスを開きます。 例： [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. を選択します。 **登録** フォームとクリック **編集。** アダプティブフォームエディターでフォームが開きます。

   ![](/help/forms/assets/screenshot2028118529.png)

1. を選択します。 **電話番号** フィールドに入力し、 **編集アイコン（鉛筆アイコン）** 」と入力します。 ポップアップツールバーが表示されない場合は、 **編集** 右上のボタン、左から **プレビュー** 」ボタンをクリックします。

   ![](/help/forms/assets/screenshot2028119629.png)

1. ラベルを「モバイル番号」に変更します。 フォーム内の空のスペースをクリックすると、フォームに加えた変更が保存されます。

   ![](/help/forms/assets/screenshot2028119729.png)

更新したフォームを発行して、変更を発行環境に反映します。

1. 「 AEM Forms管理インターフェイス」タブで、登録フォームを選択し、 **非公開**. 次の項目が表示されない場合、 **非公開** ボタンをクリックし、手順 3 に進んで変更を直接公開します。

   ![](/help/forms/assets/screenshot2028119829.png)

1. **非公開**&#x200B;をクリックします。クリック **閉じる** を設定します。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. ブラウザーが更新されたら、登録フォームを選択し、 **公開**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. 「**公開する**」をクリックします。クリック **閉じる** を設定します。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. ヘッドレスフォームが表示された状態で、ブラウザータブを更新します。 「電話番号」のラベルが「モバイル番号」に変更されていることに注意してください。

   ![](/help/forms/assets/screenshot2028120529.png)

1. を起動するために使用する [ コマンドプロンプト ] ウィンドウを開きます。 **react-starter-kit-aem-headless-forms** プロジェクト、押す **Ctrl + C**&#x200B;を入力し、 **Y** をクリックし、Enter キーを押して npm プロセスを終了します。 次の一連の演習と競合しないように、npm サーバーを停止することが重要です。

1. Visual Studio の [ コード ] ウィンドウと [ コマンドプロンプト ] ウィンドウを閉じます。


## レッスン 5

### 目的

Google Material UI を使用してフォームをヘッドレスフォームとしてレンダリング

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者がGoogle Material UI を使用して、前の手順でヘッドレスフォームとして作成したアダプティブフォームをレンダリングする方法を学びます。

### 演習

Material UI スタータープロジェクトを使用してローカルリポジトリを設定します。

1. 管理者権限を使用してコマンドプロンプトを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)


1. コマンドプロンプトで、次のコマンドを使用してに移動します。 **c:\git** フォルダー：

   ```Shell
   cd c:\git
   ```

1. 次のコマンドをリストに表示された順序で実行して、mui という名前のフォルダーを作成し、次のコマンドを使用して mui フォルダーに移動します。

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. 次のコマンドを使用して、アダプティブフォームの React スタータープロジェクトを複製します。

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. 次のコマンドをリストに表示された順序で使用して、 **react-starter-kit-aem-headless-forms** フォルダーに移動し、Visual Studio コードでコードを開きます。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

クラウドサービスのパブリッシュ環境でホストされるフォームをレンダリングするには：

1. 名前を変更 **env_template** ～に提出する **.env** ファイル。 名前を変更するには、 **env_template** ファイルと選択 **名前を変更**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. .env ファイル内の変数に次の値を設定します。 変数を更新したら、ファイルを保存します。 以下を使用： **Ctrl + S** 組み合わせを切り替えてファイルを保存します。

   * **AEM_URL**:クラウドサービスパブリッシュ環境の URL を指定します。 例： [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**:前のレッスンで作成したアダプティブフォームのパスを指定します。 例： /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. コマンドウィンドウを開き、 **react-starter-kit-aem-headless-forms** ディレクトリに移動し、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. [ コマンドプロンプト ] ウィンドウで、次のコマンドを実行します。

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   このコマンドは、ローカル開発サーバーを起動し、Google Material UI フロントエンドライブラリを使用して、AEMから取得したフォーム定義をヘッドレスにレンダリングします。

   >[!NOTE]
   >
   >を実行した後、ブラウザーで空白の画面が表示される場合、 `npm start` 3 ～ 4 分以上のコマンド、変更 `localhost` （ブラウザー URL が 127.0.0.1 に達し、を押します） **入力**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. このフォームレンディションでの同じビジネスロジックの実行を評価するには：

   選択 **チェックボックスをオンにして 5%オフにします**. 後続のオプション **We.Finance 社のクレジットカードフォームを申し込みますか？** は無効になります。

   ![](/help/forms/assets/screenshot2028127329.png)

## レッスン 6

### 目的

マテリアル UI コンポーネントのバリエーションを使用して、ヘッドレスフォームの代替ルックアンドフィールを作成する

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者がビジネスユーザーによって以前に作成されたアダプティブフォームの Material UI を使用して、様々なコンポーネントの代替表現を作成する方法を学びます。

### 演習

ヘッドレスプロジェクト内のコンポーネントのバリエーションを更新します。 マテリアル UI のテキスト入力コンポーネントのバリアントをに変更するには `OutlinedInput`:

1. ビジュアルコードで、 `index.tsx` ～にファイルを送る `src/components/textinput/index.tsx`.

1. 追加 `//` コード行 103 の先頭に配置されます。 行がコメントに変換されます。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 104 行目で次のコードを追加して、別のバリアントのコンポーネントを使用し、ファイルを保存します。 以下を使用： **Ctrl + S** 組み合わせを切り替えてファイルを保存します。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   「OutlinedInput」バリアントで正しい大文字を使用する必要があります。大文字を使用しない場合、コンパイルが失敗します。 ローカル開発環境のコンパイルは、コマンドプロンプトで自動的に開始されます。 次のメッセージが表示されるまで待ちます

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. ブラウザを更新し、自動的に更新されない場合は、テキスト入力コンポーネントが別のバリアントを使用していることを確認します。

   ![](/help/forms/assets/screenshot2028127729.png)


   この変更は、AEM Forms Server のフォーム定義に変更を加えずにエンドユーザーに対しておこなわれ、考慮中のヘッドレスチャネルに固有のものです。 例えば、この実習では Web チャネルを使用します。

   ![](/help/forms/assets/screenshot2028127529.png)


1. Visual Studio コードとコマンドプロンプトウィンドウを閉じます。

## よくある質問 (FAQ)

+++ アダプティブフォームウィザードは一般に使用できますか？

はい、AEM FormsでCloud Serviceとして使用できます。

+++


+++ コアコンポーネントは一般公開されていますか？

はい、アダプティブFormsのコアコンポーネントは、AEM FormsでCloud Serviceとして使用できます。

+++

+++ ヘッドレスフォームは公開されていますか？

はい、ヘッドレスフォームは、AEM FormsでCloud Serviceとして使用できます。

+++

+++ ヘッドレスフォームには別のライセンスが必要ですか？

いいえ、ヘッドレスフォームは同じライセンス値指標、フォーム送信数を使用します。

+++

+++ コアコンポーネントとヘッドレスフォームはAEM 6.5 Formsで利用できますか？

はい。アダプティブフォームのコアコンポーネントとヘッドレスフォームは、AEM Forms 6.5 Service Pack 16 以降で使用できます。

+++


## 次の手順

これで、アダプティブフォームの構築方法を学び、ヘッドレスフォームを使用して複数のチャネルにアダプティブフォームを配信する方法を学びました。新しいスキルを活用する必要があります。 優れたデータキャプチャエクスペリエンスを作成し、大規模なエンドユーザーに提供することで、楽しみながら先に進むことができます。

## リソース

* [アダプティブフォームのコアコンポーネントの概要](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [コアコンポーネントを使用してアダプティブフォームを作成する](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [コアコンポーネントベースの AF のスタイル設定を更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [ヘッドレス React スターターキットの使用](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


