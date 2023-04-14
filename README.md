# urlpa

import requests
import re

# 设置headers
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3'}
# 设置搜索关键词
keyword = "inurl:/php?id=1"

# 爬取搜索引擎的结果
urls = []
for page in range(0, 101, 10):
    url = "https://www.google.com/search?q={}&start={}".format(keyword, page)
    r = requests.get(url, headers=headers)
    # 使用正则表达式匹配所有url
    urls += re.findall('href="(https?://.*?)"', r.text)

# 去重
urls = list(set(urls))

# 将url保存到文件
with open('urls.txt', 'w') as f:
    for url in urls:
        f.write(url + '\n')
