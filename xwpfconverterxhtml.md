# XWPFConverterXHTML

## XWPFDocument 2 XHTML

org.apache.poi.xwpf.converter.xhtml包提供了基于 Apache POI XWPF 的 DOCX 2 XHTML 转换器。

## 下载

maven：

```text
<dependency>
  <groupId>fr.opensagres.xdocreport</groupId>
  <artifactId>org.apache.poi.xwpf.converter.xhtml</artifactId>
  <version>XDOCREPORT_VERSION</version>
</dependency>
```

其中 XDOCREPORT\_VERSION 是 XDocReport 版本（例如：1.0.0）

## 示例

以下为将 org.apache.poi.xwpf.usermodel.XWPFDocument 转换为 XHTML 格式的示例：

```text
import org.apache.poi.xwpf.converter.xhtml.XHTMLOptions;
import org.apache.poi.xwpf.converter.xhtml.XHTMLConverter;

...
// 1) 将 DOCX 加载到 XWPFDocument 中
InputStream in= new FileInputStream(new File("HelloWord.docx"));
XWPFDocument document = new XWPFDocument(in);

// 2) 准备XHTML选项（这里我们设置`ImageManager`来存储图像并解析iamge src）
XHTMLOptions options = XHTMLOptions.create().setImageManager( new ImageManager( new File(root), "images" ) );

// 3) 将 XWPFDocument 转换为 XHTML
OutputStream out = new FileOutputStream(new File("HelloWord.htm"));
XHTMLConverter.getInstance().convert(document, out, options);
```

## XHTML Settings

### 图像提取

如果您的 docx 有图像并且您希望在 HTML 中显示，您可以为使用 XHTMLOptions 配置类 ImageManageroptions.setImageManager\( new ImageManager\( new File\(baseDir\), "images" \) \);

它将默认执行以下操作：

* `extract`  图像到 `baseDir/imageSubDir/` 下
* `resolve`  html中的图像src属性

### 内嵌图像

如果要使用 base64 将图像嵌入到 html 中，可以使用 Base64EmbedImgManager

```text
XHTMLOptions options = XHTMLOptions.create().indent( 4 ).setImageManager(new Base64EmbedImgManager());
```





