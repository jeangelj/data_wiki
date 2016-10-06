    !pip install xmltodict
    from bs4 import BeautifulSoup
    import requests
    import xmltodict
    import os
    import webbrowser

##requests + beautiful soup:

    def browse(soup):
        """ Browse current HTML. """
        if str(type(soup)) != "<class 'bs4.BeautifulSoup'>":
            soup = BeautifulSoup(soup.content, 'lxml')
        path = os.path.abspath('browse.html')
        url = 'file://' + path
        with open(path, 'w') as f:
            f.write(soup.encode('ascii','ignore'))
        return webbrowser.open(url)
    res = requests.get(url)
    res.text[:1000]
    soup = BeautifulSoup(res.text)

##Wikipedia tables:

    !pip install html5lib
    import html5lib
    import pandas as pd
    url ='https://en.wikipedia.org/wiki/XXX’
    tables = pd.read_html(url)

##requests:

    search_string = raw_input()
    headers = {'X-Requested-With': 'XMLHttpRequest'}
    data = {'searchRequestJson': #enter from website’}
    res = requests.post(url, data=data, headers=headers)
    result_dict = xmltodict.parse(res.text)
    df = pd.DataFrame(result_dict['result']['requisition'])
    df.head()
