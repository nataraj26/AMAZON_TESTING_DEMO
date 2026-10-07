# Amazon Login, Search, Add to Cart and Checkout Automation

### PROGRAM CODE 
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Edge()
driver.maximize_window()

wait = WebDriverWait(driver, 20)

driver.get("https://www.amazon.in/")

print("Amazon opened")

driver.find_element(By.CLASS_NAME, "nav-line-1-container").click()

print("Login page opened")

phone = wait.until(
    EC.visibility_of_element_located((By.NAME, "email"))
)

phone.send_keys("9025445537")

print("Phone number entered")

driver.find_element(By.CLASS_NAME, "a-button-input").click()

print("Continue clicked")

time.sleep(3)

try:
    otp = WebDriverWait(driver, 5).until(
        EC.visibility_of_element_located((By.NAME, "code"))
    )

    print("OTP required")

    otp.send_keys(input("Enter OTP: "))

    driver.find_element(By.CLASS_NAME, "a-button-input").click()

    print("OTP submitted")

    time.sleep(5)

except:
    print("OTP not required")

search = wait.until(
    EC.visibility_of_element_located((By.ID, "twotabsearchtextbox"))
)

search.send_keys("Mens shirts")

driver.find_element(By.ID, "nav-search-submit-button").click()

print("Product searched")

time.sleep(5)

buttons = driver.find_elements(
    By.XPATH,
    '//button[@aria-label="Add to cart"]'
)

print("Add to cart buttons:", len(buttons))

for button in buttons:
    try:
        if button.is_displayed():
            driver.execute_script(
                "arguments[0].scrollIntoView();",
                button
            )
            time.sleep(1)
            button.click()
            print("Product added to cart")
            break
    except:
        pass

time.sleep(3)

driver.get("https://www.amazon.in/gp/cart/view.html")

print("Cart opened")

time.sleep(5)

print("Looking for checkout...")

elements = driver.find_elements(
    By.XPATH,
    "//*[contains(text(),'Proceed to checkout')]"
)

print("Checkout elements found:", len(elements))

for element in elements:
    try:
        if element.is_displayed():
            driver.execute_script(
                "arguments[0].scrollIntoView({block:'center'});",
                element
            )
            time.sleep(1)
            element.click()
            print("Checkout clicked")
            break
    except:
        pass

time.sleep(5)

print("Reached checkout/payment page")

input("Press Enter to close...")

driver.quit()
```
### output
<img width="1917" height="1012" alt="Screenshot 2026-10-06 144915" src="https://github.com/user-attachments/assets/215e509f-3848-4bd7-8665-81a5a4642a57" />

<img width="1917" height="1013" alt="Screenshot 2026-10-07 104557" src="https://github.com/user-attachments/assets/93c7006a-0e9a-4ed3-ae0a-4c4b70287535" />


<img width="1920" height="1020" alt="Screenshot 2026-10-06 145011" src="https://github.com/user-attachments/assets/1a52e9cf-1c3c-457f-b3ac-b8b5ec58022f" />

<img width="1915" height="907" alt="image" src="https://github.com/user-attachments/assets/1eaae080-0c39-4f6e-95fc-7e31f8f9bbaa" />


<img width="1920" height="1080" alt="Screenshot 2026-10-06 205637" src="https://github.com/user-attachments/assets/516df165-4b74-45db-b18d-b17257335a3c" />


<img width="1366" height="225" alt="Screenshot 2026-10-06 205801" src="https://github.com/user-attachments/assets/b6c6917a-6552-4de9-87fd-2260c8aa0ca5" />
