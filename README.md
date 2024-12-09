# Google Web Scraping

This project demonstrates web scraping of Google search results using Python and BeautifulSoup.

## Requirements

- Python 3.x
- Install required libraries:

    ```bash
    pip install beautifulsoup4 requests pandas
    ```

## Usage

1. Clone the repository:

    ```bash
    git clone https://github.com/yourusername/google-web-scraping.git
    cd google-web-scraping
    ```

2. Scrape Google search results:

    ```python
    from bs4 import BeautifulSoup
    import requests
    import pandas as pd
    from pandas import Series, DataFrame

    # Define the search query and number of results
    query = "Web scraping with Python"
    num_results = 10

    # Perform Google search and parse results
    url = f"https://www.google.com/search?q={query}&num={num_results}"
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')

    # Extract titles, URLs, and snippets
    results = []
    for item in soup.find_all('h3'):
        title = item.text
        url = item.find_parent('a')['href']
        snippet = item.find_parent('div').find_next('div').text
        results.append({'title': title, 'url': url, 'snippet': snippet})

    # Display results
    for result in results:
        print(result)
    
    # Save to CSV
    df = pd.DataFrame(results)
    df.to_csv('google_results.csv', index=False)
    ```

## License

This project is licensed under the MIT License.
