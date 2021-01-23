---
title: "PdfToImage"
date: 2021-01-23T20:21:14+08:00
lastmod: 2021-01-23
author: "xiaonan"
math:
 enable: true

tags: [convert]
categories: [linux]
---

### Install

```bash
sudo pacman -S imagemagick
sudo pacman -S ghostscript
```

### Error[^BUG]
[^BUG]: [ImageMagick安全策略'PDF'阻止转换](https://qa.1r1g.com/sf/ask/3709883201/)

{{< admonition tip >}}

> convert: attempt to perform an operation not allowed by the security policy \`PDF\' @ error/constitute.c/IsCoderAuthorized/408.

> convert: no images defined `output.png' @ error/convert.c/ConvertImageCommand/3288.


`/etc/ImageMagick-7/policy.xml`

```xml
-: <policy domain="delegate" rights="none" pattern="gs" />

---

+: <policy domain="coder" rights="read | write" pattern="PDF" />

```

{{< /admonition >}}

### Convert[^convert]
[^convert]: [How to Convert PDF to Images with Imagemagick](https://jdhao.github.io/2019/11/20/convert_pdf_to_image_imagemagick/)

```
# convert single page of PDF file to image
convert presentation.pdf[0] test.jpg

# convert from page 0 to page 5
convert presentation.pdf[0-5] test.jpg
```

{{< admonition >}}
- `-density`
used to specify the DPI of the output images.

- `quality`
specify the quality for the generated images.

- `%3d`
used to specify the format for generated image names. The generated images will be named `output-001.jpg`, `output-002.jpg`
{{< /admonition >}}

