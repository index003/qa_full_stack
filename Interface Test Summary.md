# Interface Test Summary

## 第一部分 request get

```python
""" 使用requests get """
# request_get01.py

import requests
import json

# 基本GET
response = requests.get("http://httpbin.org/get")
# print(type(response))
# print(response.status_code)
# print(type(response.text))
response.encoding = 'utf-8'
print(response.text)
# print(response.cookies)
print('=========================================')
# print(response.content)
print(response.content.decode("utf-8"))
print('=========================================')

'''
response.text返回的是Unicode格式，通常需要转换为utf-8格式，否则就是乱码。
response.content是二进制模式，可以下载视频之类的，如果想看的话需要decode成utf-8格式。
不管是通过response.content.decode("utf-8)的方式
还是通过response.encoding="utf-8"的方式都可以避免乱码的问题发生
'''
'''
# 一大推请求方式
requests.post("http://httpbin.org/post")
requests.put("http://httpbin.org/put")
requests.delete("http://httpbin.org/delete")
requests.head("http://httpbin.org/get")
requests.options("http://httpbin.org/get")
'''

# 带参数的GET请求

url = 'http://httpbin.org/get'
data = {
    'name':'zhangsan',
    'age':'25'
}

response = requests.get(url,params=data)
print('response.text ===>',response.text)
response.encoding = 'utf-8'
print(type(json.loads(response.text)))
print(json.loads(response.text))
print(response.text)
# print(response.cookies)
print('=========================================')
# print(response.content)
print(response.content.decode("utf-8"))
print('=========================================')


"""使用json"""
# request_get02.py
import json
import requests

response = requests.get("http://httpbin.org/get")
res = response.json()
# print(type(response.text))
print('=========================================')
print(res)
print('=========================================')
print(json.dumps(res, sort_keys=True, indent=2))
print('=========================================')
print(json.loads(response.text))
print('=========================================')
# print(type(response.json()))
print('=========================================')
# 打印请求页面的状态（状态码）
print(type(response.status_code),response.status_code)
print('=========================================')
# 打印请求网址的headers所有信息
print(type(response.headers),response.headers)
print('=========================================')
# 打印请求网址的cookies信息
print(type(response.cookies),response.cookies)
print('=========================================')
# 打印请求网址的地址
print(type(response.url),response.url)
print('=========================================')
# 打印请求的历史记录（以列表的形式显示）
# print(type(response.history),response.history)
print('=========================================')

# 添加Header头
url = 'https://www.zhihu.com/'
headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/57.0.2987.133 Safari/537.36'
}
response = requests.get(url, headers=headers)
response.encoding = 'utf-8'
print(response.text)
```

## 第二部分 request post

```python
"""使用requests post"""
# 基本post请求：
# 通过post把数据提交到url地址，等同于一字典的形式提交form表单里面的数据

import requests
url = 'http://httpbin.org/post'
data = {
    'name':'zhangsan',
    'age':'25'
}

response = requests.post(url,data=data)
print(response.url)
print(response.text)

# 打印请求页面的状态（状态码）
print(type(response.status_code),response.status_code)
# 打印请求网址的headers所有信息
print(type(response.headers),response.headers)
# 打印请求网址的cookies信息
print(type(response.cookies),response.cookies)
# 打印请求网址的地址
print(type(response.url),response.url)
# 打印请求的历史记录（以列表的形式显示）
print(type(response.history),response.history)

# 使用request内置的字母判断状态码
# 如果response返回的状态码是非正常的就返回404错误
if response.status_code != requests.codes.ok:
    print('404')
 
# 如果页面返回的状态码是200，就打印下面的状态
response = requests.get('http://www.jianshu.com')
if response.status_code == 200:
    print('200')
```

## 第三部分 整合request

```python
"""get和post最原始的方法"""
import requests
import json

# 请求需要的url和参数
get_url = 'http://httpbin.org/get'
data = {
    'name': 'zhangsan',
    'age': '25'
}

# 发送请求的结果
response_get = requests.get(get_url, params=data)
# 将结果转码，大部分情况不需要
response_get.encoding = 'utf-8'
# 字符串方式
print(response_get.text)
# 转为json，字典方式
res_get = json.loads(response_get.text)
print(res_get)
print("=========这是分割线===========")
post_url = 'http://httpbin.org/post'
# 发送请求的结果
response_post = requests.post(post_url, data=data)
# 将结果转码，大部分情况不需要
response_post.encoding = 'utf-8'
# 字符串方式
print(response_post.text)
# 转为json，字典方式
res_post = json.loads(response_post.text)
print(res_post)

"""使用类（即面向对象）的方式实现函数式的requests的get和post请求"""
import json
import requests

def json_dumps(data):
    return json.dumps(data)

class RunMain:
    def send_get(self, url, param=None, header=None):
        response = requests.get(url=url, params=param, headers=header)
        return json.loads(response.text)

    def send_post(self, url, data, header=None):
        if data is not None:
            data = json_dumps(data)
        response = requests.post(url=url, data=data, headers=header)
        return json.loads(response.text)

    def run_main(self, url, method, data=None, headers=None):
        res = None
        if method == 'GET':
            res = self.send_get(url, data)
        else:
            res = self.send_post(url, data)
        return res


if __name__ == '__main__':  # 本方法内使用

    get_url = 'http://httpbin.org/get'
    post_url = 'http://httpbin.org/post'
    datalist = {
        'name': 'zhangsan',
        'age': '25'
    }
    # 实例化
    # 如果__init__启用，就需要下面方式实例化
    # run = RunMain(baseurl, 'GET', datalist)
    run = RunMain()
    # 调用类run_main()方法
    response_main_get = run.run_main(get_url, 'GET', datalist)
    print(response_main_get)

    response_main_post = run.run_main(post_url, 'POST', datalist)
    print(response_main_get)

    # 调用类get()方法
    response_get = run.send_get(get_url, param=datalist)
    print(response_get)

    # 调用类post()方法
    response_post = run.send_post(post_url, datalist)
    print(response_post)

```

## 第四部分 request test method

```python
#########
# get_post_requests.py
"""get post方法，供unittest调用"""

import json
import requests


def json_dumps(data):
    return json.dumps(data)


class RunMain():

    def send_get(self, url, param=None, header=None):
        response = requests.get(url=url, params=param, headers=header)
        return json.loads(response.text)

    def send_post(self, url, data, header=None):
        if data is not None:
            data = json_dumps(data)
        response = requests.post(url=url, data=data, headers=header)
        return json.loads(response.text)

    def run_main(self, url, method, data=None, headers=None):
        res = None
        if method == 'GET':
            res = self.send_get(url, data)
        else:
            res = self.send_post(url, data)
        return res
    
    #########
    # run_unittest.py
    """使用unittest调用oop的get和post请求"""
import unittest
from get_post_requests import RunMain


class TestMethod(unittest.TestCase):

    def setUp(self):
        self.run = RunMain()

    def test_001_get(self):
        get_url = 'http://httpbin.org/get'
        datalist = {
            'name': 'zhangsan',
            'age': '25'
        }
        res = self.run.run_main(get_url, 'GET', datalist)
        print(res)
        self.assertEqual(res['args']['age'], '25', 'Passed')

    # @unittest.skip('test_002_post')   # 当前用例不执行
    def test_002_post(self):
        post_url = 'http://httpbin.org/post'
        datalist = {
            'name': 'zhangsan',
            'age': '25'
        }
        res = self.run.run_main(post_url, 'POST', datalist)
        print(res)
        self.assertEqual(res['json']['age'], '26', 'Failed')


if __name__ == '__main__':
    # unittest.main()   # 全部执行，下面的方式可以自己组织
    suite = unittest.TestSuite()
    suite.addTest(TestMethod('test_001_get'))
    suite.addTest(TestMethod('test_002_post'))
    unittest.TextTestRunner().run(suite)
    
#########
# run_htmltestrunner.py
"""使用HTMLTestRunner调用oop的get和post请求，并且生成报告"""
import unittest
from get_post_requests import RunMain
from HTMLTestRunner import HTMLTestRunner
import time
import os
import sys


class TestMethod(unittest.TestCase):

    def setUp(self):
        self.run = RunMain()

    def test_001_get(self):
        baseurl = 'http://httpbin.org/get'
        datalist = {
            'name': 'zhangsan',
            'age': '25'
        }
        res = self.run.run_main(baseurl, 'GET', datalist)
        self.assertEqual(res['args']['age'], '25', 'Passed')

    # @unittest.skip('test_002_post')   # 当前用例不执行
    def test_002_post(self):
        baseurl = 'http://httpbin.org/post'
        datalist = {
            'name': 'zhangsan',
            'age': '25'
        }
        res = self.run.run_main(baseurl, 'POST', datalist)
        self.assertEqual(res['json']['age'], '25', 'Failed')


if __name__ == '__main__':
    # unittest.main()   # 全部执行，下面的方式可以自己组织
    suite = unittest.TestSuite()
    suite.addTest(TestMethod('test_001_get'))
    suite.addTest(TestMethod('test_002_post'))

    now = time.strftime("%Y-%m-%d %H-%M-%S")

    # public_path = os.getcwd()
    # print('本文件目录位置：' + public_path)
    # filename = os.path.join(public_path, 'report', now + '.html')
    # print('报告存放路径  ：' + public_path)

    # public_path = public_path = os.path.dirname(__file__)  # 当前执行文件的路径 推荐使用这种方式
    # print('本文件目录位置：' + public_path)
    # filename = os.path.join(public_path, 'report', now + '.html')
    # print('报告存放路径  ：' + filename)

    # public_path = os.path.dirname(os.path.abspath(sys.argv[0]))  # 获取当前运行的.py文件所在的绝对路径
    # print('本文件目录位置：' + public_path)
    # filename = os.path.join(public_path, 'report', now + 'report.html')
    # print('报告存放路径  ：' + filename)

    filename = os.path.join('./', 'report', now + 'report.html')

    with open(filename, 'wb') as wf:
        # 定义测试报告
        runner = HTMLTestRunner(
            stream=wf,
            title="get post HTMLTestRunner",
            description="description"
        )
        runner.run(suite)
        

```

## 第五部分 数据分离调用request

```python
#########
# common.get_post_requests.py
"""get、post及断言获取方法，供api调用调用"""

import requests
import json
import jsonpath


def json_dumps(data):
    return json.dumps(data)


class RunMain():

    def send_get(self, url, param=None, header=None):
        # response = requests.get(url=url, params=param, headers=header)
        # return json.loads(response.text)
        return requests.get(url=url, params=param, headers=header)

    def send_post(self, url, data, header=None):
        if data is not None:
            data = json_dumps(data)
        # response = requests.post(url=url, data=data, headers=header)
        # return json.loads(response.text)
        return requests.post(url=url, data=data, headers=header)

    def run_main(self, url, method, data=None, headers=None):
        res = None
        if method == 'GET':
            res = self.send_get(url, data)
        else:
            res = self.send_post(url, data)
        return res

    # 根据key获取res字典中的value
    def get_text(self, res, key):

        if res is not None:
            try:
                # 将res文本转换为JSON，通过jsonpath解析获取到指定的key的value值。
                text = json.loads(res)
                value = jsonpath.jsonpath(text, '$..{0}'.format(key))
                # jsonpath获取的结果是list类型的值,如果获取失败则是False
                if value:
                    # 将list转成String格式
                    if len(value) == 1:
                        return value[0]
                return value
            except Exception as e:
                return e
        else:
            return None
        
#########
# config.config.ini
[DEFAULT]
url = http://httpbin.org/

#########
# data.get.yaml data.post.yaml
path: get
data:
  name: zhangsan
  age: '25'
text: zhangsan

path: post
data:
  name: zhangsan
  age: '25'
text: zhangsan

#########
# yaml_function.py
"""使用数据分离调用get和post"""

import configparser
import yaml
from common.get_post_requests import RunMain


# 实例化需要的内容
conf = configparser.ConfigParser()
rm = RunMain()

with open('./data/get.yaml', 'r', encoding='utf-8') as f:
    get_data = yaml.safe_load(f)

# get测试数据
conf.read('./config/config.ini')
get_url = conf.get('DEFAULT', 'url') + get_data['path']

# 执行get测试
res = rm.run_main(get_url, 'GET', get_data['data'])
print(res.text)

print('===========这是分割线===========')

with open('./data/post.yaml', 'r', encoding='utf-8') as f:
    post_data = yaml.safe_load(f)

# post测试数据
conf.read('./config/config.ini')
post_url = conf.get('DEFAULT', 'url') + post_data['path']

# 执行post测试
res = rm.run_main(post_url, 'POST', post_data['data'])
print(res.text)

#########
# yaml_oop.py
"""将function_yaml改成面向对象方式"""

import configparser
import yaml
from common.get_post_requests import RunMain


class OopRequests:

    # 实例化需要的内容
    conf = configparser.ConfigParser()
    rm = RunMain()

    with open('./data/get.yaml', 'r', encoding='utf-8') as f:
        get_data = yaml.safe_load(f)

    # get测试数据
    conf.read('./config/config.ini')
    get_url = conf.get('DEFAULT', 'url') + get_data['path']

    # 执行get测试
    res = rm.run_main(get_url, 'GET', get_data['data'])
    print(res.text)

    print('===========这是分割线===========')

    with open('./data/post.yaml', 'r', encoding='utf-8') as f:
        post_data = yaml.safe_load(f)

    # post测试数据
    conf.read('./config/config.ini')
    post_url = conf.get('DEFAULT', 'url') + post_data['path']

    # 执行post测试
    res = rm.run_main(post_url, 'POST', post_data['data'])
    print(res.text)


if __name__ == '__main__':  # 本方法内使用
    pass

```

## 第六部分 数据分离unittest 

```python
#########
# cases.test_get.py
"""供discover调用"""
import configparser
import unittest
import ddt
from common.get_post_requests import RunMain


@ddt.ddt
class TestMethodDDT(unittest.TestCase):
    @classmethod
    def setUpClass(cls) -> None:
        cls.value = None
        # 实例化需要的内容
        conf = configparser.ConfigParser()
        conf.read('./config/config.ini')
        cls.url = conf.get('DEFAULT', 'url')
        cls.rm = RunMain()

    def setUp(self):
        print('<=================>')

    @ddt.file_data('../data/get_ddt.yaml')
    def test_001_get(self, **kwargs):
        url = self.url + kwargs['path']
        # # 执行测试
        res = self.rm.run_main(url, 'GET', kwargs['data'])
        print(res.text)

        TestMethodDDT.value = self.rm.get_text(res.text, 'name')
        print(self.value)
        self.assertEqual(first=kwargs['text'], second=self.value, msg='获取信息失败')


if __name__ == '__main__':
    unittest.main()
    
# cases.test_post.py    
"""供discover调用"""
import configparser
import unittest
import ddt
from common.get_post_requests import RunMain


@ddt.ddt
class TestMethodDDT(unittest.TestCase):
    @classmethod
    def setUpClass(cls) -> None:
        cls.value = None
        # 实例化需要的内容
        conf = configparser.ConfigParser()
        conf.read('./config/config.ini')
        cls.url = conf.get('DEFAULT', 'url')
        cls.rm = RunMain()

    def setUp(self):
        print('<=================>')

    @ddt.file_data('../data/post_ddt.yaml')
    def test_001_get(self, **kwargs):
        url = self.url + kwargs['path']
        # # 执行测试
        res = self.rm.run_main(url, 'POST', kwargs['data'])
        print(res.text)

        TestMethodDDT.value = self.rm.get_text(res.text, 'name')
        print(self.value)
        self.assertEqual(first=kwargs['text'], second=self.value, msg='获取信息失败')


if __name__ == '__main__':
    unittest.main()

#########
# common.get_post_requests.py
"""get、post及断言获取方法，供api调用调用"""
import requests
import json
import jsonpath


def json_dumps(data):
    return json.dumps(data)


class RunMain:

    def send_get(self, url, param=None, header=None):
        # response = requests.get(url=url, params=param, headers=header)
        # return json.loads(response.text)
        return requests.get(url=url, params=param, headers=header)

    def send_post(self, url, data, header=None):
        if data is not None:
            data = json_dumps(data)
        # response = requests.post(url=url, data=data, headers=header)
        # return json.loads(response.text)
        return requests.post(url=url, data=data, headers=header)

    def run_main(self, url, method, data=None, headers=None):
        res = None
        if method == 'GET':
            res = self.send_get(url, data)
        else:
            res = self.send_post(url, data)
        return res

    # 根据key获取res字典中的value
    def get_text(self, res, key):

        if res is not None:
            try:
                # 将res文本转换为JSON，通过jsonpath解析获取到指定的key的value值。
                text = json.loads(res)
                value = jsonpath.jsonpath(text, '$..{0}'.format(key))
                # jsonpath获取的结果是list类型的值,如果获取失败则是False
                if value:
                    # 将list转成String格式
                    if len(value) == 1:
                        return value[0]
                return value
            except Exception as e:
                return e
        else:
            return None

#########
# config.config.ini
[DEFAULT]
url = http://httpbin.org/

#########
# data.get.yaml
path: get
data:
  name: zhangsan
  age: '25'
text: zhangsan
    
# data.get_ddt.yaml 
demo:
  path: get
  data:
    name: zhangsan
    age: '25'
  text: zhangsan
demo2:
  path: get
  data:
    name: lisi
    age: '28'
  text: lisi
    
# data.post.yaml 
path: post
data:
  name: zhangsan
  age: '25'
text: zhangsan
    
# data.post_ddt.yaml
demo:
  path: post
  data:
    name: zhangsan
    age: '25'
  text: zhangsan
demo2:
  path: post
  data:
    name: lisi
    age: '28'
  text: lisi

#########
# report文件夹

#########
# run_unittest.py
"""数据分离使用unittest调用get和post请求"""
import configparser
import unittest
import yaml
from common.get_post_requests import RunMain


class TestMethod(unittest.TestCase):
    @classmethod
    def setUpClass(cls) -> None:
        cls.value = None
        # 实例化需要的内容
        conf = configparser.ConfigParser()
        conf.read('./config/config.ini')
        cls.url = conf.get('DEFAULT', 'url')
        cls.rm = RunMain()

    def test_001_get(self):
        with open('./data/get.yaml', 'r', encoding='utf-8') as f:
            data = yaml.safe_load(f)
        url = self.url + data['path']
        # # 执行测试
        res = self.rm.run_main(url, 'GET', data['data'])
        print(res.text)

        TestMethod.value = self.rm.get_text(res.text, 'name')
        print(self.value)
        self.assertEqual(first=data['text'], second=self.value, msg='获取信息失败')

    # @unittest.skip('test_002_post')   # 当前用例不执行
    def test_002_post(self):
        with open('./data/post.yaml', 'r', encoding='utf-8') as f:
            data = yaml.safe_load(f)
        url = self.url + data['path']
        # 执行测试
        res = self.rm.run_main(url, 'POST', data['data'])
        print(res.text)
        self.assertEqual(res['form']['age'], '26', 'Failed')


if __name__ == '__main__':
    # unittest.main()   # 全部执行，下面的方式可以自己组织
    suite = unittest.TestSuite()
    suite.addTest(TestMethod('test_001_get'))
    suite.addTest(TestMethod('test_002_post'))
    unittest.TextTestRunner().run(suite)


# run_unittest_ddt.py
"""使用ddt方式管理数据，unittest调用oop的get和post请求"""
import configparser
import sys
import unittest
import ddt

from common.get_post_requests import RunMain


@ddt.ddt
class TestMethodDDT(unittest.TestCase):
    @classmethod
    def setUpClass(cls) -> None:
        cls.value = None
        # 实例化需要的内容
        conf = configparser.ConfigParser()
        conf.read('./config/config.ini')
        cls.url = conf.get('DEFAULT', 'url')
        cls.rm = RunMain()

    def setUp(self):
        print('<=================>')

    @ddt.file_data('./data/get_ddt.yaml')
    def test_001_get(self, **kwargs):
        get_url = self.url + kwargs['path']
        # # 执行测试
        res = self.rm.run_main(get_url, 'GET', kwargs['data'])

        TestMethodDDT.value = self.rm.get_text(res.text, 'name')
        self.assertEqual(first=kwargs['text'], second=self.value, msg='获取信息失败')

    # @unittest.skip('test_002_post')   # 当前用例不执行
    @ddt.file_data('./data/post_ddt.yaml')
    def test_002_post(self, **kwargs):
        post_url = self.url + kwargs['path']
        # # 执行测试
        res = self.rm.run_main(post_url, 'POST', kwargs['data'])

        TestMethodDDT.value = self.rm.get_text(res.text, 'name')
        self.assertEqual(first=kwargs['text'], second=self.value, msg='获取信息失败')


if __name__ == '__main__':
    # unittest.main()   # 全部执行，下面的方式可以自己组织
    # unittest.main(argv=sys.argv, testRunner=unittest.TextTestRunner(verbosity=2))  # 全部执行，并且打印调用的用例
    suite = unittest.TestSuite()
    suite.addTest(TestMethodDDT('test_001_get_00001_demo'))
    suite.addTest(TestMethodDDT('test_001_get_00002_demo2'))
    suite.addTest(TestMethodDDT('test_002_post_00001_demo'))
    suite.addTest(TestMethodDDT('test_002_post_00002_demo2'))
    unittest.TextTestRunner().run(suite)


# run_htmltestrunner.py
"""使用htmltestrunner执行测试，并且生成报告"""
import configparser
import unittest
import yaml
import time
import os
import sys
from HTMLTestRunner import HTMLTestRunner
from common.get_post_requests import RunMain


class TestMethod(unittest.TestCase):

    @classmethod
    def setUpClass(cls) -> None:
        cls.value = None
        # 实例化需要的内容
        conf = configparser.ConfigParser()
        conf.read('./config/config.ini')
        cls.url = conf.get('DEFAULT', 'url')
        cls.rm = RunMain()

    def test_001_get(self):
        with open('./data/get.yaml', 'r', encoding='utf-8') as f:
            data = yaml.safe_load(f)
        url = self.url + data['path']
        # # 执行测试
        res = self.rm.run_main(url, 'GET', data['data'])
        print(res.text)

        TestMethod.value = self.rm.get_text(res.text, 'name')
        print(self.value)
        self.assertEqual(first=data['text'], second=self.value, msg='获取信息失败')

    # @unittest.skip('test_002_post')   # 当前用例不执行
    def test_002_post(self):
        with open('./data/post.yaml', 'r', encoding='utf-8') as f:
            data = yaml.safe_load(f)
        url = self.url + data['path']
        # 执行测试
        res = self.rm.run_main(url, 'POST', data['data'])
        print(res.text)
        self.assertEqual(res['form']['age'], '26', 'Failed')


if __name__ == '__main__':
    # unittest.main()   # 全部执行，下面的方式可以自己组织
    suite = unittest.TestSuite()
    suite.addTest(TestMethod('test_001_get'))
    suite.addTest(TestMethod('test_002_post'))

    now = time.strftime("%Y-%m-%d %H-%M-%S")
    # public_path = os.path.dirname(os.path.abspath(sys.argv[0]))  # 获取当前运行的.py文件所在的绝对路径
    # public_path = os.path.dirname(__file__)  # 当前执行文件的路径 推荐使用这种方式
    # filename = public_path + "/report/" + now + "report.html"
    # filename = os.path.join(public_path, 'report', now + 'report.html')
    filename = os.path.join('./', 'report', now + 'report.html')
    print('==========', filename)
    with open(filename, 'wb') as wf:
        # 定义测试报告
        runner = HTMLTestRunner(
            stream=wf,
            title="get post HTMLTestRunner",
            description="description"
        )
        runner.run(suite)


# run_htmltestrunner_ddt.py
"""使用unittest调用oop的get和post请求"""
import configparser
import os
import time
import unittest
import ddt
import sys
from HTMLTestRunner import HTMLTestRunner
from common.get_post_requests import RunMain


@ddt.ddt
class TestMethodDDT(unittest.TestCase):
    @classmethod
    def setUpClass(cls) -> None:
        cls.value = None
        # 实例化需要的内容
        conf = configparser.ConfigParser()
        conf.read('./config/config.ini')
        cls.url = conf.get('DEFAULT', 'url')
        cls.rm = RunMain()

    def setUp(self):
        print('<=================>')

    @ddt.file_data('./data/get_ddt.yaml')
    def test_001_get(self, **kwargs):
        get_url = self.url + kwargs['path']
        # # 执行测试
        res = self.rm.run_main(get_url, 'GET', kwargs['data'])
        print(res.text)

        TestMethodDDT.value = self.rm.get_text(res.text, 'name')
        print(self.value)
        self.assertEqual(first=kwargs['text'], second=self.value, msg='获取信息失败')

    # @unittest.skip('test_002_post')   # 当前用例不执行
    @ddt.file_data('./data/post_ddt.yaml')
    def test_002_post(self, **kwargs):
        post_url = self.url + kwargs['path']
        # # 执行测试
        res = self.rm.run_main(post_url, 'POST', kwargs['data'])
        print(res.text)

        TestMethodDDT.value = self.rm.get_text(res.text, 'name')
        print(self.value)
        self.assertEqual(first=kwargs['text'], second=self.value, msg='获取信息失败')


if __name__ == '__main__':
    # unittest.main()   # 全部执行，下面的方式可以自己组织
    # unittest.main(argv=sys.argv, testRunner=unittest.TextTestRunner(verbosity=2))  # 全部执行，并且打印调用的用例
    suite = unittest.TestSuite()
    suite.addTest(TestMethodDDT('test_001_get_00001_demo'))
    suite.addTest(TestMethodDDT('test_001_get_00002_demo2'))
    suite.addTest(TestMethodDDT('test_002_post_00001_demo'))
    suite.addTest(TestMethodDDT('test_002_post_00002_demo2'))
    # unittest.TextTestRunner().run(suite)

    now = time.strftime("%Y-%m-%d %H-%M-%S")
    # public_path = os.path.dirname(os.path.abspath(sys.argv[0]))  # 获取当前运行的.py文件所在的绝对路径
    # filename = os.path.join(public_path, 'report', now + 'report.html')
    # print('==========', filename)
    filename = os.path.join('./', 'report', now + 'report.html')
    with open(filename, 'wb') as wf:
        # 定义测试报告
        runner = HTMLTestRunner(
            stream=wf,
            title="get post HTMLTestRunner",
            description="description"
        )
        runner.run(suite)


# run_discover.py
"""使用discover调用oop的get和post请求"""
import unittest
# 测试用例存放路径
case_path = './cases'
discover = unittest.defaultTestLoader.discover(case_path, pattern="test*.py")
suite = unittest.TestSuite()
runner = unittest.TextTestRunner()
runner.run(discover)


# run_discover_htmltestrunner.py
"""使用discover调用oop的get和post请求"""
import os
import sys
import time
import unittest
from HTMLTestRunner import HTMLTestRunner


# 测试用例存放路径
case_path = './cases'
discover = unittest.defaultTestLoader.discover(case_path, pattern="test*.py")
suite = unittest.TestSuite()

now = time.strftime("%Y-%m-%d %H-%M-%S")
# public_path = os.path.dirname(os.path.abspath(sys.argv[0]))  # 获取当前运行的.py文件所在的绝对路径
# filename = os.path.join(public_path, 'report', now + 'report.html')
# print('==========', filename)

filename = os.path.join('./', 'report', now + 'report.html')

with open(filename, 'wb') as wf:
    # 定义测试报告
    runner = HTMLTestRunner(
    stream=wf,
    title="get post HTMLTestRunner",
    description="description"
    )
    runner.run(discover)

```

