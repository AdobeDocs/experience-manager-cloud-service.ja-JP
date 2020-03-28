---
title: メディアハンドラーとワークフローを使用したアセットの処理
description: 様々なハンドラーの概要と、ワークフローでハンドラーを使用してアセットに対してタスクを実行する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 068195919c4bf73c41b1156eadb47544e4c41e65

---


# メディアハンドラーとワークフローを使用したアセットの処理 {#processing-assets-using-media-handlers-and-workflows}

Adobe Experience Manager (AEM) Assets には、アセットを処理するためのデフォルトのワークフローとメディアハンドラーのセットが付属しています。ワークフローでは、アセットに対して実行する全般的なタスクを定義し、特定のタスクをメディアハンドラーに委任します。例えば、サムネールの生成やメタデータの抽出などです。

ワークフローは、特定のタイプのアセットがサーバーにアップロードされたときに自動的に実行されるように定義できます。処理手順は、一連の AEM Assets メディアハンドラーに基づいて定義されます。AEM には、[組み込みのハンドラー](#default-media-handlers)がいくつか用意されています。さらに、追加のハンドラーを[カスタムで開発](#creating-a-new-media-handler)したり、処理を[コマンドラインツール](#command-line-based-media-handler)に委任して定義したりできます。

メディアハンドラーは、アセットに対して特定の処理を実行する AEM Assets 内のサービスです。例えば、MP3 オーディオファイルを AEM にアップロードすると、ワークフローは MP3 ハンドラーを呼び出し、MP3 ハンドラーはメタデータを抽出してサムネールを生成します。通常、メディアハンドラーはワークフローと組み合わせて使用されます。AEM 内では、よく使用される MIME タイプがサポートされています。アセットに対して特定のタスクを実行するには、ワークフローを拡張または作成するか、メディアハンドラーを拡張または作成するか、メディアハンドラーを無効または有効にします。

>[!NOTE]
>
>See [Assets supported file formats](file-format-support.md) article for a description of all the formats supported by AEM Assets as well as the features supported for each format.

## デフォルトのメディアハンドラー {#default-media-handlers}

AEM Assets 内では以下のメディアハンドラーを使用できます。また、これらのメディアハンドラーはよく使用される MIME タイプを処理できます。

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

<table>
 <tbody>
  <tr>
   <td>ハンドラー名</td>
   <td>サービス名（システムコンソールでの名称）</td>
   <td>サポートされる MIME タイプ</td>
  </tr>
  <tr>
   <td>TextHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.TextHandler</p> </td>
   <td>text/plain</td>
  </tr>
  <tr>
   <td>PdfHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pdf.PdfHandler</p> </td>
   <td><p>application/pdf<br /> application/illustrator</p> </td>
  </tr>
  <tr>
   <td>JpegHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.JpegHandler</p> </td>
   <td>image/jpeg</td>
  </tr>
  <tr>
   <td>Mp3Handler</td>
   <td><p>com.day.cq.dam.handler.standard.mp3.Mp3Handler</p> </td>
   <td><p>audio/mpeg</p> </td>
  </tr>
  <tr>
   <td>ZipHandler</td>
   <td><p>com.day.cq.dam.handler.standard.zip.ZipHandler</p> </td>
   <td><p>application/java-archive</p> <p>application/zip</p> </td>
  </tr>
  <tr>
   <td>PictHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pict.PictHandler</p> </td>
   <td><p>image/pict</p> </td>
  </tr>
  <tr>
   <td>StandardImageHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.StandardImageHandler</p> </td>
   <td><p>image/gif</p> <p>image/png</p> <p>application/photoshop</p> <p>image/jpeg</p> <p>image/tiff</p> <p>image/x-ms-bmp</p> <p>image/bmp</p> </td>
  </tr>
  <tr>
   <td>MSOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler</td>
   <td>application/msword<br /> </td>
  </tr>
  <tr>
   <td>MSPowerPointHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler</td>
   <td>application/vnd.ms-powerpoint<br /> </td>
  </tr>
  <tr>
   <td>OpenOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler</td>
   <td>application/vnd.openxmlformats-officedocument.wordprocessingml.document<br /> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet<br /> application/vnd.openxmlformats-officedocument.presentationml.presentation<br /> <br /> </td>
  </tr>
  <tr>
   <td>EPubHandler</td>
   <td>com.day.cq.dam.handler.standard.epub.EPubHandler</td>
   <td>application/epub+zip</td>
  </tr>
  <tr>
   <td>GenericAssetHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.GenericAssetHandler</p> </td>
   <td>アセットからデータを抽出するためのハンドラーが他に見つからなかった場合のフォールバック</td>
  </tr>
 </tbody>
</table>

すべてのハンドラーは以下のタスクを実行できます。

* アセットから使用できるすべてのメタデータを抽出する
* アセットからサムネール画像を作成する

以下のようにアクティブなメディアハンドラーを表示できます。

1. ブラウザーで、`http://localhost:4502/system/console/components` に移動します。
1. リンク `com.day.cq.dam.core.impl.store.AssetStoreImpl` をクリックします。
1. すべてのアクティブなメディアハンドラーリストが表示されます。

## ワークフローでメディアハンドラーを使用したアセットに対するタスクの実行 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

通常、メディアハンドラーはワークフローと組み合わせて使用されるサービスです。

AEM には、アセットを処理するデフォルトのワークフローがいくつかあります。ワークフローを表示するには、ワークフローコンソールを開き、「**[!UICONTROL モデル]**」タブをクリックします。「AEM Assets」から始まるワークフロータイトルは、アセット固有のタイトルです。

特定の要件に従って、既存のワークフローを拡張し、新しいワークフローを作成してアセットを処理できます。

以下の例は、**[!UICONTROL AEM Assets 同期]**&#x200B;ワークフローを拡張して、PDF ドキュメント以外のすべてのアセットについてサブアセットを生成するための方法を示しています。

### メディアハンドラーの無効化／有効化 {#disabling-enabling-a-media-handler}

メディアハンドラーを無効または有効にするには、Apache Felix Web Management Console を使用します。メディアハンドラーを無効にすると、そのアセットに対してメディアハンドラーのタスクは実行されません。

メディアハンドラーを有効または無効にするための手順

1. ブラウザーで、`https://<host>:<port>/system/console/components` に移動します。
1. メディアハンドラーの名前の横にある「**[!UICONTROL Disable]**」をクリックします。例：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`
1. ページを更新します。メディアハンドラーの横に、無効であることを示すアイコンが表示されます。
1. メディアハンドラーを有効にするには、メディアハンドラーの名前の横にある「**[!UICONTROL Enable]**」をクリックします。

### 新しいメディアハンドラーの作成 {#creating-a-new-media-handler}

新しいメディアタイプをサポートしたり、アセットで特定のタスクを実行したりするには、新しいメディアハンドラーを作成する必要があります。ここでは、その進め方について説明します。

#### 重要なクラスおよびインターフェイス {#important-classes-and-interfaces}

実装を開始するための最適な方法は、最も多くの点について対応し、適切なデフォルト動作を提供している付属の抽象実装から継承することです。それが `com.day.cq.dam.core.AbstractAssetHandler` クラスです。

このクラスには、抽象的なサービス記述子が用意されています。そのため、このクラスから継承し、maven-sling-plugin を使用する場合、inherit フラグを `true` に設定する必要があります。

次のメソッドを実装します。

* `extractMetadata()`：使用可能なすべてのメタデータを抽出します。
* `getThumbnailImage()`：渡されたアセットからサムネール画像を作成します。
* `getMimeTypes()`：アセットの MIME タイプを返します。

以下にテンプレートの例を示します。

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

インターフェイスとクラスには以下が含まれます。

* `com.day.cq.dam.api.handler.AssetHandler` インターフェイス：このインターフェイスは、特定のMIMEタイプのサポートを追加するサービスを記述します。 新しいMIMEタイプを追加するには、このインターフェイスを実装する必要があります。 このインターフェイスには、特定のドキュメントの読み込みと書き出し、サムネールの作成およびメタデータの抽出をおこなうメソッドがあります。
* `com.day.cq.dam.core.AbstractAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。
* `com.day.cq.dam.core.AbstractSubAssetHandler` クラス：
   * その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。さらに、サブアセットの抽出についてよく使用される機能も提供します。
   * 実装を開始するための最適な方法は、最も多くの点について対応し、適切なデフォルト動作を提供している付属の抽象実装から継承することです。それが com.day.cq.dam.core.AbstractAssetHandler クラスです。
   * このクラスには、抽象的なサービス記述子が用意されています。そのため、このクラスから継承し、maven-sling-plugin を使用する場合、inherit フラグを true に設定する必要があります。

以下のメソッドを実装する必要があります。

* `extractMetadata()`：使用できるすべてのメタデータを抽出します。
* `getThumbnailImage()`：渡されたアセットのサムネール画像を作成します。
* `getMimeTypes()`:このメソッドは、アセットのMIMEタイプを返します。

以下にテンプレートの例を示します。

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // 関係する部分を実装 }

インターフェイスとクラスには以下が含まれます。

* `com.day.cq.dam.api.handler.AssetHandler` インターフェイス：このインターフェイスは、特定のMIMEタイプのサポートを追加するサービスを記述します。 新しいMIMEタイプを追加するには、このインターフェイスを実装する必要があります。 このインターフェイスには、特定のドキュメントの読み込みと書き出し、サムネールの作成およびメタデータの抽出をおこなうメソッドがあります。
* `com.day.cq.dam.core.AbstractAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。
* `com.day.cq.dam.core.AbstractSubAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。さらに、サブアセットの抽出についてよく使用される機能も提供します。

<!--
#### Example: create a specific Text Handler {#example-create-a-specific-text-handler}

In this section, you will create a specific Text Handler that generates thumbnails with a watermark.

Proceed as follows:

Refer to [Development Tools](../sites-developing/dev-tools.md) to install and set up Eclipse with a Maven plugin and for setting up the dependencies that are needed for the Maven project.

After you perform the following procedure, when you upload a txt file into AEM, the file's metadata are extracted and two thumbnails with a watermark are generated.

1. In Eclipse, create `myBundle` Maven project:

    1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
    1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
    1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
    1. Define the Maven project:

        * Group Id: com.day.cq5.myhandler
        * Artifact Id: myBundle
        * Name: My AEM bundle
        * Description: This is my AEM bundle

    1. Click **[!UICONTROL Finish]**.

1. Set the Java Compiler to version 1.5:

    1. Right-click the `myBundle` project, select Properties.
    1. Select Java Compiler and set following properties to 1.5:

        * Compiler compliance level
        * Generated .class files compatibility
        * Source compatibility

    1. Click **[!UICONTROL OK]**. In the dialog window, click Yes.

1. Replace the code in the pom.xml file with the following code:

1. Create the package `com.day.cq5.myhandler` that contains the Java classes under `myBundle/src/main/java`:

    1. Under myBundle, right-click `src/main/java`, select New, then Package.
    1. Name it `com.day.cq5.myhandler` and click Finish.

1. Create the Java class `MyHandler`:

    1. In Eclipse, under `myBundle/src/main/java`, right-click the `com.day.cq5.myhandler` package, select New, then Class.
    1. In the dialog window, name the Java Class MyHandler and click Finish. Eclipse creates and opens the file MyHandler.java.
    1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;

   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/

   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }

    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile the Java class and create the bundle:

    1. Right-click the myBundle project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
    1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). The new text handler is now active in AEM.
1. In your browser, open the Apache Felix Web Management Console. Select the Components tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

-->

## コマンドラインベースのメディアハンドラー {#command-line-based-media-handler}

AEM を使用すると、ワークフロー内で任意のコマンドラインツールを実行して、アセットを変換し（ImageMagick など）、新しいレンディションをアセットに追加できます。必要な操作は、AEM サーバーをホストするディスクにコマンドラインツールをインストールし、ワークフローにプロセスのステップを設定することのみです。また、`CommandLineProcess` という起動プロセスによって、特定の MIME タイプに従ってフィルター処理を実行し、新しいレンディションに基づいて複数のサムネールを作成することもできます。

以下の変換を自動的に実行し、AEM Assets 内に保存することができます。

* [ImageMagick](https://www.imagemagick.org/script/index.php) および [Ghostscript](https://www.ghostscript.com/) を使用した EPS および AI 変換
* [FFmpeg](https://ffmpeg.org/) を使用した FLV ビデオのトランスコーディング
* [LAME](http://lame.sourceforge.net/) を使用した MP3 エンコーディング
* [SOX](http://sox.sourceforge.net/) を使用したオーディオ処理

>[!NOTE]
>
>非 Windows システムでは、ファイル名に一重引用符（&#39;）を含むビデオアセットのレンディションの生成中に FFMpeg ツールがエラーを返します。ビデオファイル名に一重引用符が含まれている場合は、AEM にアップロードする前に削除してください。

`CommandLineProcess` プロセスは、リストに表示されている順序で以下の操作を実行します。

* 特定のMIMEタイプに従ってファイルをフィルターします（指定されている場合）。
* AEM サーバーをホストするディスクに一時ディレクトリを作成します。
* 元のファイルを一時ディレクトリにストリーミングします。
* ステップの引数で定義されたコマンドを実行します。AEM を実行しているユーザーの権限を使用して、一時ディレクトリ内でコマンドが実行されます。
* 結果を AEM サーバーのレンディションフォルダーにストリーミングします。
* 一時ディレクトリを削除します。
* 指定した場合は、それらのレンディションに基づいてサムネールを作成します。サムネールの数とサイズは、ステップの引数で定義されます。

### ImageMagick を使用した例 {#an-example-using-imagemagick}

以下の例は、MIME タイプが gif または tiff のアセットが AEM サーバーの /content/dam に追加されるたびに、元の画像の反転画像と 3 つの追加サムネール（140 x 100、48 x 48 および 10 x 250）が作成されるように、コマンドラインプロセスのステップを設定する方法を示します。

これを実現するには、ImageMagick を使用します。ImageMagick は無料のソフトウェアスイートです。ビットマップ画像の作成、編集および構成をおこなう機能があり、一般的にコマンドラインから使用されます。

まず、AEM サーバーをホストするディスクに ImageMagick をインストールします。

1. ImageMagickのインストール：ImageMagickのドキュメ [ントを参照してくださ](https://www.imagemagick.org/script/download.php)い。
1. コマンドラインで convert を実行できるようにツールを設定します。
1. ツールが適切にインストールされているかどうかを確認するには、コマンド `convert -h` をコマンドラインで実行します。

   convert ツールの使用できるすべてのオプションが記載されたヘルプ画面が表示されます。

   >[!NOTE]
   >
   >Windows のバージョン（Windows SE など）によっては、convert コマンドを実行できない場合があります。このコマンドは、Windows インストールの一部であるネイティブな変換ユーティリティと競合するからです。このような場合は、画像ファイルをサムネールに変換するために使用する ImageMagick ユーティリティの完全パスを指定します。例： `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. このツールが正しく実行されていることを確認するには、.jpg 画像を作業ディレクトリに追加して、コマンド convert `<image-name>.jpg -flip <image-name>-flipped.jpg` をコマンドラインで実行します。

   反転画像がディレクトリに追加されます。

コマンドラインプロセスのステップを **[!UICONTROL DAM アセット更新]**&#x200B;ワークフローに追加します。

1. **[!UICONTROL ワークフロー]**&#x200B;コンソールを開きます。
1. 「**[!UICONTROL モデル]**」タブで、**[!UICONTROL DAM アセット更新]**&#x200B;モデルを編集します。
1. 以下のように、**[!UICONTROL Web enabled rendition]** ステップの設定を変更します。

   **引数**：

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. ワークフローを保存します。

変更したワークフローをテストするには、`/content/dam` にアセットを追加します。

1. ファイルシステムで、任意の .tiff 画像を選択します。名前を `myImage.tiff` に変更し、WebDAV などを使用して、`/content/dam` にコピーします。
1. **[!UICONTROL CQ5 DAM]** コンソール（例：`http://localhost:4502/libs/wcm/core/content/damadmin.html`）を開きます。
1. アセット **[!UICONTROL myImage.tiff]** を開き、反転画像と 3 つのサムネールが作成されたことを確認します。

#### CommandLineProcess プロセスステップの設定 {#configuring-the-commandlineprocess-process-step}

ここでは、**CommandLineProcess** の&#x200B;**プロセス引数**&#x200B;を設定する方法について説明します。

**プロセス引数**&#x200B;の値が複数ある場合はコンマで区切ります。また、値の先頭を空白にすることはできません。

<table>
 <tbody>
  <tr>
   <td> 引数のフォーマット</td>
   <td>説明</td>
  </tr>
  <tr>
   <td> mime:&lt;mime-type&gt;</td>
   <td><p>オプション引数。アセットのMIMEタイプが引数の1つと同じ場合、プロセスが適用されます。</p> <p>複数の MIME タイプを定義できます。</p> </td>
  </tr>
  <tr>
   <td> tn:&lt;width&gt;:&lt;height&gt;</td>
   <td><p>オプション引数。プロセスにより、引数に定義されたサイズのサムネールが作成されます。</p> <p>複数のサムネールを定義できます。<br /> </p> </td>
  </tr>
  <tr>
   <td> cmd: &lt;command&gt;</td>
   <td><p>実行されるコマンドを定義します。この構文はコマンドラインツールによって異なります。</p> <p>1 つのコマンドのみを定義できます。</p> <p>以下の変数を使用してコマンドを作成できます。<br/></p> <p><code>${filename}</code>: name of the input file, for example `original.jpg`<br/><code>${file}</code>: full path name of the input file, for example, `/tmp/cqdam0816.tmp/original.jpg`<br/><code>${directory}</code>: directory of the input file, for example `/tmp/cqdam0816.tmp`.<br/> <code>${basename}</code>:拡張子を含まない入力ファイルの名前(オリジナル<br/><code>${extension}</code>:入力ファイルの拡張子（JPGなど）<br/></p></td>
  </tr>
 </tbody>
</table>

例えば、AEM サーバーをホストするディスクに ImageMagick がインストールされており、**CommandLineProcess** を実装として使用し、以下の値を&#x200B;**プロセス引数**&#x200B;として使用してプロセスのステップを作成するとします。

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

この場合、ワークフローを実行すると、MIME タイプが image/gif または mime:image/tiff のアセットにのみ、このステップが適用され、元の画像の反転画像が作成され、.jpg に変換され、140 x 100、48 x 48 および 10 x 250 というサイズの 3 つのサムネールが作成されます。

ImageMagick を使用して 3 つの標準のサムネールを作成するには、以下の&#x200B;**プロセス引数**&#x200B;を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

ImageMagick を使用して Web 対応レンディションを作成するには、以下の&#x200B;**プロセス引数**&#x200B;を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>**CommandLineProcess** ステップは、アセット（ノードタイプ ）またはアセットの子孫にのみ適用されます。`dam:Asset`
