
# Scrape Google News Using Python and Export Data to CSV

Access to real-time news search results is crucial for businesses to stay updated on the latest headlines and public sentiment surrounding their brand. By leveraging this data, companies can enhance their reputation, monitor media coverage, and gain a competitive edge in their market.

Python, one of the [most popular languages for web scraping](https://bit.ly/Scraperapi), allows users to build automated scrapers to extract valuable data from the internet for purposes such as **data analysis**, **SEO monitoring**, **news monitoring**, and more. In this guide, we'll show you how to scrape Google News using Python and extract data into a structured CSV file.

---

## Why Access Google News Data?

Accessing Google News data offers several advantages, including:

1. **Brand Monitoring**: Track how your brand is perceived in the media and spot potential issues early.
2. **Stay Informed**: Keep up-to-date on current events, political developments, and advancements in your industry.
3. **Market Research**: Analyze historical trends, consumer sentiment, and competitor strategies.
4. **Competitor Analysis**: Monitor your competitor’s latest developments and media campaigns to refine your own strategies.
5. **Public Awareness**: Use Google News data to create awareness on key topics such as economics, science, or politics.

---

## Methods to Scrape Google News

We'll discuss two ways to extract news from Google:

1. Using Python and **Beautiful Soup** for manual scraping.
2. Using the **ScraperAPI Google News API** for scalable and efficient scraping.

For large-scale scraping or avoiding issues like CAPTCHAs and IP blocks, **ScraperAPI's Google News API** is recommended. It handles these challenges by rotating millions of proxies and headers automatically, saving time and effort.

---

## Method 1: Scraping Google News Using Python

### Libraries You’ll Need
Before starting, ensure you’ve set up a Python environment and installed the required libraries. Import the following:

```python
import json
import requests
from bs4 import BeautifulSoup
```

### Writing the Script

Below is a function to scrape Google News results:

```python
def getNewsData():
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36"
    }
    response = requests.get(
        "https://www.google.com/search?q=amazon&gl=us&tbm=nws&num=100", headers=headers
    )
    soup = BeautifulSoup(response.content, "html.parser")
    news_results = []

    for el in soup.select("div.SoaBEf"):
        news_results.append(
            {
                "link": el.find("a")["href"],
                "title": el.select_one("div.MBeuO").get_text(),
                "snippet": el.select_one(".GI74Re").get_text(),
                "date": el.select_one(".LfVVr").get_text(),
                "source": el.select_one(".NUnG9d span").get_text(),
            }
        )

    # Save results to a JSON file or print them
    print(json.dumps(news_results, indent=2))

getNewsData()
```

This script fetches the first 100 news results for the search query `amazon`, extracting details such as the **headline**, **link**, **source**, **date**, and **description**.

---

### Exporting Data to a CSV File

To save the scraped data into a CSV file, add the following code:

```python
import csv

def saveToCSV(news_results):
    with open("news_data.csv", "w", newline="") as csv_file:
        fieldnames = ["link", "title", "snippet", "date", "source"]
        writer = csv.DictWriter(csv_file, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerows(news_results)

    print("Data saved to news_data.csv")
```

Run the function after scraping:

```python
news_results = getNewsData()
saveToCSV(news_results)
```

---

## Method 2: Using ScraperAPI’s Google News API

For faster and more scalable scraping, ScraperAPI offers a dedicated **Google News API**. This API simplifies the scraping process by delivering structured JSON responses without worrying about CAPTCHAs or HTML parsing.

### Steps to Get Started with ScraperAPI

1. **Sign Up and Get API Credentials**  
   - Register for a free trial on [ScraperAPI](https://bit.ly/Scraperapi). Use the code `SCRAPE9837861` to get started.
   - Once registered, copy your API key from the dashboard.

2. **Install Required Libraries**
   Install the necessary Python libraries for HTTP requests and JSON handling:
   ```bash
   pip install requests
   ```

3. **Write the API Request Code**
   Use your API key to fetch Google News data:

   ```python
   import requests

   def fetchNewsWithAPI():
       api_url = "https://api.scraperapi.com/?api_key=YOUR_API_KEY&url=https://www.google.com/search?q=amazon&tbm=nws"
       response = requests.get(api_url)
       data = response.json()
       print(data)
   ```

Replace `YOUR_API_KEY` with your actual ScraperAPI key.

4. **Save API Data to a CSV File**
   Modify the function to save API results into a CSV file:

   ```python
   def saveAPIResultsToCSV(data):
       with open("news_results.csv", "w", newline="") as csv_file:
           fieldnames = ["title", "snippet", "source", "date", "link"]
           writer = csv.DictWriter(csv_file, fieldnames=fieldnames)
           writer.writeheader()
           for news in data["news_results"]:
               writer.writerow({
                   "title": news["title"],
                   "snippet": news["snippet"],
                   "source": news["source"],
                   "date": news["lastUpdated"],
                   "link": news["url"]
               })
       print("Data saved to news_results.csv")
   ```

Run the API call and save the results:

```python
data = fetchNewsWithAPI()
saveAPIResultsToCSV(data)
```

---

## Why Use ScraperAPI?

ScraperAPI is the most efficient way to scrape data without hassle. It handles all complexities such as IP rotation, CAPTCHAs, and headers while delivering clean, structured data. 

- **Ease of Use**: No need to write complicated parsing code.
- **Scalable**: Supports large-scale data collection.
- **Reliable**: Access data from Amazon, Google, Walmart, and more.
- **Affordable**: Get started with the discount code `SCRAPE9837861`.

👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Conclusion

In this article, we explored two ways to scrape Google News: using Python’s Beautiful Soup library and using ScraperAPI’s Google News API. While manual scraping is flexible, APIs provide a faster, cleaner solution for large-scale data extraction. Whether you're monitoring your brand, tracking competitors, or conducting market research, these methods will help you access the data you need.

For hassle-free and scalable scraping, trust [ScraperAPI](https://bit.ly/Scraperapi) to handle all the heavy lifting.
