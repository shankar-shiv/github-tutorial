# github tutorial

Hello , this from branch 1. :)

Example python code

```python

#!/home/shankar/.pyenv/shims/python

# The Keys class provide keys in the keyboard like RETURN, F1, ALT etc.

import random
import time
from datetime import date, datetime, timedelta
import argparse
from selenium import webdriver
from selenium.webdriver import ActionChains
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.ui import Select, WebDriverWait

website_url = "https://temptaking.ado.sg/group/b24b3fa41017a5faab1d2a956962f724"
driver = webdriver.Chrome()
driver.get(website_url)

# get the command line arguments

parser = argparse.ArgumentParser()
parser.add_argument('-start_date', type=str, default="01112020",
help='Enter start date in ddmmyyyy format')
parser.add_argument('-end_date', type=str, default=date.today().strftime("%d%m%Y"),
help='Enter end date in ddmmyyyy format')
parser.add_argument('-member', type=str, default="W1 Shankar",
help='Enter you name as reflected in website, ex:W1 Shankar')
parser.add_argument('-pin_number', type=int, default=5555,
help='Enter your pin number')
args = parser.parse_args()

# CHANGE THESE PARAMETERS ONLY

# The format for start date and end date is ddmmyyyy.

# The pin number is a 4 digit number.

# Enter your member name as shown in the website.

start_date = args.start_date
end_date = args.end_date
member = args.member
pin_number = args.pin_number

# start_date = "01012020"

# end_date = "31052020"

# member = "W1 Shankar"

# pin_number = 5555

time_of_the_day = ["AM", "PM"]

'''This string represents the date January 31, 2020,
according to the ISO 8601 format.
You can create a date instance with the following example:
ex : date.fromisoformat("2020-01-31")'''

start_date_formatted = date.fromisoformat(
start_date[4:8] + "-" + start_date[2:4] + "-" + start_date[0:2])

end_date_formatted = date.fromisoformat(
end_date[4:8] + "-" + end_date[2:4] + "-" + end_date[0:2])

delta = (end_date_formatted - start_date_formatted)
number_of_days = delta.days
print("number_of_days={}".format(number_of_days+1))

def choose_date(start_date):
date_input_element = driver.find_element_by_id("date-input")
date_input_element.send_keys(start_date)

def choose_time_of_the_day(am_or_pm):
select_am_pm = Select(driver.find_element_by_id('meridies-input'))
options_am_pm = select_am_pm.options

    for option in options_am_pm:
        # print(option.get_attribute("value"))
        if (option.get_attribute("value") == am_or_pm):
            option.click()

def member_select(member):
select_member = Select(driver.find_element_by_id('member-select'))
options_member = select_member.options

    for option in options_member:
        # print(option)
        if (option.get_attribute("text") == member):
            option.click()

def enter_pin(pin_number):
driver.implicitly_wait(5)
pin_1_element = driver.find_element_by_id("ep1")
pin_1_element.clear()
pin_1_element.send_keys(pin_number)

def enter_temperature():
temperature_box_1_element = driver.find_element_by_id("td1")
temperature_box_1_element.clear()
temp = int(float("{:.1f}".format(random.uniform(36.1, 37.0))) \* 10) # print(temp)
temperature_box_1_element.send_keys(temp)

def submit():
submit_element = driver.find_element_by_xpath(
"/html/body/div[1]/div[2]/div[4]/button")
submit_element.send_keys(Keys.ENTER)

    driver.implicitly_wait(5)
    driver.switch_to.active_element
    submit_confirmation_element = driver.find_element_by_id("submit-temp-btn")
    submit_confirmation_element.send_keys(Keys.ENTER)

    # WebDriverWait(driver, 20).until(EC.element_to_be_clickable(
    #     (By.XPATH, "/html/body/div[4]/div/div/div[1]/button"))).click()
    # close_button = WebDriverWait(driver, 5).until(EC.presence_of_all_elements_located(
    #     (By.XPATH, "/html/body/div[4]/div/div/div[1]/button")))
    ActionChains(driver).click(
        driver.find_element_by_class_name("close")).perform()

def go_back_to_start():
driver.get(website_url)

num = 0
for num in range(number_of_days+1):
for foo in time_of_the_day:
choose_date((start_date_formatted +
timedelta(days=num)).strftime("%d%m%Y"))
choose_time_of_the_day(am_or_pm=foo)
member_select(member)
enter_pin(pin_number)
enter_temperature()
submit()
go_back_to_start()

# To be safe, we’ll first clear any pre-populated text in the input field

# (e.g. “Search”) so it doesn’t affect our search results:

# driver.close()
```
