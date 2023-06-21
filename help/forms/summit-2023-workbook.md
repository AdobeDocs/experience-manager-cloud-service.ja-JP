---
title: コアコンポーネントとヘッドレスを使用して魅力的なフォームを構築
seo-title: Build Engaging Forms Using Core Components and Headless
description: コアコンポーネントとヘッドレスを使用して魅力的なフォームを構築
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
exl-id: e1eb0812-c92e-4a18-aabb-5a70b9e6fc7d
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '3359'
ht-degree: 99%

---

# コアコンポーネントとヘッドレスを使用して魅力的なフォームを構築

## ラボの概要

この実践ラボでは、次のことを学習します。

AEM Forms を使用して、AEM Sites と一貫性のある最新のコアコンポーネントを使って簡単にアダプティブフォームを作成し、アダプティブフォームをヘッドレスフォームとして web、モバイル、チャットに配信することで、オムニチャネルのデータ取得機能を有効にする方法。また、スタイル設定、カスタマイズ、フロントエンド開発に関するベストプラクティスについても学習します。

## 重要ポイント

* **ビジネスの俊敏性**：ビジネスユーザーは、複数のチャネル用のフォームエクスペリエンスを簡単に作成できます。

* **フロントエンド開発者に力を与える**：フロントエンド開発者は、ヘッドレスフォームを使用してエンドユーザーエクスペリエンスを制御できます。

* **開発者の速度**：開発者は、Sites コンポーネントと Forms コンポーネントを簡単かつ一貫してカスタマイズできます。

## 前提条件


+++AEM Forms as Cloud Service サンドボックス



<table>
        <thead>
            <tr><th>ラボ ID</th><th>オーサーインスタンス URL</th><th>パブリッシュインスタンス URL</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## レッスン 1

### 目的

AEM Forms as a Cloud Service 環境に慣れる。

### レッスンのコンテキスト

このレッスンでは、ユーザーインターフェイスをナビゲートして、AEM Forms as a Cloud Service の環境に慣れ親しみます。

### 演習

1. ブラウザーを開き、Cloud Service オーサー環境の URL を入力します。

1. Cloud Service オーサー環境にログインします。ラボでは、オーサー環境のログイン資格情報が共有されます。

1. ログインした後、AEM Forms UI に移動します。**Forms** をクリックします。

   ![](/help/forms/assets/screenshot2028113829.png)

1. **フォームとドキュメント**&#x200B;をクリックします。環境設定や情報に関連するポップアップを解除します。

   ![](/help/forms/assets/screenshot2028113929.png)

   使用可能なすべてのフォームが表示されます。

   ![](/help/forms/assets/screenshot2028114029.png)

## レッスン 2

### 目的

最新のコアコンポーネントを使用してアダプティブフォームを作成し、フォームを設定して送信します。

### レッスンのコンテキスト

このレッスンでは、ビジネスユーザーとして、データ取得用の標準化された OOTB コアコンポーネントを使用して作成されたアダプティブフォームを使用して、web、モバイル、チャットなど複数のチャネル用のアダプティブフォームを作成します。

### 演習

1. フォームの送信エンドポイントを作成します。

   1. 新しいブラウザータブで、<https://requestbin.com/> を開きます。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. **公開 bin を作成**をクリックし、エンドポイント URL をコピーします。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. ウィザードインターフェイスを使用してアダプティブフォームを作成します。

   1. レッスン 1 で使用したブラウザータブで、AEM Forms as a Cloud Service web インターフェイスに移動し、フォーム＆ドキュメントに移動します。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. 「**作成**」をタップして、「アダプティブフォーム」を選択します。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. 選択画面から、**コアコンポーネントを使用した空白**テンプレートを選択します（下図を参照）。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 「**スタイル**」タブをクリックし、「**wknd-theme**」テーマを選択します（下図を参照）。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 「**送信**」タブをクリックし、「**REST エンドポイントに送信**」カードを選択し、
      「**POST リクエストの URL**」フィールドで公開 bin を指定します（下図を参照）。
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 「**作成**」をクリックします。フォームの名前とタイトルを指定します。例：**contactus**。「**作成**」をクリックします。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. アダプティブフォームエディターが開きます。ポップアップまたはダイアログを閉じて、環境設定や情報を表示します。左側のパネルでコンポーネントブラウザーをクリックし、**フッター**コンポーネントを空白のフォームの下部に配置します。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. ヘッダーは、アダプティブフォームテンプレートの一部です。これにより、すべてのアダプティブフォームで一貫したヘッダー／フッターを簡単に提供できます。または、次の手順のフッターコンポーネントで見られるように、フォーム内で編集可能な状態を維持することもできます。

   1. **タイトル**コンポーネントをフォームの中央に追加します。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. **テキスト入力**コンポーネントをタイトルコンポーネントの後に追加します。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. **数値入力**コンポーネントを追加します。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. **送信ボタン**コンポーネントをフォームに追加します。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. **タイトル**&#x200B;コンポーネントをクリックして、**ポップアップメニュー**&#x200B;を表示します。メニューの&#x200B;**編集アイコン**をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. タイトルテキストとして `Contact Us` と入力します。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. **テキスト入力**&#x200B;コンポーネントをクリックして、ポップアップメニューを表示します。メニューの&#x200B;**編集アイコン**をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. フィールドラベルとして、**氏名**と入力します。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. **数値入力**&#x200B;コンポーネントをクリックして、ポップアップメニューを表示します。**編集アイコン**をクリックし、ラベルを編集します。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. フィールドラベルとして、「**電話番号**」と入力します。
      ![](/help/forms/assets/screenshot2028123829.png)


1. フォームに検証機能を追加します。

   1. **電話番号**&#x200B;コンポーネントをクリックして、ポップアップメニューを表示します。**レンチアイコン**をクリックして、フィールドを設定します。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. **「検証」タブ**&#x200B;を開き、フィールドに&#x200B;**必須**&#x200B;とマークを付け、「**完了**」をクリックします。成功メッセージが表示されます。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. 「**プレビュー**」をクリックして、エンドユーザーの観点からフォームをプレビューします。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. ダミーデータでフォームに入力
      ![](/help/forms/assets/screenshot2028125629.png)

   1. フォームを送信
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 「リクエスト bin」タブで、送信されたデータを確認します。
      ![](/help/forms/assets/screenshot2028125829.png)

残りの演習では、事前に作成した登録フォームを使用します。

1. AEM Forms 管理インターフェイス（例：`https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`）を開き、登録フォームを選択します。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 「**公開する**」をクリックします。

   ![](/help/forms/assets/screenshot2028115629.png)

   成功メッセージが表示されます。

   ![](/help/forms/assets/screenshot2028115729.png)

   フォームの公開 URL は、次のようになります。`https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`

1. 公開されたフォームを表示するには、上記の URL のプログラム ID（pXXXXXX）と環境 ID（eXXXXXX）を、お使いの環境の ID に置き換えます。


## レッスン 3

### 目的

フロントエンド開発のベストプラクティスを使用して、スタイルを更新します。

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者が、以前に作成したアダプティブフォームのスタイル設定を簡単に更新する方法を学習します。

### 演習

テーマのローカルリポジトリを設定します。

1. 管理者権限でコマンドプロンプトまたはシェルを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)

1. コマンドプロンプトで、次のコマンドを使用して **c:\git** フォルダーに移動します。

   ```Shell
   cd c:\git
   ```

1. 次のコマンドを使用して、テーマのフロントエンドコードを複製します。

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 次のコマンドをリストに表示された順序で使用して、**aem-forms-theme-canvas** ディレクトリに移動し、Visual Studio Code を開きます。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 「**親フォルダー内のすべてのファイルの作成者を信頼する**」を選択し、「**はい、私は作成者を信頼します**」をクリックします。

   ![](/help/forms/assets/screenshot2028116229.png)

1. クラウドサービスのパブリッシュ環境でホストされているフォームをレンダリングするには、`env_template` ファイルの名前を変更します。ファイル名を変更するには、**env_template** ファイルを右クリックして、「**名前を変更**」オプションを選択します。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. .env ファイルの変数に次の値を設定して、ファイルを保存します。

   * **AEM_URL**：クラウドサービスのパブリッシュ環境を指定します。例：`https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**：フォームのパスを指定します。例えば、フォームのパスが `/content/forms/af/registration` の場合、この変数の値は `registration` になります。

   ![](/help/forms/assets/screenshot2028116429.png)


1. コマンドプロンプトウィンドウで、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * `npm notice Run npm nstall -g npm@9.6.0` コマンドを使用して npm をアップデートするように求めるメッセージが表示された場合、メッセージを無視します。
   > * ワークブックでの指示がない限り、他の npm コマンドを実行しないでください。

1. 次のコマンドを実行して、フォームをプレビューします。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   上記のコマンドを実行したら、`webpack compiled` メッセージが表示されるまで待機します。フォームがブラウザータブに表示されます。

   >[!NOTE]
   >
   >`npm run live` コマンドを実行した後、ブラウザーで 3～4 分以上空白の画面が表示される場合は、ブラウザーの URL の `localhost` を 127.0.0.1 に変更して **Enter** キーを押します。


   ![](/help/forms/assets/screenshot2028115129.png)


1. Visual Studio Code で、`PROJECT\src\site\_variables.scss` ファイルを開きます。`$error` のカラーは赤の網掛けです。

   ![](/help/forms/assets/screenshot2028120729.png)

1. ブラウザーでフォームを送信して、「**名前（名）**」フィールドが赤くなるのを確認します。

   ![](/help/forms/assets/screenshot2028120829.png)

1. **$error** の色を **#5736eb** に設定して、ファイルを保存します。

   ![](/help/forms/assets/screenshot2028120729.png)

1. ブラウザーを更新し、フォームを送信します。名フィールドのエラーカラーが、それに応じて変更されました。

   ![](/help/forms/assets/screenshot2028121129.png)

1. コマンドプロンプトで、**Ctrl + C** キーを押して、**Y** キーを押し、**Enter** キー を押して npm プロセスを終了します。次の一連の演習と競合しないように、npm サーバーを停止することが重要です。
1. Visual Studio Code とコマンドプロンプトウィンドウを閉じます。

## レッスン 4

### 目的

フォームをヘッドレスフォームとして web／モバイルおよび他のインターフェイスにレンダリングします。

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者として、React スペクトルデザインフレームワークを使用して、前にヘッドレスフォームとして作成したアダプティブフォームをレンダリングする方法を学びます。

### 演習

React スタータープロジェクトを使用してローカルリポジトリを設定します。

1. 管理者権限を使用してコマンドプロンプトを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)

1. コマンドプロンプトで、次のコマンドを使用して **c:\git** フォルダーに移動します。

   ```Shell
   cd c:\git
   ```

1. 次のコマンドを使用して、アダプティブフォームの React スタータープロジェクトを複製します。

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 次のコマンドをリストに表示された順序で使用して、**react-starter-kit-aem-headless-forms** ディレクトリに移動し、Visual Studio Code を開きます。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Visual Studio Code ウィンドウが開きます。

   ![](/help/forms/assets/screenshot2028117429.png)

クラウドサービスのパブリッシュ環境でホストされるフォームをレンダリングするには、次の手順に従います。

1. env_template ファイルを.env ファイルに名前変更します。名前を変更するには、**env_template** ファイルを右クリックし、「**名前を変更**」オプションを選択します。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. .env ファイル内の変数に次の値を設定します。変数を更新したら、ファイルを保存します。

   * **AEM_URL**：クラウドサービスパブリッシュ環境の URL を指定します。例：`https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**：前のレッスンで作成したアダプティブフォームのパスを指定します。例：`/content/forms/af/registration/`

     ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. コマンドウィンドウを開き、react-starter-kit-aem-headless-forms ディレクトリにいることを確認し、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. コマンドプロンプトウィンドウで、次のコマンドを実行します。

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上記のコマンドは、ローカル開発サーバーを起動し、AEM から取得したフォーム定義を react-spectrum フロントエンドライブラリを使ってヘッドレスでレンダリングするものです。

   >[!NOTE]
   >
   > 
   > `npm start` コマンドを実行した後、ブラウザーで 3～4 分以上空白の画面が表示される場合は、ブラウザーの URL の `localhost` を 127.0.0.1 に変更して **Enter** キーを押します。

   ![](/help/forms/assets/screenshot2028118229.png)

このヘッドレスフォームのルールの実行を確認しましょう。

1. 「**チェックボックスをオンにして 5％オフを受け取る**」オプションを選択します。クレジットカードを適用する後続のオプションは無効になります。

   ![](/help/forms/assets/screenshot2028126229.png)

1. 「**チェックボックスをオンにして 5％オフを受け取る**」のチェックを解除して、クレジットカードオプションを有効にします。

   ![](/help/forms/assets/screenshot2028126329.png)

サーバー上のフォームをビジネスユーザーとして変更し、ヘッドレスフォームに自動的に反映された変更を表示します。

1. ブラウザーで AEM Forms 管理インターフェイスを開きます。\
1. **登録**&#x200B;フォームを選択し、「**編集**」をクリックします。アダプティブフォームエディターでフォームが開きます。

   ![](/help/forms/assets/screenshot2028118529.png)

1. 「**電話番号**」フィールドを選択し、ツールバーの&#x200B;**編集アイコン（鉛筆アイコン）**&#x200B;をクリックします。ポップアップツールバーが表示されない場合は、右上の、「**プレビュー**」ボタンの左側にある「**編集**」ボタンをクリックして、編集モードに切り替えます。

   ![](/help/forms/assets/screenshot2028119629.png)

1. ラベルを「携帯電話番号」に変更します。フォーム内の空のスペースをクリックすると、フォームに加えた変更が保存されます。

   ![](/help/forms/assets/screenshot2028119729.png)

更新したフォームを公開して、変更をパブリッシュ環境に反映します。

1. 「AEM Forms 管理インターフェイス」タブで、登録フォームを選択し、「**非公開**」をクリックします。「**非公開**」ボタンが表示されない場合、手順 3 に進んで変更を直接公開します。

   ![](/help/forms/assets/screenshot2028119829.png)

1. 「**非公開**」をクリックします。次のダイアログで「**閉じる**」をクリックします。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. ブラウザーが更新されたら、登録フォームを選択し、「**公開**」をクリックします。

   ![](/help/forms/assets/screenshot2028120129.png)


1. 「**公開する**」をクリックします。次のダイアログで「**閉じる**」をクリックします。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. ヘッドレスフォームが表示された状態で、ブラウザータブを更新します。「電話番号」のラベルが「携帯電話番号」に変更されていることに注意してください。

   ![](/help/forms/assets/screenshot2028120529.png)

1. **react-starter-kit-aem-headless-forms** プロジェクトの起動に使用するコマンドプロンプトウィンドウを開き、**CTRL + C** キーを押し、
「**Y**」を入力して、Enter キーを押して npm プロセスを終了します。次の一連の演習と競合しないように、npm サーバーを停止することが重要です。

1. Visual Studio Code とコマンドプロンプトウィンドウを閉じます。


## レッスン 5

### 目的

Google Material UI を使用してフォームをヘッドレスフォームとしてレンダリングする

### レッスンのコンテキスト

このレッスンでは、フロントエンド開発者が Google Material UI を使用して、前の手順でヘッドレスフォームとして作成したアダプティブフォームをレンダリングする方法を学びます。

### 演習

Material UI スタータープロジェクトを使用してローカルリポジトリを設定します。

1. 管理者権限を使用してコマンドプロンプトを開きます。

   ![](/help/forms/assets/screenshot2028115829.png)


1. コマンドプロンプトで、次のコマンドを使用して **c:\git** フォルダーに移動します。

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

1. 次のコマンドをリストに表示された順序で使用して、**react-starter-kit-aem-headless-forms** フォルダーに移動し、Visual Studio Code でコードを開きます。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

クラウドサービスのパブリッシュ環境でホストされるフォームをレンダリングするには、次の手順に従います。

1. **env_template** ファイルを **.env** ファイルに名前変更します。名前を変更するには、**env_template** ファイルを右クリックし、「**名前を変更**」を選択します。

   ![](/help/forms/assets/screenshot2028126629.png)

1. .env ファイル内の変数に次の値を設定します。変数を更新したら、ファイルを保存します。**Ctrl + S** キーを使用してファイルを保存します。

   * **AEM_URL**：クラウドサービスパブリッシュ環境の URL を指定します。

   * **AEM_FORM_PATH**：前のレッスンで作成したアダプティブフォームのパスを指定します。例：/content/forms/af/registration/

     ![](/help/forms/assets/screenshot2028126929.png)

1. コマンドウィンドウを開き、**react-starter-kit-aem-headless-forms** ディレクトリにいることを確認し、次のコマンドを実行します。

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. コマンドプロンプトウィンドウで、次のコマンドを実行します。

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   このコマンドは、ローカル開発サーバーを起動し、Google Material UI フロントエンドライブラリを使用して、AEM から取得したフォーム定義をヘッドレスにレンダリングします。


   >[!NOTE]
   >
   >`npm start` コマンドを実行した後、ブラウザーで 3～4 分以上空白の画面が表示される場合は、ブラウザーの URL の `localhost` を 127.0.0.1 に変更して **Enter** キーを押します。

   ![](/help/forms/assets/screenshot2028127229.png)

1. このフォームレンディションで同じビジネスロジックの実行を評価するには：

   「**チェックボックスをオンにして 5%オフを受け取る**」を選択します。後続のオプション「**We.Finance のコーポレートクレジットカードフォームを申し込みますか？**」が無効になります。

   ![](/help/forms/assets/screenshot2028127329.png)

## レッスン 6

### 目的

Material UI コンポーネントのバリエーションを使用して、ヘッドレスフォームの代替ルックアンドフィールを作成する

### レッスンのコンテキスト

このレッスンでは、ビジネスユーザーが以前に作成したアダプティブフォームに対して、フロントエンド開発者が Material UI を使用して、様々なコンポーネントの代替表現を作成する方法を学びます。

### 演習

ヘッドレスプロジェクト内のコンポーネントのバリエーションを更新します。Mterial UI のテキスト入力コンポーネントのバリアントを `OutlinedInput` に変更する手順は次のとおりです。

1. Visual Code で、`src/components/textinput/index.tsx` にある `index.tsx` ファイルを開いて、テキスト入力コンポーネントに移動します。

1. コード 103 行目の先頭に `//` を追加します。行がコメントに変換されます。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 別のバリアントのコンポーネントを使用するために、104 行目に次のコードを追加して、ファイルを保存します。**Ctrl + S** キーを使用してファイルを保存します。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   「OutlinedInput」バリアントは正しく大文字と小文字を使用する必要があります。さもないと、コンパイルが失敗します。ローカル開発環境のコンパイルは、コマンドプロンプトで自動的に開始されます。次のメッセージが表示されるまで待ちます

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. 自動的に更新されない場合は、ブラウザーを更新し、テキスト入力コンポーネントが別のバリアントを使用していることを確認します。

   ![](/help/forms/assets/screenshot2028127729.png)


   この変更は、エンドユーザーに対して AEM Forms Server のフォーム定義に変更を加えずに行われ、検討中のヘッドレスチャネルに固有のものです。
例えば、このラボの web チャネルです。

   ![](/help/forms/assets/screenshot2028127529.png)


1. Visual Studio Code とコマンドプロンプトウィンドウを閉じます。

## よくある質問（FAQ）

+++ アダプティブフォームウィザードは一般に使用できますか？

はい、AEM Forms as a Cloud Service で使用できます。

+++


+++ コアコンポーネントは一般公開されていますか？

はい、アダプティブフォームのコアコンポーネントは、AEM Forms as a Cloud Service で使用できます。

+++

+++ ヘッドレスフォームは公開されていますか？

はい、ヘッドレスフォームは、AEM Forms as a Cloud Service で使用できます。

+++

+++ ヘッドレスフォームには別のライセンスが必要ですか？

いいえ、ヘッドレスフォームは同じライセンス値指標、フォーム送信数を使用します。

+++

+++ コアコンポーネントとヘッドレスフォームは AEM 6.5 Forms で利用できますか？

はい。アダプティブフォームのコアコンポーネントとヘッドレスフォームは、AEM Forms 6.5 サービスパック 16 以降で使用できます。

+++


## 次の手順

アダプティブフォームの構築方法と、ヘッドレスフォームを使用して複数のチャネルにアダプティブフォームを配信する方法の説明は以上です。新しいスキルを活用してみましょう。優れたデータキャプチャエクスペリエンスを作成し、大規模なエンドユーザーに提供することで、楽しみながら先に進むことができます。

## リソース

* [アダプティブフォームのコアコンポーネントの概要](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)

* [コアコンポーネントを使用してアダプティブフォームを作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=ja)

* [コアコンポーネントベースの AF のスタイル設定を更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=ja)

* [ヘッドレスアダプティブフォーム](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=ja)

* [ヘッドレス React スターターキットの使用](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=ja)
