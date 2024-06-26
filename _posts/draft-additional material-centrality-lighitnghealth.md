


$\text{Katz Centrality}(v) = \alpha \sum_{j=1}^{n} A_{ij} x_j + \beta$

$\text{PageRank}(p_i) = \frac{1-d}{N} + d \sum_{p_j \in M(p_i)} \frac{\text{PageRank}(p_j)}{L(p_j)}$


This is an attemt to define centrality metrics in an intuitive way that would work for even your four legged kid, if you try. I'll also add some thoughts on relevance of the metric in context of Lightning network.

6.  **Katz Centrality**
        -   Similar to its cousin, the Eigenvector, but adds a sprinkle of influence from all nodes within a few handshakes. It acknowledges even the faintest nod from across the room.
7.  **PageRank**
        -   The algorithm of the Internet age, crafted by Google’s own. Nodes gain status not just by having many connections, but how significant those connections are. It’s the difference between a nod from a king and a wave from a crowd.


get connected to a node with high degree centrality with good channel size that is balanced, you are well set to send and receive payments. However, when we are comparing nodes with similar degree centrality, the one that have good channel size, and kept it balance is the one you should choose, even though they may have relatively lower degree centrality


## A more comprehensive graph

```mermaid
flowchart LR
    Ava --- Mia
    Mia --- Zoe
    Zoe --- Ivy
    Ivy --- Mya
    Mya --- Eva
    Eva --- Ida
    Ida --- Uma
    Uma --- Ava
    Zoe --- Eva
    Mia --- Ida
    Ava --- Uma
    Uma --- Ivy
    Ivy --- Zoe
    Zoe --- Mya
    Mya --- Uma
   ```

## Python code to do centrality measure

## Generic formula for centrality measure for mathematically savvy

$\text{Betweenness Centrality}(v) = \sum_{s \neq v \neq t} \frac{\sigma_{st}(v)}{\sigma_{st}}$

$\text{Degree Centrality}(v) = \frac{\text{Degree of } v}{N-1}$

$\text{Closeness Centrality}(v) = \frac{N-1}{\sum_{u=1}^{N} d(v, u)}$

$\text{Eigenvector Centrality}Ax = \lambda x$


     - This is also a good node to get connected to. However make sure that the canal is wide enough, and secondly, it is quite possible two nodes have same betweenness centrality but they add completely different value to you. Think of Panama and Swej.

        - what this metrics tells you is that if you have to do mass payments of micro sizes. this is the node to get connected to. The condition of micro size matters because it mimizes the effect of channel size and balanced channel. Mass payments matters because if you expect to send or receive from all almost everyone then it is good metric to look at.



Given that both graphs are designed for transmitting data from one node to another, the comparison should focus on metrics that highlight the efficiency, robustness, and overall performance of data transmission within each network. Here are several key metrics and considerations that can help you determine which graph might be better suited for data transmission tasks:

### 1. **Connectivity**

-   **Description**: Check the connectivity of each graph. A well-connected graph ensures that there are multiple paths for transmitting data, which increases the reliability of data transfer.
-   **Metric**: Look at the number of connected components, the size of the largest connected component, and the average node degree.

### 2. **Path Length**

-   **Description**: The average shortest path length is crucial for data transmission as it affects the speed of communication between any two nodes.
-   **Metric**: Average shortest path length (mean geodesic distance) and diameter of the graph (the longest of all the shortest path lengths).

### 3. **Robustness**

-   **Description**: The ability of the graph to maintain connectedness and functionality when nodes or edges fail.
-   **Metric**: Measure the graph's resilience by simulating node or edge failures and observing how the graph's connectivity and average path length are affected.

### 4. **Throughput**

-   **Description**: The graph’s capacity to handle large amounts of data simultaneously without significant delays.
-   **Metric**: This can be indirectly measured by analyzing the graph’s degree distribution and bandwidth (which might be theoretical in some cases unless specified by the network’s physical or software design).

### 5. **Network Efficiency**

-   **Description**: Overall efficiency of the network in terms of both local and global efficiency.
-   **Metric**: Global efficiency (inverse of the average shortest path length) and local efficiency (measures efficiency of information transfer in localized clusters).

### 6. **Clustering Coefficient**

-   **Description**: Indicates the degree to which nodes in the graph tend to cluster together. High clustering can suggest robustness, as parallel paths can exist for data transmission.
-   **Metric**: Global and average local clustering coefficients.

### 7. **Centrality Measures**

-   **Description**: Important to identify critical nodes for maintaining fast and reliable communication.
-   **Metric**: Degree centrality (for node importance), betweenness centrality (nodes critical for bridging paths), and closeness centrality (nodes efficiently distributing data).

### 8. **Scalability**

-   **Description**: How well can the network grow? This is particularly important if the network needs to accommodate more nodes or heavier data flow without significant performance degradation.
-   **Metric**: This is more of a qualitative assessment, looking at how adding nodes or edges affects the metrics mentioned above.

### 9. **Load Balancing**

-   **Description**: The ability of the network to distribute traffic evenly among nodes to prevent any single node from becoming a bottleneck.
-   **Metric**: Variance in node degree and edge loads can be simulated under various traffic conditions to observe potential bottlenecks.

### Practical Comparison Steps:

-   **Simulation**: Run simulations on both graphs to see how data flows under various conditions, such as high traffic, node/edge failures, or rapid network scaling.
-   **Software Tools**: Use network analysis and simulation tools like NetworkX for Python, Gephi, or specialized simulation software that can model data flow and test network resilience under stress.

### Decision Criteria:

-   Choose the graph that demonstrates better performance across these metrics, particularly focusing on robustness, efficiency, and shortest paths if your main goal is to optimize for fast and reliable data transmission. The choice might also depend on specific operational requirements like fault tolerance, load capacity, or future scalability.

By focusing on these metrics, you can make a well-informed decision about which graph is more suitable for your data transmission needs, considering both the current performance and future adaptability of the network.

    import networkx as nx
import matplotlib.pyplot as plt

def create_graph(edges):
    G = nx.Graph()
    G.add_edges_from(edges)
    return G

def analyze_graph(G, name):
    print(f"Analysis of {name}:")
    # Number of nodes and edges
    print("Number of nodes:", G.number_of_nodes())
    print("Number of edges:", G.number_of_edges())

    # Check connectivity
    print("Is connected:", nx.is_connected(G))
    if nx.is_connected(G):
        # Average shortest path length and diameter
        print("Average shortest path length:", nx.average_shortest_path_length(G))
        print("Diameter (longest shortest path):", nx.diameter(G))
    
    # Clustering coefficient
    print("Average clustering coefficient:", nx.average_clustering(G))

    # Degree Centrality
    degree_centrality = nx.degree_centrality(G)
    print("Max degree centrality:", max(degree_centrality.values()))

    # Betweenness Centrality
    betweenness_centrality = nx.betweenness_centrality(G)
    print("Max betweenness centrality:", max(betweenness_centrality.values()))

    # Closeness Centrality
    closeness_centrality = nx.closeness_centrality(G)
    print("Max closeness centrality:", max(closeness_centrality.values()))

    # Plotting the graph
    plt.figure(figsize=(8, 6))
    nx.draw(G, with_labels=True, node_color='skyblue')
    plt.title(f"Network Diagram of {name}")
    plt.show()
    # Example edges for two graphs
edges1 = [(1, 2), (2, 3), (3, 4), (4, 5), (1, 5), (2, 4)]
edges2 = [(1, 2), (2, 3), (3, 4), (4, 5), (1, 5), (1, 3), (2, 5)]
# Create graphs
G1 = create_graph(edges1)
G2 = create_graph(edges2)

# Analyze both graphs
analyze_graph(G1, "Graph 1")
analyze_graph(G2, "Graph 2")

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4MDM0NTY1NF19
-->