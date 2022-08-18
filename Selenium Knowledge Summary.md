# Selenium Knowledge Summary



## 第一部分 hello world

```python
import time
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("http://www.baidu.com")
time.sleep(3)
driver.maximize_window()
time.sleep(3)
driver.quit()

```

## 第二部分 bases

```python
#########
# base.py
from selenium.webdriver.support.wait import WebDriverWait

class Base:
    def __init__(self, driver):
        self.driver = driver

    # 查找元素
    def base_find_element(self, loc, timeout=30, poll=0.5):
        return WebDriverWait(self.driver,
                             timeout=timeout,
                             poll_frequency=0.5).until(lambda x: x.find_element(*loc))
    
    # 点击方法
    def base_click(self, loc):
        self.base_find_element(loc).click()

    # 获取结果
    def base_get_value(self, loc):
        return self.base_find_element(loc).get_attribute("value")

    # 截图
    def base_get_image(self):
        return self.driver.get_screenshot_as_file("../image/fail.png")

    # 判断元素是否找到
    def base_element_exist(self, loc):
        try:
            self.base_find_element(loc)
            return True
        except:
            return False

########        
# get_driver.py
from selenium import webdriver
from chapter05.calculate import pages


class GetDriver:
    driver = None
    @classmethod
    def get_driver(cls):
        if cls.driver is None:
            cls.driver = webdriver.Chrome()
            cls.driver.maximize_window()
            cls.driver.get(pages.url)

        return cls.driver

    @classmethod
    def quit_driver(cls):
        if cls.driver:
            cls.driver.quit()
            cls.driver = None
```

## 第三部分 cases

```python
########
# test_calc_add.py
import unittest
from parameterized import parameterized
from chapter05.calculate.bases.get_driver import GetDriver
from chapter05.calculate.pages.page_calc import PageCalc
from chapter05.calculate.tools.read_json import read_json


def get_data():
    datas = read_json("calc.json")
    print(datas)
    print(type(datas))
    arrs = []
    for data in datas.values():
        print(data)
        print(type(data))
        arrs.append((data['a'], data['b'], data['expect']))

    return arrs


class TestCalcAdd(unittest.TestCase):

    driver = None
    @classmethod
    def setUpClass(cls) -> None:
        cls.driver = GetDriver().get_driver()
        cls.calc = PageCalc(cls.driver)

    @classmethod
    def tearDownClass(cls) -> None:
        GetDriver.quit_driver()

    def tearDown(self) -> None:
        self.calc.page_click_clear()

    @parameterized.expand(get_data())
    def test_calc_add(self, a, b, expect_result):
        self.calc.page_calc_add(a, b)
        result = self.calc.page_get_value()
        # 断言
        try:
            self.assertEqual(str(expect_result), result)
        except AssertionError:
            self.calc.base_get_image()
            raise

```

## 第四部分 data

```json
########
# calc.json
{
  "calc_001": {"a": 101, "b": 202, "expect": 333},
  "calc_002": {"a": 111, "b": 222, "expect": 333},
  "calc_003": {"a": 1, "b": 2, "expect": 3},
  "calc_004": {"a": 1111, "b": 1222, "expect": 2333}
}

########
#tmp.txt
111, 222, 333
101, 202, 303
1, 2, 3
1111, 1222, 2333
```

## 第五部分 image

## 第六部分 pages

```python
########
# page_calc.py
from selenium.webdriver.common.by import By
from chapter05.calculate.bases.base import Base
from chapter05.calculate import pages


class PageCalc(Base):
    def page_click_num(self, num):
        for n in str(num):
            loc = (By.CSS_SELECTOR, "#simple{}".format(n))
            self.base_click(loc)

    def page_click_add(self):
        self.base_click(pages.calc_add)

    def page_click_eq(self):
        self.base_click(pages.calc_eq)

    def page_get_value(self):
        return self.base_get_value(pages.calc_result)

    def page_click_clear(self):
        self.base_click(pages.calc_clear)

    def page_get_image(self):
        return self.base_get_image()

    def page_is_login_success(self):
        return self.base_element_exist(pages.calc_add)

    def page_calc_add(self, a, b):
        self.page_click_num(a)
        self.page_click_add()
        self.page_click_num(b)
        self.page_click_eq()

```

## 第七部分 reports

## 第八部分 scripts

```python
########
# run_main.py

import unittest
from HTMLTestRunner import HTMLTestRunner

suite = unittest.defaultTestLoader.discover("../cases")

with open("../reports/report.html", "wb") as f:
    HTMLTestRunner(stream=f, verbosity=2, title="private title",
                   description="private desc").run(suite)

# with open("../report/report.txt", "w", encoding="utf-8") as f:
#     unittest.TextTestRunner(stream=f, verbosity=2).run(suite)

```

第九部分 tools

```python
########
# read_json.py
import json


def read_json(filename):

    file_path = "../data/" + filename
    with open(file_path, "r", encoding="utf-8") as f:
        return json.load(f)

########
# read_txt.py

def read_txt(filename):
    file_path = "../data/" + filename
    with open(file_path, "r", encoding="utf-8") as f:
        return f.readlines()

```



