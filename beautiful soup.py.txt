import requests
from bs4 import BeautifulSoup

# URL of the webpage you want to scrape
url = 'https://example.com/news'

# Send a GET request to the webpage
response = requests.get(url)

# Check if the request was successful
if response.status_code == 200:
    # Parse the content of the request with BeautifulSoup
    soup = BeautifulSoup(response.content, 'html.parser')

    # Find all article tags (assuming they are contained in <article> tags)
    articles = soup.find_all('article')

    # Loop through each article and extract the title and link
    for article in articles:
        # Extract the title (assuming it is contained in an <h2> tag)
        title_tag = article.find('h2')
        if title_tag:
            title = title_tag.get_text()

            # Extract the link (assuming it is contained in an <a> tag within the <h2> tag)
            link_tag = title_tag.find('a')
            if link_tag:
                link = link_tag['href']
                print(f'Title: {title}')
                print(f'Link: {link}')
                print('---')

else:
    print(f'Failed to retrieve the webpage. Status code: {response.status_code}')
