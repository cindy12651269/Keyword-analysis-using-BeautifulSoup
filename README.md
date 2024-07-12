# Keyword-analysis-using-BeautifulSoup
This Python script demonstrates how to scrape news articles from a website using requests and BeautifulSoup libraries. The script begins by sending a GET request to the URL 'https://udn.com/news/breaknews/1' using requests. It then parses the HTML content of the response using BeautifulSoup.

## Sample Code

```python
import requests
from bs4 import BeautifulSoup

# Send a request to the API source using requests
response = requests.get('https://udn.com/news/breaknews/1')
soup = BeautifulSoup(response.text, 'html.parser')

news = []

# Extract news content for the first 4 articles
for link in soup.find_all('h3', class_='rounded-thumb__title')[:4]:
    # Get the URL of each news article
    news_url = link.a['href']
    
    # Send a request to the news article URL
    news_response = requests.get('https://udn.com' + news_url)
    
    # Parse the HTML content of the news article
    news_soup = BeautifulSoup(news_response.text, 'html.parser')
    
    # Find the content of the news article
    news_content = news_soup.find('div', class_='article-content__paragraph').text.strip().replace('\n', ' ')
    
    # Append the news content to the list
    news.append(news_content)

print(news)
