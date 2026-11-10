# WDM-Ex-NO-8-Web-Scraping-On-e-commerce-platform-using-BeautifulSoup
**Web Scraping On E-commerce platform using BeautifulSoup**<br>
**NAME:Yoga varma B**<br>
**DATE:**<br>
**AIM:**<br>
To perform Web Scraping on Amazon using (beautifulsoup) Python.<br>
**Description:**<br>
Web scraping is the process of extracting data from various websites and parsing it. In other words, it’s a technique to extract unstructured data and store that data either in a local file or in a database. There are many ways to collect data that involve a huge amount of hard work and consume a lot of time. Web scraping can save programmers many hours. Beautiful Soup is a Python web scraping library that allows us to parse and scrape HTML and XML pages. One can search, navigate, and modify data using a parser. It’s versatile and saves a lot of time.
**The basic steps involved in web scraping are:**<br>

1) Loading the document (HTML content)

2) Parsing the document

3) Extraction

4) Transformation

**Procedure:**<br>
Import necessary libraries (requests, BeautifulSoup, re, matplotlib.pyplot).
Define convert_price_to_float(price) Function: to Remove non-numeric characters from a price string and convert it to a float.
Define get_amazon_products(search_query) Function: to Scrape Amazon for product information based on the search query.
Fetch and parse the HTML content then Extract product names and prices from the search results and Sort product information based on converted prices in ascending order.
Return sorted product data as a list of dictionaries.
Call get_amazon_products(search_query) to get product data based on the user's search query.
Check if products are found; if not, display "No products found."
Visualize Product Data using a Bar Chart<br>
**Program:**
```
import requests
from bs4 import BeautifulSoup
import matplotlib.pyplot as plt
import re

def convert_price_to_float(price):
    price = re.sub(r'[^\d.]', '', price)
    return float(price) if price else 0.0

def get_products():

    url = "https://books.toscrape.com/"
    response = requests.get(url)

    products_data = []

    if response.status_code == 200:

        soup = BeautifulSoup(response.content, 'html.parser')

        products = soup.find_all('article', class_='product_pod')

        for product in products:

            name = product.h3.a['title']
            price = product.find('p', class_='price_color').text

            products_data.append({
                'Product': name,
                'Price': price
            })

    else:
        print("Website error:", response.status_code)

    return sorted(
        products_data,
        key=lambda x: convert_price_to_float(x['Price'])
    )


products = get_products()

if products:

    for product in products:
        print(product['Product'], "-", product['Price'])

    names = [p['Product'][:30] for p in products]
    prices = [convert_price_to_float(p['Price']) for p in products]

    plt.figure(figsize=(12, 7))
    plt.barh(names, prices)
    plt.xlabel("Price (£)")
    plt.ylabel("Books")
    plt.title("Book Prices - Ascending Order")
    plt.tight_layout()
    plt.show()

else:
    print("No products found.")

```
**Output:**<br>
<img width="963" height="362" alt="image" src="https://github.com/user-attachments/assets/0464f92a-26b5-4462-974d-ac7f51c92e45" />

<img width="1061" height="555" alt="image" src="https://github.com/user-attachments/assets/dd2d30b8-5dff-4baf-b01f-66b4a3e7dbfc" />

**Result:**
Thus the Web Scraping On e-commerce platform using BeautifulSoup is executed successfully
