# BrandInsightX
### Project Overview
BrandInsightX offers an in-depth analysis of customer feedback for a retail store chain across online platforms using advanced data aggregation and NLP. It evaluates product performance, service quality, delivery, packaging, and pricing. The insights drive operational efficiency and customer experience improvements, enhancing market positioning and business growth.

- **Objective**: This project goes beyond conventional sentiment analysis by delving into detailed reviews across various platforms to assess specific aspects of customer experience. 

- **Research**: I began by identifying key platforms where the store is active, including Amazon, Flipkart, Dunzo, Google Maps, and the store’s website. 

- **Data Collection**: Employing sophisticated web scraping techniques, I gathered and integrated reviews from these sources to build a rich dataset.

- **Analysis Focus**: Unlike basic sentiment analysis, this project evaluates product performance, in-store service, delivery efficiency, packaging quality, and pricing strategies. By analyzing these factors, BrandInsightX aims to provide actionable insights that enhance operational efficiency, improve customer satisfaction, and strategically position the store in the market.

- **Goal**: The aim is to deliver a comprehensive understanding of consumer behavior and preferences, enabling the retail chain to make informed decisions that drive business growth and optimize overall customer experience.



# Data Collection 

Scraped and analyzed reviews for each product available from the store on different platforms, extracted the reviews, and saved them in a structured format using Python.

## **1. Initial Setup and Problem Encountered**

  ### - **Objective:**
    Extract reviews from an Amazon product page.

   ###- **Steps Taken:**

   **Imported Required Libraries in Python:**

         ```import requests
            from bs4 import BeautifulSoup
         ```
 
   **Attempted to Scrape Data using Python:**

          ```URL = 'https://www.amazon.in/gp/aw/d/B0CMDTNB9P/'
             headers = { "User-Agent": "Mozilla/5.0 ..."}
             page = requests.get(URL, headers=headers)
             soup = BeautifulSoup(page.content, "html.parser")
             ```

### - **Problems Encountered:**

      **No reviews found:** The script was unable to locate review blocks.

- **Solutions:**
 
     **Adjusted Scraping Logic:**
      Ensured the HTML structure was correctly parsed and used accurate tags/attributes for review extraction.



**2. Pagination and Advanced Scraping**
   
   - **Objective:**
      Handle pagination to scrape reviews from multiple pages.

   - **Steps Taken:**

        **Selenium for Pagination:**

           ```from selenium import webdriver
           from selenium.webdriver.chrome.service import Service
           from selenium.webdriver.common.by import By
           from selenium.webdriver.chrome.options import Options
           ```
  
       **Configured Chrome WebDriver:**
           Downloaded chromedriver and set up the path.

  - **Problems Encountered:**

       **Driver Not Found / Path Issue:** The script couldn't find the ChromeDriver executable.

  - **Solutions:**

      **Download and Setup:**
          Downloaded chromedriver from ChromeDriver Downloads and set the correct path.



**3. Review Extraction and Saving**
   
  - **Objective:**
         Extract reviews and save them to an Excel file.

  - **Steps Taken:**

       **Scraped Reviews:**

           ```reviews = []
           for review in soup.find_all('div', {'data-hook': 'review'}):
           title = review.find('a', {'data-hook': 'review-title'}).text.strip()
           body = review.find('span', {'data-hook': 'review-body'}).text.strip()
           reviews.append({'Title': title, 'Body': body})
           ```

       **Converted to DataFrame and Saved to Excel:**

         ```import pandas as pd
         df = pd.DataFrame(reviews)
         df.to_excel('amazon_reviews.xlsx', index=False)```

  - **Problems Encountered:**

       **Incorrect Attribute Names:** Errors in attribute names while scraping.
  
       **File Encoding Issue:** Errors when saving the Excel file.

  - **Solutions:**

       **Correct Attribute Names:** Ensured correct attribute names for review extraction.
  
       **Saved Correctly:** Verified the file is saved correctly and opened using Excel.



**4. Final Adjustments**
   
  - **Objective:**
        Ensure the correct functionality and file handling.

  - **Steps Taken:**

       **Verified Functionality:**
        Ran scripts to ensure the data is correctly scraped and saved.

       **Handled File Errors:**
        Ensured the file is opened with appropriate software (Excel) to avoid encoding issues.

       **Final File Location:**
        The final Excel file was saved as amazon_reviews.xlsx in the specified directory.



# Commands Used:

## Scraping Data:

   ```import requests
    from bs4 import BeautifulSoup
    page = requests.get(URL, headers=headers)
    soup = BeautifulSoup(page.content, "html.parser")
```

## Handling Pagination with Selenium:

```from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
```

## Exporting Data to Excel:

```import pandas as pd
df = pd.DataFrame(reviews)
df.to_excel('amazon_reviews.xlsx', index=False)
```

## Summary:
This stage of the project involved web scraping, handling data pagination, and exporting data to an Excel file for all products available from the brand on different platforms. The journey included troubleshooting path issues, handling data extraction errors, and ensuring correct file-saving procedures.

