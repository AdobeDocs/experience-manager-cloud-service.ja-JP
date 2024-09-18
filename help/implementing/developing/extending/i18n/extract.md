---
title: 翻訳のための文字列の抽出
description: xgettext-maven-plugin を使用して、ソースコードから翻訳する必要のある文字列を抽出します
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 42b177e6d948a3097bf3edf72362054a10fc8bfb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 翻訳のための文字列の抽出{#extracting-strings-for-translating}

xgettext-maven-plugin を使用して、ソースコードから翻訳する必要のある文字列を抽出します。Maven プラグインは、翻訳のために送信する XLIFF ファイルに文字列を抽出します。文字列は次の場所から抽出されます。

* Java ソースファイル
* JavaScript ソースファイル
* XML ファイル形式の SVN リソース（JCR ノード）

## 文字列の抽出の設定 {#configuring-string-extraction}

xgettext-maven-plugin ツールでプロジェクトの文字列を抽出する方法を設定します。

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| セクション | 説明 |
|---|---|
| /filter | 解析するファイルを識別します。 |
| /parsers/vaultxml | コンテナファイルの解析を設定します。外部化された文字列と翻訳のヒントを含む JCR ノードを識別します。さらに、処理を行わない JCR ノードも識別します。 |
| /parsers/javascript | 文字列を外部化する JavaScript 関数を識別します。このセクションを変更する必要はありません。 |
| /parsers/regexp | Java、JSP、ExtJS テンプレートファイルの解析を設定します。このセクションを変更する必要はありません。 |
| /potentials | 国際化する文字列を検出するための式。 |

### 解析するファイルの識別 {#identifying-the-files-to-parse}

i18n.any ファイルの /filter セクションでは、xgettext-maven-plugin ツールで解析するファイルを識別します。解析するファイルと無視するファイルを識別するために、include 規則と exclude 規則をいくつか追加します。すべてのファイルを含めてから、解析する必要のないファイルを除外する必要があります。通常、UI に影響しないファイルの種類や、翻訳しない UI 定義ファイルは除外します。include 規則と exclude 規則には以下の形式を使用します。

```
{ /include "pattern" }
{ /exclude "pattern" }
```

規則の pattern の部分は、含めるファイルまたは除外するファイルの名前を照合するために使用します。pattern のプレフィックスにより、JCR ノード（コンテナでの形式）と照合するか、ファイルシステムと照合するかを指定します。

| プレフィックス | 効果 |
|---|---|
| / | JCR パスを指定します。したがって、このプレフィックスを指定した場合は、jcr_root ディレクトリの下のファイルと照合されます。 |
| &amp;ast; | ファイルシステム上の標準ファイルを指定します。 |
| なし | プレフィックスがない場合または pattern がフォルダーまたはファイル名で始まる場合は、ファイルシステム上の標準ファイルを指定します。 |

pattern 内で使用されている場合、「/」文字はサブディレクトリを指定し、「*」文字はすべてのファイルと照合されます。次の表に、規則の例をいくつか示します。

<table>
 <tbody>
  <tr>
   <th>規則の例</th>
   <th>効果</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>すべてのファイルを含めます。</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>すべての PDF ファイルを除外します。</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>POM ファイルを除外します。</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>/content ノードの下にあるすべてのファイルを除外します。</p> <p>/content/catalogs/geometrixx/templatepages ノードを含めます。</p> <p>/content/catalogs/geometrixx/templatepages のすべての子ノードを含めます。</p> </td>
  </tr>
 </tbody>
</table>

### 文字列の抽出  {#extracting-the-strings}

POM なし：

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

POM あり：POM に以下を追加します。

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

コマンド：

```shell
mvn xgettext:extract
```

### 出力ファイル {#output-files}

* `raw.xliff`：抽出された文字列
* `warn.log`：警告（存在する場合）（`CQ.I18n.getMessage()` API が正しく使用されていない場合）。これらは常に修正が必要で、その後再実行する必要があります。

* `parserwarn.log`：パーサーの警告（ある場合）。js パーサーの問題など。
* `potentials.xliff`：抽出されなかったものの、翻訳が必要な、人間が判読できる文字列である可能性がある「候補」（無視してかまいません。大量の誤検出が生じます）。
* `strings.xliff`：ALF にインポートするために、フラット化された xliff ファイル。
* `backrefs.txt`：これにより、指定された文字列のソースコードの場所を簡単に調べることができます。
