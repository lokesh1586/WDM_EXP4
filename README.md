### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 04.08.2026
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("clustervisitor.csv")

X = df["Age"].values
k = 3

centroids = list(X[:k])

while True:
    clusters = [[] for _ in range(k)]
    labels = []

    for value in X:
        distances = [abs(value - c) for c in centroids]
        cluster = distances.index(min(distances))
        clusters[cluster].append(value)
        labels.append(cluster)

    new_centroids = []

    for cluster in clusters:
        if len(cluster) > 0:
            new_centroids.append(sum(cluster) / len(cluster))
        else:
            new_centroids.append(0)

    if new_centroids == centroids:
        break

    centroids = new_centroids

df["Cluster"] = labels

print("\nComplete Dataset\n")
print(df)

for i in range(k):
    print(f"\nCluster {i}\n")
    print(df[df["Cluster"] == i])




```
### Output:
<img width="650" height="787" alt="Screenshot 2026-08-04 112425" src="https://github.com/user-attachments/assets/aaf01106-43cb-4810-bbd9-a58fc0cc8111" />
<img width="662" height="672" alt="Screenshot 2026-08-04 112435" src="https://github.com/user-attachments/assets/9f381afb-7e11-46a2-892a-7f02f85ef361" />
<img width="563" height="320" alt="Screenshot 2026-08-04 112442" src="https://github.com/user-attachments/assets/7809729d-4b40-4f66-befc-dc4f07df0c79" />


### Visualization:
```python

colors = ["red", "blue", "green"]

plt.figure(figsize=(8,5))

for i in range(3):
    cluster_data = df[df["Cluster"] == i]
    plt.scatter(cluster_data["Age"],
                [i] * len(cluster_data),
                color=colors[i],
                s=80,
                label=f"Cluster {i}")

plt.scatter(centroids,
            range(3),
            color="black",
            marker="X",
            s=200,
            label="Centroids")

plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.yticks([0, 1, 2], ["Cluster 0", "Cluster 1", "Cluster 2"])
plt.legend()
plt.grid(True)
plt.show()
```
### Output:

<img width="1087" height="665" alt="Screenshot 2026-08-04 112521" src="https://github.com/user-attachments/assets/bc3bf375-1e61-40fe-9637-98f0856ecbea" />

### Result:
