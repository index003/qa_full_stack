# Appium Knowledge Summary



## 第一部分 hello

```python
#########
# hello.py
from appium import webdriver
import time

desired_caps = dict()
desired_caps['platformName'] = 'Android'
desired_caps['platformVersion'] = '5'
desired_caps['deviceName'] = '192.168.157.102:5555'
desired_caps['unicodeKeyboard'] = True
desired_caps['resetKeyboard'] = True

desired_caps['appPackage'] = 'com.android.settings'
desired_caps['appActivity'] = '.Settings'

driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)
time.sleep(5)
print(driver.current_package)
print(driver.current_activity)

driver.start_activity('com.android.mms', '.ui.ConversationList')
time.sleep(5)
print(driver.current_package)
print(driver.current_activity)

driver.background_app(5)

# if driver.is_app_installed('cn.goapk.market'):
#     driver.remove_app('cn.goapk.market')
# else:
#     driver.install_app('D:\\Download\\anzhishichang.apk')

driver.quit()

```

## 第二部分 find element

```python
########
# get_element.py
from appium import webdriver
import time

from selenium.webdriver.common.by import By

desired_caps = dict()
desired_caps['platformName'] = 'Android'
desired_caps['platformVersion'] = '5'
desired_caps['deviceName'] = '192.168.157.102:5555'
desired_caps['unicodeKeyboard'] = True
desired_caps['resetKeyboard'] = True

desired_caps['appPackage'] = 'com.android.settings'
desired_caps['appActivity'] = '.Settings'

driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)
time.sleep(3)

search_button = driver.find_element(By.ID, 'com.android.settings:id/search')
search_button.click()
time.sleep(3)

search_input = driver.find_element(By.CLASS_NAME, 'android.widget.EditText')
search_input.send_keys('hello')
time.sleep(3)
search_input.clear()

search_back = driver.find_element(By.XPATH, "//*[@content-desc='Collapse']")
print(search_back.location)
print(search_back.size)
search_back.click()
time.sleep(3)

driver.quit()

########
# get_elements.py
from appium import webdriver
import time

from appium.webdriver.common.touch_action import TouchAction
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait
from appium.webdriver.connectiontype import ConnectionType

desired_caps = dict()
desired_caps['platformName'] = 'Android'
desired_caps['platformVersion'] = '5'
desired_caps['deviceName'] = '192.168.157.102:5555'
desired_caps['unicodeKeyboard'] = True
desired_caps['resetKeyboard'] = True

desired_caps['appPackage'] = 'com.android.settings'
desired_caps['appActivity'] = '.Settings'

driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)

time.sleep(3)
driver.open_notifications()
time.sleep(3)
driver.press_keycode(4)
time.sleep(3)
driver.press_keycode(24)
time.sleep(3)
driver.press_keycode(24)
time.sleep(3)
driver.press_keycode(24)
time.sleep(3)
# driver.press_keycode(4)
time.sleep(3)
driver.press_keycode(25)
time.sleep(3)
driver.press_keycode(25)

time.sleep(3)
x = driver.get_window_size()['width']
y = driver.get_window_size()['height']
z = driver.get_window_size()
print(x)
print(y)
print(z)
time.sleep(3)
driver.get_screenshot_as_file("screen.png")
time.sleep(3)

# 隐式等待,针对全局元素
driver.implicitly_wait(10)

print("start swipe ....")
driver.swipe(100, 600, 100, 200, 2000)
time.sleep(2)
driver.swipe(100, 200, 100, 600, 2000)
print("start end ....")

titles = driver.find_elements(By.ID, 'com.android.settings:id/title')

print(titles)
print(len(titles))

for title in titles:
    print("==============================")
    print(title.text)
    print(title.get_attribute("enabled"))
    print(title.get_attribute("clickable"))
    print(title.get_attribute("text"))
    print(title.get_attribute("resource-id"))
    print(title.get_attribute("class"))
    print("==============================")

# time.sleep(2)
# driver.scroll(titles[1], titles[3])
# time.sleep(2)
# driver.scroll(titles[3], titles[1])

# time.sleep(2)
# driver.drag_and_drop(titles[1], titles[3])
# time.sleep(2)
# driver.drag_and_drop(titles[3], titles[1])
time.sleep(2)

titles[1].click()
time.sleep(3)

# 显式等待,针对单个元素
# wait = WebDriverWait(driver, 5)
# more_back = wait.until(lambda x: x.By.CLASS_NAME, 'android.widget.ImageButton')
more_back = driver.find_element(By.CLASS_NAME, 'android.widget.ImageButton')

# 轻敲
# TouchAction(driver).tap(more_back).perform()
# 按下，松开
TouchAction(driver).press().release().perform()
# more_back.click()
time.sleep(3)

textviews = driver.find_elements(By.CLASS_NAME, 'android.widget.TextView')

print(textviews)
print(len(textviews))

for textview in textviews:
    print(textview.text)
time.sleep(3)

eles = driver.find_elements(By.XPATH, "//*[contains(@text, 'o')]")

print(len(eles))

for ele in eles:
    print(ele.text)

driver.quit()
```

## 第三部分 base

```python
########
# base_page.py
class BasePage:

    def __init__(self, driver):
        self.driver = driver

    # 元素定位
    def locator(self, loc):
        return self.driver.find_element(*loc)

    # 输入
    def input(self, loc, value):
        self.locator(loc).send_keys(value)

    # 点击
    def click(self, loc):
        self.locator(loc).click()

    # 滑动（上下左右）滑动
    def swipe(self, start_x_rate, start_y_rate, end_x_rate, end_y_rate, duration=2000):
        # 获取屏幕尺寸
        window_size = self.driver.get_window_size()
        x = window_size['width']
        y = window_size['height']
        self.driver.swipe(
            start_x=x * start_x_rate,
            start_y=y * start_y_rate,
            end_x=x * end_x_rate,
            end_y=y * end_y_rate,
            duration=duration
        )

```

## 第四部分 config

```yaml
########
# config.yaml
desired_caps:
  platformName: Android
  platformVersion: 5
  deviceName: 192.168.157.102:5555
  unicodeKeyboard: True
  resetKeyboard: True
  appPackage: com.android.settings
  appActivity: .Settings
```

## 第五部分 data

## 第六部分 pageobjects

```python
########
# login_page.py
from base.base_page import BasePage
from appium.webdriver.common.mobileby import MobileBy


class LoginPage(BasePage):

    ele_more = (MobileBy.ID, "aaa")

    def login(self):
        self.click(self.ele_more)
        self.input(self.ele_more)

```

## 第七部分 testcases

```python
########
# test_login.py
from appium.webdriver import webdriver
from pageobjects.login_page import LoginPage
import pytest


class TestLogin:

    def setup(self):
        desired_caps = dict()
        desired_caps['platformName'] = 'Android'
        desired_caps['platformVersion'] = '5'
        desired_caps['deviceName'] = '192.168.157.102:5555'
        desired_caps['unicodeKeyboard'] = True
        desired_caps['resetKeyboard'] = True

        desired_caps['appPackage'] = 'com.android.settings'
        desired_caps['appActivity'] = '.Settings'

        self.driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)

    def test_login(self):
        login_page = LoginPage(driver=self.driver)
        login_page.login()
        
if __name__ == '__main__':
    pytest.main()
```

