> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [baijiahao.baidu.com](https://baijiahao.baidu.com/s?id=1750021949025036730&wfr=spider&for=pc)

大家好，我是小智~

有两个表格，sheet2 需要根据指定列，在 sheet1 中查找，并将找到的行中内容，填充到指定的列中，实现方法如下：

![](https://pics7.baidu.com/feed/0b7b02087bf40ad173509dfd0d175bd4a9ecce3a.jpeg@f_auto?token=ca70ca02d128b52ed5cb43003e63a373)

**1、如下两个表格  
**

![](https://pics4.baidu.com/feed/1c950a7b02087bf4e971fde4a5e81d2710dfcfe1.jpeg@f_auto?token=7894ef6bf38a45ec771cd891bd963452)上图为 sheet1![](https://pics2.baidu.com/feed/9f2f070828381f308994a21aff3a06036f06f0be.jpeg@f_auto?token=f15636b44eded031531096dab1c6273d)

**2、通过 sheet2 中的学号，在 sheet1 中查找相同学号，并将 sheet1 中的姓名填充到 sheet2 中**

使用 vlookup 函数

VLOOKUP(lookup_value,table_array,col_index_num,[range_lookup])

![](https://pics4.baidu.com/feed/faedab64034f78f01aefc7352e0a405eb1191cd2.jpeg@f_auto?token=4b6ac4f7f1269d7315157ac3d40c375b)

**3、使用方法  
**

![](https://pics1.baidu.com/feed/95eef01f3a292df594221bfceb0a166b35a87338.jpeg@f_auto?token=1d4b0d24a05a861a72113bd24c8cf5fc)VLOOKUP 公式

公式：VLOOKUP(A2,Sheet1!A2:B6,2,FALSE)

先选中 C2 单元格，并在编辑栏输入函数公式：=VLOOKUP（）；然后输入 VLOOKUP 函数第 1 个参数：A2，为学号；第 2 个参数：到 sheet1 中，选择 A2:B6 单元格区域，位查询区域；第 3 个参数：2，代表查询区域第 2 列中的姓名；第 4 个参数：0，代表精确匹配；最后按回车键结束确认，即可用 VLOOKUP 函数；  

**最后复制公式到最后一行，得到最终的匹配结果  
**

![](https://pics6.baidu.com/feed/72f082025aafa40f91718fd3f25f494479f019cb.jpeg@f_auto?token=cbc409616991da8eae7aaea8d859655d)复制公式![](https://pics1.baidu.com/feed/95eef01f3a292df575ecfbccea0a166b35a87386.jpeg@f_auto?token=25a137fa4b3ace09cd138f2096c0a09f)匹配结果举报 / 反馈