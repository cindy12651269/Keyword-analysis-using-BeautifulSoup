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
import requests
from bs4 import BeautifulSoup

# Send a request to the API source using requests
response = requests.get('https://udn.com/news/breaknews/1')
soup = BeautifulSoup(response.text, 'html.parser')

news = []

#Install jieba Chinese word segmentation package
!pip install jieba

#Download the official dictionary file
!wget https://raw.githubusercontent.com/fxsjy/jieba/master/extra_dict/dict.txt.big

#Import the package and load the dictionary file
import jieba
jieba.load_userdict("dict.txt.big")

#Tokenization in precise mode
tokens=[]
for d in news:
  token = list(jieba.cut(d, HMM=False)) #Tokenization result of string d
  tokens.append(token)
word_count = {}
for word in tokens:
    for num in word:
        if num not in word_count:
            word_count[num]=1
        else:
            word_count[num]+=1
 #Calculate the frequency of each word in the tokenized results
print(word_count)

word_count = dict(sorted(word_count.items(), key=lambda item: item[1], reverse=True))
# Sort by frequency from highest to lowest
print(word_count)
