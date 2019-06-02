# Web Structure Mining

Abstrak:

Karena meningkatnya jumlah data yang tersedia secara online, World Wide Web telah menjadi salah satu sumber daya paling berharga untuk pengambilan informasi dan penemuan pengetahuan. Teknologi penambangan web adalah solusi yang tepat untuk penemuan pengetahuan di Web. Pengetahuan yang diekstraksi dari Web dapat digunakan untuk meningkatkan kinerja untuk pencarian informasi Web, menjawab pertanyaan, dan penyimpanan data berbasis web. Dalam makalah ini, kami menyediakan pengantar penambangan Web serta peninjauan kategori penambangan Web. Kemudian  fokus pada salah satu kategori ini: penambangan struktur Web. Dalam kategori ini, akan memperkenalkan penambangan tautan dan meninjau metode populer yang diterapkan dalam penambangan struktur Web: PageRank.

Web struncture mining dikenal juga  sebagai web log mining adalah teknik yang digunakan untuk menemukan struktur link dari hyperlink dan membangun rangkuman website dan halaman  web. Salah satu manfaatnya adlah untuk  menentukan pagerank pada suatu halaman web.

## Code

Berikut Kode Utama Untuk Melakukan Crawling, mengunakan library requests dan BeautifulSoup4 : 

``` python
def getAllLinks(src):
   
    try:
        page = requests.get(src)
        soup = BeautifulSoup(page.content, 'html.parser')
        tags = soup.findAll("a")

        links = []
        for tag in tags:
            try:
                link = tag['href']
                if not link in links and 'http' in link:
                    links.append(link)
            except KeyError:
                pass
        return links
    except:
        return list()
```

Program Di atas digunakan untuk mengambil semua link yang ada pada sebuah website pertama yang di crawl, 

Kemudian Untuk Mendapatkan crawling secara berulang , definisikan sebuah fungsi crawl :

``` python
def simplifiedURL(url):
    # cek 1 : www
    if "www." in url:
        ind = url.index("www.")+4
        url = "http://"+url[ind:]
    # cek 3 : tanda / di akhir
    if url[-1] == "/":
        url = url[:-1]
    # Cek 4 : cuma domain utama
    parts = url.split("/")
    url = ''
    for i in range(3):
        url += parts[i] + "/"
    return url

def crawl(url, max_deep,  show=False, deep=0, done=[]):
    global edgelist
    deep += 1
    url = simplifiedURL(url)
    if not url in done:
        links = getAllLinks(url)
        done.append(url)
        if show:
            if deep == 1:
                print(url)
            else:
                print("|", end="")
                for i in range(deep-1): print("--", end="")
                print(url)
            
        for link in links:
            link = simplifiedURL(link)
            edge = (url,link)
            if not edge in edgelist:
                edgelist.append(edge)
            if (deep != max_deep):
                crawl(link, max_deep, show, deep, done)
```

Method `simplifiedURL` berfungsi untuk menyamakan semua format url, menjadi `http://urlweb.com/`

Proses pemanggilan method di atas bisa dilakukan dengan cara berikut:

```python
import requests
import pandas as pd
from bs4 import BeautifulSoup

# Inisialisasi variabel

root = "https://www.liputan6.com/"
nodelist = [root]
edgelist = []

#crawl
crawl(root, 3, show=True)
edgelistFrame = pd.DataFrame(edgelist, None, ("From", "To"))
```

