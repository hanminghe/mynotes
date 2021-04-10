http://chromedriver.storage.googleapis.com/index.html



download  the correspondent  version of chromdriver. 

first check  the version of chrome in your machine, by clicking  three dots in your chrome browser, and help> about Google Chrome.

my chrome says it's 89.0.4389.114

go to the above website and downloaded 89.0.4389.23 version of chromedriver_win32.zip. make sure major release number math with your chrome version.

after download, unzip the file and put chromedriver.exe to your chrome application directory. 

my chrome is under "C:\Program Files\Google\Chrome\Application". you can check the location by right clicking chrome icon in your desktop, and click the bottom one(properties), and open file location from pop up window.

after put chromedriver.exe file into the location mine looks like this.

![image-20210410124030710](https://github.com/hanminghe/mynotes/blob/master/imgs/image-20210410124030710.png)

```python
from selenium import webdriver
import time

driver=webdriver.Chrome(r"C:\Program Files\Google\Chrome\Application\chromedriver.exe")

driver.get("https://www.google.com/maps/")
time.sleep(2)



def find_business_name(addr):

        input_addr = driver.find_elements_by_id("searchboxinput")
        input_addr[0].click()

        input_addr[0].send_keys(addr)


        search_button =  driver.find_elements_by_id("searchbox-searchbutton")

        search_button[0].click()
        time.sleep(3)

        xpath="//*[@id=\"pane\"]/div/div[1]/div/div"
        business_name_xpath=driver.find_element_by_xpath(xpath)

        business_names = business_name_xpath.text.split("\n")
        found_name = ''
        space_removed = [i.strip() for i in business_names]
        # print(space_removed)
        if 'At this place' in space_removed:
            at_this_place = space_removed.index('At this place')
            found_name = space_removed[at_this_place +1]
        return found_name

search_addr = "5240 Turney Rd, Garfield Heights, OH"

print(find_business_name(search_addr))

```

