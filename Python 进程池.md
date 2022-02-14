# Python 进程池

```Python
from concurrent.futures import ThreadPoolExecutor
import threading
import time

import requests

# 一个简单的示例，创建一个包含两个线程的线程池，执行一百次访问百度首页
class Demo:
    count = 0

    @staticmethod
    def action(_):
        a = requests.get("https://www.baidu.com")
        Demo.count += 1
        return threading.current_thread().name + "  " + str(a.status_code) + "  " + str(Demo.count)


# 创建一个包含4条线程的线程池
with ThreadPoolExecutor(max_workers=2) as pool:
    # 使用线程执行map计算
    # 后面元组有3个元素，因此程序启动3条线程来执行action函数
    results = pool.map(Demo.action, range(100))

    for r in results:
        print(r)

```




![](image/%E7%BD%91%E9%A1%B5%E6%8D%95%E8%8E%B7_11-2-2022_115834_c.biancheng.net.jpeg)

