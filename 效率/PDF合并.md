```python
# -*- coding:utf-8*-
# 利用PyPDF2模块合并同一文件夹下的所有PDF文件
# 只需修改存放PDF文件的文件夹变量：file_dir 和 输出文件名变量: outfile

import os, sys, codecs
from PyPDF2 import PdfFileReader, PdfFileWriter, PdfFileMerger
import time


# 使用os模块的walk函数，搜索出指定目录下的全部PDF文件
# 获取同一目录下的所有PDF文件的绝对路径
def getFileName(filedir):
    file_list = [os.path.join(root, filespath) \
                 for root, dirs, files in os.walk(filedir) \
                 for filespath in files \
                 if str(filespath).endswith('pdf')
                 ]
    return file_list if file_list else []


# 合并同一目录下的所有PDF文件
def MergePDF(filepath, outfile):
    merger = PdfFileMerger(strict=False)

    outputPages = 0
    pdf_fileName = getFileName(filepath)
    if pdf_fileName:
        for pdf_file in pdf_fileName:
            f = open(pdf_file, "rb")

            print("路径：%s" % pdf_file)

            # 读取源PDF文件
            input = PdfFileReader(f)
            # input = PdfFileReader(open(pdf_file,'rb'))
            # input = PdfFileReader(open(pdf_file, "rb"))

            # 获得源PDF文件中页面总数
            merger.append(input, import_bookmarks=False)

            print("合并文件:%s." % pdf_file)
            f.close()
        # 写入到目标PDF文件
        out_filename = os.path.join(os.path.abspath(filepath), outfile)
        out = open(out_filename, "wb")
        merger.write(out)
        print('合并后的输出文件：%s' % (out_filename))
        merger.close()
        print("PDF文件合并完成！")

    else:
        print("没有可以合并的PDF文件！")


# 主函数
def main():
    time1 = time.time()
    file_dir = '/Users/free.hao/Downloads/demo-batch-markdown-to-pdf-master/pdf'  # 存放PDF的原文件夹
    outfile = "merger.pdf"  # 输出的PDF文件的名称
    MergePDF(file_dir, outfile)
    time2 = time.time()
    print('总共耗时：%s s.' % (time2 - time1))


main()


```