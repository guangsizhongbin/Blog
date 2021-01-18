---
title: "Momo"
date: 2021-01-18T20:55:50+08:00
lastmod: 2021-01-18
author: "xiaonan"
math:
 enable: true

tags: [momo]
categories: [python]
---

### URL拼接 替换参数[^python3 使用format函数对URL进行拼接]
[^python3 使用format函数对URL进行拼接]:[python3 使用format函数对URL进行拼接](https://blog.csdn.net/weixin_43837330/article/details/92159677)

```python
url = 'https://www.aliexpress.com/item/{}.html'.format(123)
print(url)
```

> https://www.aliexpress.com/item/123.html

### termcolor[^python库termcolor用法]
[^python库termcolor用法]: [python库termcolor用法](https://www.cnblogs.com/everfight/p/python_termcolor.html)

> colored(text, color=None, on_color=None, attrs=None)

color: 字体颜色， on_color: 背景颜色

```python
from termcolor import colored, cprint

text = colored('Hello, World!','red', 'on_white', attrs=['blink'])
print(text)

cprint('Hello, World!', 'red', 'on_white', attrs=['blink'])
```


![](https://img.fengqigang.cn//img/20210118211955.png)

### momo
```python
#encoding: utf8
import aiohttp
import asyncio
from termcolor import colored
from requests import get
import re
import time
import sys
ids = ()

def getProxy(completion, TargetNum, proxynum, ProxyList):
    global proxies

    if completion >= TargetNum:
        return 0
 ##   print('[+] %s' % colored('get proxy...', 'blue', attrs=['bold']), end='')

    while 1:
        try:
            url = 'http://www.89ip.cn/tqdl.html?num=%s' % proxynum
            html = get(url).text

            proxies = set(re.findall(
                r"[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}:[0-9]+", html)) - set(ProxyList)

            if not len(proxies):
##                print('\n  [-]Waiting')
                time.sleep(3)
                continue

  ##          print(colored('[%d]' % len(proxies), 'yellow', attrs=['bold']), '%s' % (
   ##             colored('Done!', 'green', attrs=['bold'])))
            return 1
        except Exception as e:
    ##        print('\n  [-]Error: ' + str(e))
            time.sleep(5)


async def autoVisit(proxy, sem):
    global ProxyList, completion
    async with sem:
        async with aiohttp.ClientSession() as session:
            try:
                for id in ids:
                    async with session.get(url=id, proxy='http://' + proxy, timeout=5) as resp:
                        print('[%s]' % colored(proxy, 'cyan', attrs=['bold']),
                           colored('Successfully!', 'green', attrs=['bold']))
                        ProxyList.append(proxy)
                        completion += 1
            except Exception as e:
                print('', end='')


proxies = []
ProxyList = []
completion = 0

# how many proxies you want to
# get in one request of free proxy site
proxynum = 100

# how many visition your want to get
TargetNum = 40

loop = asyncio.get_event_loop()
sem = asyncio.Semaphore(proxynum)
while getProxy(completion, TargetNum, proxynum, ProxyList):
    tasks = [asyncio.ensure_future(autoVisit(i, sem)) for i in proxies]
    loop.run_until_complete(asyncio.wait(tasks))
loop.close()
print(colored(completion, 'yellow', attrs=['bold']))


```
