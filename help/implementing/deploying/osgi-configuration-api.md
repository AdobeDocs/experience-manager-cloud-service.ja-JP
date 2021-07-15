---
title: OSGi設定API
description: AEM as aCloud ServiceOSGi設定サーフェスの説明
feature: デプロイ
source-git-commit: fb62b0dff49ccaeb4e38ac67dd910519380b7794
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 5%

---


# OSGi設定API

次の2つのリストは、AEM as aCloud ServiceのOSGi設定面を反映し、お客様が設定できる内容を示しています。

1. 顧客コードで設定する必要のないOSGi設定のリスト
1. プロパティを設定できるが、示されている検証ルールに従う必要があるOSGi設定のリスト。 これらのルールには、プロパティの宣言が必須かどうか、プロパティのタイプ、場合によっては値の範囲が許可されます。

OSGi設定がリストに表示されない場合は、顧客コードで設定できます。

これらのルールは、Cloud Managerのビルドプロセス中に検証されます。 時間の経過と共に追加のルールを追加でき、期待される実施日が表に示されます。 お客様は、ターゲットの実施日までにこれらのルールを遵守する必要があります。 削除日の後にルールに従わないと、Cloud Managerのビルドプロセスでエラーが発生します。 ローカルSDKの開発中にOSGI設定エラーにフラグを付けるには、Mavenプロジェクトに[AEM as a Maven SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)を含める必要があります。

OSGI設定に関する追加情報は、[この場所](/help/implementing/deploying/configuring-osgi.md)にあります。

## 変更できないOSGi設定 {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (発表日：4/30/2021、施行日：7/31/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (発表日：4/30/2021、施行日：7/31/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (発表日：4/30/2021、施行日：7/31/2021)
* **`org.apache.felix.http (Factory)`** (発表日：4/30/2021、施行日：7/31/2021)

## ビルド検証ルールの対象となるOSGi設定 {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (発表日：4/30/2021、施行日：7/31/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * 型：整数
      * 必要な範囲：2 ～ 100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * 型：重複
   * `org.apache.felix.eventadmin.Timeout`
      * 型：整数
   * `org.apache.felix.eventadmin.RequireTopic`
      * 型：boolean
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * 必須
      * 型：文字列の配列
      * 必要な範囲：`org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*`の少なくともすべてを含める必要があります。
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * 型：文字列の配列
* **`org.apache.felix.http`** (発表日：4/30/2021、施行日：7/31/2021)
   * `org.apache.felix.http.timeout`
      * 型：整数
   * `org.apache.felix.http.session.timeout`
      * 型：整数
   * `org.apache.felix.http.jetty.threadpool.max`
      * 型：整数
   * `org.apache.felix.http.jetty.headerBufferSize`
      * 型：整数
   * `org.apache.felix.http.jetty.requestBufferSize`
      * 型：整数
   * `org.apache.felix.http.jetty.responseBufferSize`
      * 型：整数
   * `org.apache.felix.http.jetty.maxFormSize`
      * 型：整数
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * 型：boolean
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 型：boolean
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Type：string
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 型：boolean
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Type：string
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Type：string
   * `org.eclipse.jetty.servlet.SessionPath`
      * Type：string
   * `org.eclipse.jetty.servlet.MaxAge`
      * 型：整数
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * 型：整数
   * `org.apache.felix.jetty.gziphandler.enable`
      * 型：boolean
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 型：整数
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 型：整数
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 型：整数
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 型：boolean
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Type：string
   * `org.apache.felix.jetty.gzip.includedMethods`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.includedPaths`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * 型：文字列の配列
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * 型：文字列の配列
   * `org.apache.felix.http.session.invalidate`
      * 型：boolean
   * `org.apache.felix.http.session.container.attribute`
      * 型：文字列の配列
   * `org.apache.felix.http.session.uniqueid`
      * 型：boolean
* **`org.apache.sling.scripting.cache`** (発表日：4/30/2021、施行日：7/31/2021)
   * `org.apache.sling.scripting.cache.size`
      * 型：整数
      * 必要な範囲：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必須
      * 型：文字列の配列
      * 必要な範囲：jsを含める必要がある
* **`com.day.cq.mailer.DefaultMailService`** (発表日：4/30/2021、施行日：7/31/2021)
   * `smtp.host`
      * Type：string
   * `smtp.port`
      * 型：整数
      * 必要な範囲：465、587または25
   * `smtp.user`
      * Type：string
   * `smtp.password`
      * Type：string
   * `from.address`
      * Type：string
   * `smtp.ssl`
      * Type：string
   * `smtp.starttls`
      * 型：boolean
   * `smtp.requiretls`
      * 型：boolean
   * `debug.email`
      * 型：boolean
   * `oauth.flow`
      * 型：boolean
