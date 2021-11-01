---
title: OSGi 設定 API
description: AEM as a Cloud Service OSGi 設定サーフェスの説明
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 100%

---

# OSGi 設定 API

次の 2 つのリストは、AEM as a Cloud Service の OSGi 設定サーフェスを反映しており、顧客が設定できる内容を示しています。

1. 顧客コードで設定してはいけない OSGi 設定のリスト
1. プロパティを設定できるが、示されている検証ルールに従う必要がある OSGi 設定のリスト。これらのルールには、プロパティの宣言が必須かどうか、プロパティの型、場合によっては許容される値の範囲が許可されます。

OSGi 設定がリストに表示されない場合は、顧客コードで設定できます。

これらのルールは、Cloud Manager のビルドプロセス中に検証されます。今後、ルールが追加される可能性があり、その実施予定日が表に記載されています。顧客は、目標の実施日までにこれらのルールを遵守する必要があります。削除日の後にルールに従わないと、Cloud Manager のビルドプロセスでエラーが発生します。ローカル SDK の開発中に OSGI 設定エラーにフラグを付けるには、Maven プロジェクトに [AEM as a Maven SDK Build Analyzer Maven プラグイン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja) を含める必要があります。

OSGI 設定に関する追加情報は、[この場所](/help/implementing/deploying/configuring-osgi.md)にあります。

## 変更できない OSGi 設定 {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`**（発表日：4/30/2021、施行日：7/31/2021）
* **`com.day.cq.auth.impl.cug.CugSupportImpl`**（発表日：4/30/2021、施行日：7/31/2021）
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`**（発表日：4/30/2021、施行日：7/31/2021）
* **`org.apache.felix.http (Factory)`**（発表日：4/30/2021、施行日：7/31/2021）
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`**（発表日：8/25/2021、施行日：11/26/2021）

## ビルド検証ルールの対象となる OSGi 設定 {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`**（発表日：4/30/2021、施行日：7/31/2021）
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * 型：integer
      * 要求範囲：2 ～ 100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * 型：double
   * `org.apache.felix.eventadmin.Timeout`
      * 型：integer
   * `org.apache.felix.eventadmin.RequireTopic`
      * 型：boolean
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * 必須
      * 型：文字列の配列
      * 要求範囲：少なくとも `org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*` をすべてを含める必要があります。
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * 型：文字列の配列
* **`org.apache.felix.http`**（発表日：4/30/2021、施行日：7/31/2021）
   * `org.apache.felix.http.timeout`
      * 型：integer
   * `org.apache.felix.http.session.timeout`
      * 型：integer
   * `org.apache.felix.http.jetty.threadpool.max`
      * 型：integer
   * `org.apache.felix.http.jetty.headerBufferSize`
      * 型：integer
   * `org.apache.felix.http.jetty.requestBufferSize`
      * 型：integer
   * `org.apache.felix.http.jetty.responseBufferSize`
      * 型：integer
   * `org.apache.felix.http.jetty.maxFormSize`
      * 型：integer
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * 型：boolean
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 型：boolean
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 型：string
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 型：boolean
   * `org.eclipse.jetty.servlet.SessionCookie`
      * 型：string
   * `org.eclipse.jetty.servlet.SessionDomain`
      * 型：string
   * `org.eclipse.jetty.servlet.SessionPath`
      * 型：string
   * `org.eclipse.jetty.servlet.MaxAge`
      * 型：integer
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * 型：integer
   * `org.apache.felix.jetty.gziphandler.enable`
      * 型：boolean
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 型：integer
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 型：integer
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 型：integer
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 型：boolean
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * 型：string
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
* **`org.apache.sling.scripting.cache`**（発表日：4/30/2021、施行日：7/31/2021）
   * `org.apache.sling.scripting.cache.size`
      * 型：integer
      * 要求範囲：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必須
      * 型：文字列の配列
      * 要求範囲：js を含める必要があります
* **`com.day.cq.mailer.DefaultMailService`**（発表日：4/30/2021、施行日：7/31/2021）
   * `smtp.host`
      * 型：string
   * `smtp.port`
      * 型：integer
      * 要求範囲：465、587、25 のいずれか
   * `smtp.user`
      * 型：string
   * `smtp.password`
      * 型：string
   * `from.address`
      * 型：string
   * `smtp.ssl`
      * 型：string
   * `smtp.starttls`
      * 型：boolean
   * `smtp.requiretls`
      * 型：boolean
   * `debug.email`
      * 型：boolean
   * `oauth.flow`
      * 型：boolean
