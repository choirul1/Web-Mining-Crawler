PageRank 

**PageRank** adalah sebuah [algoritme](https://id.wikipedia.org/wiki/Algoritme) yang telah dipatenkan yang berfungsi menentukan [situs web](https://id.wikipedia.org/wiki/Situs_web) mana yang lebih penting/populer. PageRank merupakan salah satu fitur utama [mesin pencari](https://id.wikipedia.org/wiki/Mesin_pencari) [Google](https://id.wikipedia.org/wiki/Google) dan diciptakan oleh pendirinya, [Larry Page](https://id.wikipedia.org/wiki/Larry_Page) dan [Sergey Brin](https://id.wikipedia.org/wiki/Sergey_Brin) yang merupakan mahasiswa Ph.D. [Universitas Stanford](https://id.wikipedia.org/wiki/Universitas_Stanford).



## Algoritma

Dari pendekatan yang sudah dijelaskan pada artikel konsep *pagerank*, Lawrence Page and Sergey Brin membuat algoritme *pagerank* seperti di bawah:

Algoritme awal



Salah satu algoritme lain yang dipublikasikan



- `PR(A)` adalah Pagerank halaman A
- `PR(T1)` adalah Pagerank halaman T1 yang mengacu ke halaman A
- `C(T1)` adalah jumlah link keluar (*outbound link*) pada halaman T1
- `d` adalah damping factor yang bisa diberi antara 0 dan 1.
- `N` adalah jumlah keseluruhan halaman web (yang terindeks oleh Google)

Dari algoritme di atas dapat dilihat bahwa pagerank ditentukan untuk setiap halaman anda bukan keseluruhan situs web. Pagerank sebuah halaman ditentukan dari pagerank halaman yang mengacu kepadanya yang juga menjalani proses penentuan pagerank dengan cara yang sama, jadi proses ini akan berulang sampai ditemukan hasil yang tepat.

Akan tetapi pagerank halaman A tidak langsung diberikan kepada halaman yang dituju, akan tetapi sebelumnya dibagi dengan jumlah link yang ada pada halaman T1 (outbound link), dan pagerank itu akan dibagi rata kepada setiap link yang ada pada halaman tersebut. Demikian juga dengan setiap halaman lain “Tn” yang mengacu ke halaman “A”.

Setelah semua pagerank yang didapat dari halaman-halaman lain yang mengacu ke halaman “A” dijumlahkan, nilai itu kemudian dikalikan dengan damping factor yang bernilai antara 0 sampai 1. Hal ini dilakukan agar tidak keseluruhan nilai pagerank halaman T didistribusikan ke halaman A. 



## Konsep

Banyak cara digunakan *search engine* dalam menentukan kualitas/rangking sebuah halaman web, mulai dari penggunaan *META Tags*, isi dokumen, penekanan pada *content* dan masih banyak teknik lain atau gabungan teknik yang mungkin digunakan. *Link popularity*, sebuah teknologi yang dikembangkan untuk memperbaiki kekurangan dari teknologi lain (*Meta Keywords, Meta Description*) yang bisa dicurangi dengan halaman yang khusus di desain untuk search engine atau biasa disebut *doorway pages*. Dengan algoritme ‘*PageRank*’ ini, dalam setiap halaman akan diperhitungkan *inbound link* (link masuk) dan *outbound link*(link keuar) dari setiap halaman web.

*PageRank*, memiliki konsep dasar yang sama dengan *link popularity*, tetapi tidak hanya memperhitungkan “jumlah” *inbound* dan *outbound link*. Pendekatan yang digunakan adalah sebuah halaman akan diangap penting jika halaman lain memiliki link ke halaman tersebut. Sebuah halaman juga akan menjadi semakin penting jika halaman lain yang memiliki rangking (pagerank) tinggi mengacu ke halaman tersebut.

Dengan pendekatan yang digunakan *PageRank*, proses terjadi secara rekursif dimana sebuah rangking akan ditentukan oleh rangking dari halaman web yang rangkingnya ditentukan oleh rangking halaman web lain yang memiliki link ke halaman tersebut. Proses ini berarti suatu proses yang berulang (rekursif). Di dunia maya, ada jutaan bahkan milyaran halaman web. Oleh karena itu sebuah rangking halaman web ditentukan dari struktur link dari keseluruhan halaman web yang ada di dunia maya. Sebuah proses yang sangat besar dan komplek.

Code :

``` python
import networkx as nx
# hitung pagerank
damping = 0.85
max_iterr = 100
error_toleransi = 0.0001
pr = nx.pagerank(g, alpha = damping, max_iter=max_iterr, tol=error_toleransi)

```
