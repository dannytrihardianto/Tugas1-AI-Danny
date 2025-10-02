# Implementasi Algoritma A* Search pada contoh graf di gambar

# 1️⃣ Membuat representasi graf dalam bentuk dictionary
#    Setiap node memiliki tetangga dan biaya ke tetangga tersebut
graph = {
    'S': {'A': 2, 'D': 2},
    'A': {},
    'D': {'B': 1, 'E': 4},
    'B': {'C': 2, 'E': 1},
    'C': {},
    'E': {'G': 2},
    'G': {}
}

# 2️⃣ Membuat nilai heuristik (h) untuk tiap node sesuai gambar
#    Heuristik = perkiraan jarak dari node ke goal (G)
heuristics = {
    'S': 7,
    'A': 9,
    'D': 5,
    'B': 4,
    'C': 2,
    'E': 3,
    'G': 0
}

# 3️⃣ Fungsi A* Search
def a_star_search(start, goal):
    # frontier: daftar node yang akan dieksplor, format (f, g, path)
    # f = g + h, g = biaya sebenarnya sejauh ini
    frontier = [(heuristics[start], 0, [start])]
    explored = []  # untuk mencatat urutan eksplorasi

    while frontier:
        # 4️⃣ Ambil node dengan f terendah dari frontier
        frontier.sort(key=lambda x: x[0])  # urutkan berdasarkan f
        f, g, path = frontier.pop(0)       # ambil node teratas
        current = path[-1]                 # node saat ini = node terakhir di path

        # 5️⃣ Jika sudah mencapai goal, kembalikan hasil
        explored.append(current)
        if current == goal:
            return path, explored

        # 6️⃣ Perluas tetangga dari node saat ini
        for neighbor, cost in graph[current].items():
            # g baru = biaya sejauh ini + biaya ke tetangga
            new_g = g + cost
            # f baru = g baru + heuristik dari tetangga
            new_f = new_g + heuristics[neighbor]
            # path baru = path lama + tetangga
            new_path = path + [neighbor]
            # masukkan ke frontier
            frontier.append((new_f, new_g, new_path))

    return None, explored  # jika tidak ditemukan jalur

# 7️⃣ Jalankan A* dari S ke G
path, explored_nodes = a_star_search('S', 'G')

# 8️⃣ Cetak hasil
print("Jalur terbaik (Path):", " -> ".join(path))
print("Urutan eksplorasi node:", " -> ".join(explored_nodes))
