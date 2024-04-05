## Error Message 
```
AttributeError: 'WebDriver' object has no attribute 'find_element_by_xpath'
```

## Reason
Selenium just removed that method in version 4.3.0

```
Selenium 4.3.0
* Deprecated find_element_by_* and find_elements_by_* are now removed (#10712)
* Deprecated Opera support has been removed (#10630)
* Fully upgraded from python 2x to 3.7 syntax and features (#10647)
* Added a devtools version fallback mechanism to look for an older version when mismatch occurs (#10749)
* Better support for co-operative multi inheritance by utilising super() throughout
* Improved type hints throughout
```

## Solution 
Use New Methond
```
from selenium.webdriver.common.by import By

driver.find_element(by=By.XPATH, value='//<your xpath>')
```

## Source
https://stackoverflow.com/q/72754651/9819140
