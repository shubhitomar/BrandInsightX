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

   ### - **Steps Taken:**

   **Imported Required Libraries in Python:**
   
```!pip install nltk```

```!pip install pandas```

```import requests
from bs4 import BeautifulSoup
```
 
   **Attempted to Scrape Data using Python:**

```
# Connecting to the website

URL = 'https://www.amazon.in/gp/aw/d/B0CMDTNB9P/?_encoding=UTF8&pd_rd_plhdr=t&aaxitk=1d0c45f61c45e81f8a92c016b4cc8062&hsa_cr_id=0&qid=1723127243&sr=1-1-e0fa1fdd-d857-4087-adda-5bd576b25987&ref_=sbx_be_s_sparkle_lsi4d_asin_0_price&pd_rd_w=KljCJ&content-id=amzn1.sym.df9fe057-524b-4172-ac34-9a1b3c4e647d%3Aamzn1.sym.df9fe057-524b-4172-ac34-9a1b3c4e647d&pf_rd_p=df9fe057-524b-4172-ac34-9a1b3c4e647d&pf_rd_r=1ZZF8R8DY69VY73N4DF5&pd_rd_wg=7Hl0A&pd_rd_r=a9c6b55f-311d-4706-b7cf-acf69aa1779b'

headers = {
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
    "Accept-Encoding": "gzip, deflate, br, zstd",
    "Accept-Language": "en-US,en;q=0.9,hi;q=0.8",
    "Dnt": "1",
    "Host": "www.amazon.in",
    "Priority": "u=0, i",
    "Referer": "https://www.youtube.com/",
    "Sec-Ch-Ua": "\"Not)A;Brand\";v=\"99\", \"Google Chrome\";v=\"127\", \"Chromium\";v=\"127\"",
    "Sec-Ch-Ua-Mobile": "?0",
    "Sec-Ch-Ua-Platform": "\"Windows\"",
    "Sec-Fetch-Dest": "document",
    "Sec-Fetch-Mode": "navigate",
    "Sec-Fetch-Site": "cross-site",
    "Sec-Fetch-User": "?1",
    "Upgrade-Insecure-Requests": "1",
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36",
    "X-Amzn-Trace-Id": "Root=1-66b4d8cc-22162f4a0c03e60a11711d6a"
}

# Get the page content
page = requests.get(URL, headers=headers)

# Parse the page with BeautifulSoup
soup = BeautifulSoup(page.content, "html.parser")

# Find all review elements by their data-hook attribute
reviews = soup.find_all(attrs={"data-hook": "review"})

# Extract and print the relevant content of each review
for review in reviews:
    review_title = review.find(attrs={"data-hook": "review-title"}).get_text(strip=True)
    review_body = review.find(attrs={"data-hook": "review-body"}).get_text(strip=True)
    
    print(f"Title: {review_title}")
    print(f"Review: {review_body}\n")
```

### - **Problems Encountered:**

  **No reviews found:** The script was unable to locate review blocks.

- **Solutions:**
 
     **Adjusted Scraping Logic:**
      Ensured the HTML structure was correctly parsed and used accurate tags/attributes for review extraction.



## **2. Pagination and Advanced Scraping**
   
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



## **3. Review Extraction and Saving**
   
  - **Objective:**
         Extract reviews and save them to an Excel file.

  - **Steps Taken:**

       **Installed library**
    
    ```pip install openpyxl```

    **Scraped Reviews:**

```reviews = []
for review in soup.find_all('div', {'data-hook': 'review'}):
    title = review.find('a', {'data-hook': 'review-title'}).get_text(strip=True)
    body = review.find('span', {'data-hook': 'review-body'}).get_text(strip=True)
    rating = review.find('i', {'data-hook': 'review-star-rating'}).get_text(strip=True)
    reviews.append({
        'Title': title,
        'Rating': rating,
        'Body': body
    })
```

  **Converted to DataFrame :**

   ```   df = pd.DataFrame(reviews)     ```

  **Exported to Excel:**
  
   ```   df.to_excel('amazon_reviews.xlsx', index=False)     ```

   - **Problems Encountered:**

       **Incorrect Attribute Names:** Errors in attribute names while scraping.
  
       **File Encoding Issue:** Errors when saving the Excel file.

  - **Solutions:**

       **Correct Attribute Names:** Ensured correct attribute names for review extraction.
  
       **Saved Correctly:** Verified the file is saved correctly and opened using Excel.



## **4. Final Adjustments**
   
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

```df = pd.DataFrame(reviews)
   df.to_excel('amazon_reviews.xlsx', index=False)
```

## Summary:
This stage of the project involved web scraping, handling data pagination, and exporting data to an Excel file for all products available from the brand on different platforms. The journey included troubleshooting path issues, handling data extraction errors, and ensuring correct file-saving procedures.

