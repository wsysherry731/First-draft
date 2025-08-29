from selenium import webdriver
from selenium.webdriver.common.by import By
import time

# Set up the Chrome driver
driver = webdriver.Chrome()

# Open the target webpage
driver.get("https://admin.ozforex.com.au/home.asp")  # Replace with your target URL

# Wait for the page to load
time.sleep(15)

# Find the "OffSet Deal" header
header = driver.find_element(By.XPATH, "//td[text()='OffSet Deal']")

# Get the parent table or row
parent_row = header.find_element(By.XPATH, "./ancestor::tr")

# Find all deal rows after the header
deal_rows = parent_row.find_elements(By.XPATH, "following-sibling::tr")

# Click only the first 5 deals
for i in range(min(5, len(deal_rows))):  # Ensure we don't exceed the available deals
    deal = deal_rows[i].find_element(By.TAG_NAME, 'td')
    deal.click()
    time.sleep(1)  # Wait for 1 second between clicks

# Close the driver
driver.quit()
