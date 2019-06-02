## Graph

Grafik adalah struktur data non-linear yang terdiri dari node dan edge. Node kadang-kadang juga disebut sebagai simpul dan ujungnya adalah garis atau busur yang menghubungkan dua node dalam grafik.

Pada Web Structure Mining, Graph Berarah (directed graph) digunakan untuk menggambarkan hubungan suatu web. Beberapa terminology yang digunakan di Web Structure Mining 

### Code

Proses pembuatan Graph pada Python bisa dilakukan dengan mudah menggunakan library `networkx` dan mathplotlib untuk menampilkannya.


``` python
import networkx as nx
import networkx as nx

#membuat Graph
g = nx.from_pandas_edgelist(edgelistFrame, "From", "To", None, nx.DiGraph())
# deklarasi pos (koordinat) (otomatis)
pos = nx.spring_layout(g)
# Membuat Label && print pagerank
print("keterangan node:")
nodelist = g.nodes
label= {}
data = []
for i, key in enumerate(nodelist):
    data.append((pr[key], key))
    label[key]=i
    print(i, key, pr[key])
data = pd.DataFrame(data, None, ("PageRank", "Node"))
# Draw Graph
#plt.figure(1)
#plt.title('circle_layout')
nx.draw(g, pos)
nx.draw_networkx_labels(g, pos, label, font_color="b")
# show figure
plt.axis("off")
plt.show()
```

Pertama  membuat sebuah Graph berarah dengan memanggil g = `nx.Graph()` lalu `g = g.to_directed()`. Lalu untuk memasukkan daftar edge yang telah dibuat ke graph,menggunakan `.from_pandas_edgelist` dengan paraeter berturut-turut pandas.DataFrame, nama_kolom_sumber, nama_kolom_tujuan, edge_attribut, dan jenis_graph.

Kemuidan mendefinisikan letak dari setiap node menggunakan layout yang tersedia di networkx, seperti `nx.spring_layout(g)`. Untuk menampilkan graph, menggunakan method `nx.draw(graph, pos)`. Kemudian `plt.show()