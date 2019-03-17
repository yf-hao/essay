```python

from pathlib import Path
import os
from sys import argv

work_dir = Path.cwd()
md_dir = ''
length = len(argv)

export_html_dir = work_dir
export_pdf_dir = work_dir / 'pdf'
css_file = work_dir / 'css/githb.css'

if length == 1:
    md_dir = work_dir / 'md'
elif length == 2:
    md_dir = argv[1]

if not export_html_dir.exists():
    export_html_dir.mkdir()
if not export_pdf_dir.exists():
    export_pdf_dir.mkdir()

for md_file in list(Path(md_dir).glob('*.md')):
    md_file_name = md_file.name
    html_file_name = md_file_name.replace('.md', '.html')
    html_file = export_html_dir / html_file_name
    cmd = "/usr/local/Cellar/pandoc/2.1.1/bin/pandoc -s -f gfm -t html5 --metadata=title:'{}' --css=css/pandoc.css '{}' -o '{}'".format(
        md_file_name, md_file, html_file)
    os.system(cmd)
for html_file in list(export_html_dir.glob('*.html')):
    html_file_name = html_file.name
    pdf_file_name = html_file_name.replace('.html', '.pdf')
    pdf_file = export_pdf_dir / pdf_file_name
    cmd = "wkhtmltopdf --quiet  --outline '{}'  '{}'".format(html_file, pdf_file)
    os.system(cmd)
    os.system("rm -f '{}' ".format(html_file_name))

```