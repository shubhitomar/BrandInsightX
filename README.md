# BrandInsightX

## Table of contents
- [Project overview](#project-overview)
- [Data Collection](#data-collection)
- [Making the dataset](#making-a-dataset)

  
### Project Overview
---
BrandInsightX offers an in-depth analysis of customer feedback for a retail store chain across online platforms using advanced data aggregation and NLP. It evaluates product performance, service quality, delivery, packaging, and pricing. The insights drive operational efficiency and customer experience improvements, enhancing market positioning and business growth.

- **Objective**: This project goes beyond conventional sentiment analysis by delving into detailed reviews across various platforms to assess specific aspects of customer experience. 

- **Research**: I began by identifying key platforms where the store is active, including Amazon, Flipkart, Dunzo, Google Maps, and the store’s website. 

- **Data Collection**: Employing sophisticated web scraping techniques, I gathered and integrated reviews from these sources to build a rich dataset.

- **Analysis Focus**: Unlike basic sentiment analysis, this project evaluates product performance, in-store service, delivery efficiency, packaging quality, and pricing strategies. By analyzing these factors, BrandInsightX aims to provide actionable insights that enhance operational efficiency, improve customer satisfaction, and strategically position the store in the market.

- **Goal**: The aim is to deliver a comprehensive understanding of consumer behavior and preferences, enabling the retail chain to make informed decisions that drive business growth and optimize overall customer experience.



# Data Collection 
---
Scraped and analyzed reviews for each product available from the store on different platforms, extracted the reviews, and saved them in a structured format using Python.

## **1. Initial Setup and Problem Encountered**

  ### - **Objective:** 
  Extract reviews from an Amazon product page.

   ### - **Steps Taken:**

   **Imported Required Libraries in Python:**
   
```!pip install nltk```

```!pip install pandas```

```
import requests
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

```
reviews = []

for review in soup.find_all('div', {'data-hook': 'review'}):
    title = review.find('a', {'data-hook': 'review-title'}).get_text(strip=True)
    body = review.find('span', {'data-hook': 'review-body'}).get_text(strip=True)
    rating = review.find('i', {'data-hook': 'review-star-rating'}).get_text(strip=True)
    reviews.append({
        'Title': title,
        'Rating': rating,
        'Body': body
    })

# Check if any reviews were found and print them
if reviews:
    for review in reviews:
        print(f"Title: {review['Title']}\nRating: {review['Rating']}\nBody: {review['Body']}\n")
else:
    print("No reviews found.")

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

---

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



|Heading1|Heading2|
|--------|--------|
|Column1|Column2|
|Python|Sql|

`column1`

**bold**

*italic*


# Making a dataset 
---

**Data Preparation Stage**

1. **Data Collection and Integration**:
   - **Source Identification**: Collected data from multiple platforms, including Google Maps, Amazon, and Flipkart.
   - **File Aggregation**: Merged data files from these platforms into a single dataset. The data was in various formats such as CSV and Excel, which were unified into a single format for consistency.

2. **Data Cleaning**:
   - **Column and Row Removal**: Removed irrelevant columns and rows that did not contribute to the analysis. This included columns with extraneous information or metadata and rows with incomplete or irrelevant data.
   - **Column Adjustment**: Reorganized and adjusted columns to ensure consistency across the dataset. This included renaming columns for uniformity, standardizing column formats (e.g., date formats, numerical values), and ensuring that all necessary columns for analysis were present.

3. **Handling Null Values**:
   - **Identification**: Identified columns and rows with missing values.
   - **Treatment**: Applied appropriate techniques to handle null values:
     - **Removal**: Deleted rows with excessive missing values that could not be imputed reliably, ensuring the dataset remained robust and meaningful.

4. **Data Validation**:
   - **Consistency Check**: Verified that data merged from different sources was coherent and accurately represented. Checked for discrepancies or anomalies that could impact the analysis.
   - **Quality Assurance**: Conducted a thorough review to ensure the dataset was clean, complete, and ready for analysis. This involved cross-referencing with the original data sources to confirm accuracy.

6. **Final Dataset Preparation**:
   - **Consolidation**: Created a final, consolidated dataset that included all the necessary data points for analysis.
   - **Export**: Exported the prepared dataset into a suitable format for further analysis, ensuring compatibility with jupyter notebook.

---


# Data Preprocessing and Analysis

**Libraries and Frameworks Used:**
- **pandas**: For data manipulation and analysis.
- **numpy**: For numerical computations.
- **scikit-learn**: For implementing machine learning algorithms,
  particularly LatentDirichletAllocation (LDA) for topic modeling.
- **TextBlob**: For sentiment analysis.
- **matplotlib**: For data visualization.

**Steps Involved:**

1. **Data Preprocessing:**
   - **Data Loading:** Loaded the combined dataset from the `review.xlsx` file that consolidated data scraped from various platforms such as Google Maps, Amazon, and Flipkart.
   - **Data Cleaning:** Removed unnecessary columns and rows that did not contribute to the analysis. Adjusted the required columns to ensure consistency across the dataset.

2. **Topic Modeling:**
   - **Vectorization:** Converted the textual data into a numerical format using `CountVectorizer` from `sklearn`, which allowed for the transformation of text into a document-term matrix (DTM).
     
  ```from sklearn.feature_extraction.text import CountVectorizer
vectorizer = CountVectorizer(max_df=0.9, min_df=2, stop_words='english')
dtm = vectorizer.fit_transform(df['cleaned_reviews'])
```

   - **Latent Dirichlet Allocation (LDA):** Applied the LDA algorithm to the DTM to identify underlying topics within the reviews. The number of topics was determined based on coherence scores, and a final set of 5 topics was chosen for clarity and interpretability.

```# Applying LDA for Topic Modeling
from sklearn.decomposition import LatentDirichletAllocation
# Number of topics
n_topics = 5
# Initialize LDA model
lda = LatentDirichletAllocation(n_components=n_topics, random_state=42)
lda.fit(dtm)
# Extract topics and their corresponding words
for i, topic in enumerate(lda.components_):
    print(f"Top 10 words for topic #{i}:")
    print([vectorizer.get_feature_names_out()[index] for index in topic.argsort()[-10:]])
    print("\n")
```
   - **Topic Assignment:** Each review was assigned a dominant topic based on the LDA output, helping to categorize the reviews according to the main themes discussed.
```
topic_values = lda.transform(dtm)
df['dominant_topic'] = topic_values.argmax(axis=1)
```

 - **Displaying top words using scikit-learn and manually validating their coherence:**:

```
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.decomposition import LatentDirichletAllocation

# Assuming 'cleaned_reviews' is your preprocessed text data
vectorizer = CountVectorizer()
dtm = vectorizer.fit_transform(df['cleaned_reviews'])
feature_names = vectorizer.get_feature_names_out()

# Train LDA model
lda_model = LatentDirichletAllocation(n_components=5, random_state=0)
lda_model.fit(dtm)

# Function to display top words
def display_top_words(model, feature_names, n_top_words=10):
    for topic_idx, topic in enumerate(model.components_):
        top_words_idx = topic.argsort()[-n_top_words:][::-1]
        top_words = [feature_names[i] for i in top_words_idx]
        print(f"Topic #{topic_idx + 1}: {' '.join(top_words)}")
display_top_words(lda_model, feature_names)
```

 - **Plotted the bar graph:**
The chart highlights which topics are most frequently discussed in the customer reviews. For example, the bar for "Customer Service and Atmosphere" is higher than others, it indicates that this topic is a major area of focus for customers.

![Screenshot 2024-08-14 191231](https://github.com/user-attachments/assets/abdab9d1-3f45-454f-9cb2-293c9c44c7ab)
   

3. **Sentiment Analysis:**
   - **Sentiment Scoring:** Used TextBlob to perform sentiment analysis on the reviews, generating sentiment scores that reflect the polarity of each review (ranging from negative to positive).
   - **Sentiment Distribution:** Analyzed the distribution of sentiment scores across the identified topics to understand how different aspects of the store's services, products, and overall experience were perceived by customers.

This stage of the project provided a comprehensive understanding of the main themes in customer feedback and the associated sentiment, setting the stage for deeper analysis and actionable insights.











