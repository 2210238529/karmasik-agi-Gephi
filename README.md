# karmasik-agi-Gephi

import pandas as pd

df = pd.read_csv('data (2).csv')

nodes = []
edges = []

# Sadece Semtleri ve Evleri düğüm olarak ekliyoruz (Şehirleri sildik)
for locality in df['locality'].unique():
    nodes.append({'Id': locality, 'Label': locality, 'Type': 'Locality'})

for idx, row in df.iterrows():
    house_id = f"House_{idx}"
    # Ev düğümü
    nodes.append({'Id': house_id, 'Label': row['house_type'], 'Type': 'Property', 'City': row['city']})
    
    # SADECE Ev -> Semt bağlantısı kuruyoruz. 
    # Semt -> Şehir bağlantısını sildiğimiz için gruplar arası köprüler kalkar.
    edges.append({'Source': house_id, 'Target': row['locality'], 'Type': 'Undirected'})

pd.DataFrame(nodes).to_csv('gephi_nodes_v2.csv', index=False)
pd.DataFrame(edges).to_csv('gephi_edges_v2.csv', index=False)

print("Yeni dosyalar hazır! Şehir köprüleri kaldırıldı.")


<img width="977" height="755" alt="image" src="https://github.com/user-attachments/assets/770ffa9c-c0e7-4b27-9dab-7b18d682e762" />
