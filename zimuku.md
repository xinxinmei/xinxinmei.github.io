

```python
import requests
import bs4
from selenium.webdriver.common.keys import Keys
from selenium import webdriver
import time

prefs={
    'profile.default_content_setting_values': {
        'images': 2,
        'javascript':2
    }
}
def set(**prefs):
    chrome_options = webdriver.ChromeOptions()
    chrome_options.add_experimental_option('prefs',prefs)  #配置chrome设置
    #chrome_options.add_argument('--headless')     #配置是否显示窗口
    #chrome_options.add_argument('--disable-gpu')
    return chrome_options
chrome_options=set(**prefs)

headers={
'Host': 'www.zimuku.la',
'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:66.0) Gecko/20100101 Firefox/66.0',
    'Referer': 'http://www.zimuku.la/dld/117414.html',
}
"""data = {
    'poster': 'test',
    'syntax': 'cpp',
    'content': 'test',
}"""
"""cookie={
'PHPSESSID':'ar82gigsuuvpcs21uva6inmea2',
'yunsuo_session_verify':'99aacd1a74c689ae8d86f',
'zmk_home_view_subid':'112121',allow_redirects


}"""
web = webdriver.Chrome(chrome_options=chrome_options)
web.get("http://www.zimuku.la/")
elem1=web.find_element_by_name("q")
elem1.send_keys("反贪风暴")
elem1.send_keys(Keys.ENTER)
elem2=web.find_element_by_tag_name("tbody")
print(dir(elem2))
elem3 = elem2.find_element_by_tag_name("a")#再找到的元素中继续查找
elem3.click()                         #模拟点击元素
current= web.current_window_handle    #生成当前窗口句柄
handles = web.window_handles    #生成窗口句柄集合

web.switch_to_window(handles[1])
#print(dir(web))
#print(web.page_source)
elem4 = web.find_element_by_id("down1")
elem4.click()
"""
re=requests.get("http://www.zimuku.la/download/MTE3NDE0fDAxYzY1MDVmOGUwZDYzY2E0MGY5MzYxMHwxNTU1OTM4NzMxfGFjMDY0NjA1fGJhY2t1cA==/svr/bk1",headers=headers,allow_redirects=False)
print(dir(re))
print(re.headers)
#print(re.headers.get("Location"))
#print(requests.get(re.headers.get("Location")).headers)
#print(re.text)
"""
print(type(web.page_source))

```

    c:\users\mei\appdata\local\programs\python\python37-32\lib\site-packages\ipykernel_launcher.py:38: DeprecationWarning: use options instead of chrome_options
    

    ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_execute', '_id', '_parent', '_upload', '_w3c', 'clear', 'click', 'find_element', 'find_element_by_class_name', 'find_element_by_css_selector', 'find_element_by_id', 'find_element_by_link_text', 'find_element_by_name', 'find_element_by_partial_link_text', 'find_element_by_tag_name', 'find_element_by_xpath', 'find_elements', 'find_elements_by_class_name', 'find_elements_by_css_selector', 'find_elements_by_id', 'find_elements_by_link_text', 'find_elements_by_name', 'find_elements_by_partial_link_text', 'find_elements_by_tag_name', 'find_elements_by_xpath', 'get_attribute', 'get_property', 'id', 'is_displayed', 'is_enabled', 'is_selected', 'location', 'location_once_scrolled_into_view', 'parent', 'rect', 'screenshot', 'screenshot_as_base64', 'screenshot_as_png', 'send_keys', 'size', 'submit', 'tag_name', 'text', 'value_of_css_property']
    

    c:\users\mei\appdata\local\programs\python\python37-32\lib\site-packages\ipykernel_launcher.py:50: DeprecationWarning: use driver.switch_to.window instead
    

    <class 'str'>
    


```python

```


```python

```


```python

```


```python

```


```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import requests
import bs4
from lxml import etree
import time
import os
import random
def set_option():
    prefs={
        'profile.default_content_setting_values': {
        'images': 2,
        'javascript':2
        }
    }
    chrome_options = webdriver.ChromeOptions()
    chrome_options.add_experimental_option('prefs',prefs)  #配置chrome设置
    #chrome_options.add_argument('--headless')     #配置是否显示窗口
    #chrome_options.add_argument('--disable-gpu')
    return chrome_options
def get_data(movie_name):
    headers=[
        {
        'Host': 'www.zimuku.la',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:66.0) Gecko/20100101 Firefox/66.0',
        'Referer': 'http://www.zimuku.la/dld/117414.html',
    },
        {
        'Host': 'www.zimuku.la',
        'User-Agent': 'Opera/9.80 (Macintosh; Intel Mac OS X 10.6.8; U; en) Presto/2.8.131 Version/11.11',
        'Referer': 'http://www.zimuku.la/dld/117414.html',
    },
         {
        'Host': 'www.zimuku.la',
        'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; rv:2.0.1) Gecko/20100101 Firefox/4.0.1',
        'Referer': 'http://www.zimuku.la/dld/117414.html',
    },
         {
        'Host': 'www.zimuku.la',
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.6; rv:2.0.1) Gecko/20100101 Firefox/4.0.1',
        'Referer': 'http://www.zimuku.la/dld/117414.html',
    },
         {
        'Host': 'www.zimuku.la',
        'User-Agent': 'Mozilla/5.0 (Windows; U; Windows NT 6.1; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50',
        'Referer': 'http://www.zimuku.la/dld/117414.html',
    },
         {
        'Host': 'www.zimuku.la',
        'User-Agent': 'Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_8; en-us) AppleWebKit/534.50 (KHTML, like Gecko) Version/5.1 Safari/534.50',
        'Referer': 'http://www.zimuku.la/dld/117414.html',
    }
    ]
    chrome_options=set_option()
    web=webdriver.Chrome(chrome_options=chrome_options)
    url="http://www.zimuku.la/"
    web.get(url)
    elem1=web.find_element_by_name("q")
    elem1.send_keys(movie_name)
    elem1.send_keys(Keys.ENTER)
    elem2=web.find_element_by_tag_name("tbody")
    #print(dir(elem2))
    elem3 = elem2.find_element_by_tag_name("a")#再找到的元素中继续查找
    elem3.click()                         #模拟点击元素
    current= web.current_window_handle    #生成当前窗口句柄
    handles = web.window_handles    #生成窗口句柄集合
    web.switch_to_window(handles[1])
    #print(dir(web))
    #print(web.page_source)
    elem4 = web.find_element_by_id("down1")
    elem4.click()
    handles1=web.window_handles
    web.switch_to_window(handles1[2])
    html=web.page_source
    bs=bs4.BeautifulSoup(html,"lxml")
    xpath=etree.HTML(html)
    #print(dir(xpath))
    cont=xpath.xpath("//html/body/main/div/div/div/table/tbody/tr/td[1]/div/ul/li[6]/a/@href")
    end_url=url+cont[0]
    #print(end_url)
    i = random.randint(0,5)
    print(i)
    content=requests.get(end_url,headers=headers[i],allow_redirects=False)
   
    file=requests.get(content.headers.get("Location"))
    file_name=file.headers.get("Content-Disposition").split('filename=')[1].strip('"')
    print(file_name)
    
    format=file_name.split(".")[len(file_name.split("."))-1]
    
        
    
    if format in {"rar","zip"} :
        with open("D:\\python_study\\subtitles\\"+file_name,"wb") as f:
            f.write(file.content)
    else:
        with open("D:\\python_study\\subtitles\\"+file_name,"w") as f:
            f.write(file.text)
    web.quit()
if __name__=="__main__":
    movie_name=input()
    get_data(movie_name)
```

    钢铁侠1
    

    c:\users\mei\appdata\local\programs\python\python37-32\lib\site-packages\ipykernel_launcher.py:55: DeprecationWarning: use options instead of chrome_options
    c:\users\mei\appdata\local\programs\python\python37-32\lib\site-packages\ipykernel_launcher.py:67: DeprecationWarning: use driver.switch_to.window instead
    c:\users\mei\appdata\local\programs\python\python37-32\lib\site-packages\ipykernel_launcher.py:73: DeprecationWarning: use driver.switch_to.window instead
    

    5
    [zmk.pw]Iron.Man.2008.1080p.BluRay.x264.DTS-FGT.rar
    


```python

```


```python

```


```python

```


```python


```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```
