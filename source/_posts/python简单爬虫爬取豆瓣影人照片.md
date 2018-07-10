---
title: python简单爬虫爬取豆瓣影人照片
date: 2018-03-18 18:17:08
tags: 
- Python
- 爬虫
categories: 学习
---

```python
# -*- coding: utf-8 -*-
from bs4 import BeautifulSoup
import requests, os, re
from urllib.parse import urljoin

# 豆瓣图片爬虫

class SpiderMain(object):


    # 获取该页面上单独图片页面的链接
    def _get_new_urls(self, page_url, soup):
        new_urls = set()
        reg = r"https://movie.douban.com/celebrity/" + page_url.split('/')[4] + r"/photo/\d+/$"      #正则表达式
        links = soup.find_all('a', href=re.compile(reg))
        for link in links:
            new_url = link['href']
            new_full_url = urljoin(page_url, new_url)
            new_urls.add(new_full_url)
        return new_urls

    #获取该名人的姓名作为图片文件夹名
    def _get_name(self, root_url):
        response = requests.get(root_url)
        html_cont = response.content
        soup = BeautifulSoup(html_cont, 'html.parser')
        name = soup.find("div", attrs={"id":"content"}).h1.text.split()[0]
        return name

    # 爬图片开始喽
    def crawl(self, root_url):
        dir_name = self._get_name(root_url)
        dirIsExist = os.path.exists(os.getcwd() + r'\\douban\\%s'%dir_name)       #该文件夹是否存在
        if not dirIsExist:
            os.makedirs(os.getcwd() + r'\\douban\\%s'%dir_name)         #创建图片文件夹
        os.chdir(os.path.join(os.getcwd(), r'douban\\%s'%dir_name))     #进入该文件夹

        n = 1          #图片数量
        page = 0       #图片页码

        while page < 2:
            url_ = root_url + "photos/?start=%d" % (page*40)

            html_cont = requests.get(url_).content

            soup = BeautifulSoup(html_cont, 'html.parser')

            urls = self._get_new_urls(url_, soup)

            for url in urls:
                pic_name = str(n) + '.jpg'
                img_url = "https://img1.doubanio.com/view/photo/l/public/p" + url.split('/')[6] + ".jpg"
                pic = requests.get(img_url)
                with open(pic_name, 'wb') as file:      #open函数?
                    file.write(pic.content)
                    file.flush()
                file.close()
                print("Crawl " + str(n) + " : " + img_url)
                n += 1
            page += 1
        print("Crawl succeed !")


if __name__=="__main__":
    root_url = "https://movie.douban.com/celebrity/%d/" % 1274424       #只需修改该影人的豆瓣ID
    obj_spider = SpiderMain()
    obj_spider.crawl(root_url)
```
 



------------



