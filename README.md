#### Oanh Tran:  029661786
#### William Trinh: 
# CECS 427 -- Assignment 1: Graph.py
#### Oanh Tran:  029661786
#### William Trinh: 
`graph.py` is a command-line Python program that works with **undirected graphs** using **NetworkX**. It can:

- Generate a random graph using an Erdős–Rényi-style probability 
- Run **Breadth-First Search (BFS)** from one or more starting nodes
- Print a readable BFS tree for each BFS run
- Analyze graph structure (components, cycles, isolated nodes, density, shortest paths if connected)
- Visualize the graph using Matplotlib
  

## Libraries 
- networkx
- matplotlib
- argparse
- collections.deque
- math
- random
  
## Usage Instructions
1. install required libraries
pip install networkx matplotlib
2. Run program using terminal or command prompt

Command line structure: 

python ./graph.py [--input graph_file.gml] [--create_random_graph n c] [--multi_BFS a1 a2 ...] [--analyze] [--plot] [--output out_graph_file.gml]


Example: 
python ./graph.py --create_random_graph 150 1.35 --multi_BFS 3 12 47 --analyze --plot --output result_graph.gml

The command generates a 150 node Erdős–Rényi graph, runs BFS from nodes 3, 12, and 47, runs full analysis on the graph, visualizes the graph, and exports the result to a gml file. 






## Implementation

The program uses `argparse` to define these command-line options:

 `--create_random_graph n c`  `--multi_BFS a1 a2 ...` (a1, a2 ... are node labels) 
 `--analyze` `--plot`  `--input FILE` (in progress) - `--output FILE` (in progress)

**Generate Random Graph** using the **Erdos-Renyi model** -> generate_graph(n: int, c: float):
- n = # of nodes, c = positive constant 
- creates an undirected graph using networkx library, nx.Graph()
- nodes are added and labeled as strings "0", "1",..."n-1"
- edge probability: p = (c * ln(n))/n
- for each node pair (i, j) where i < j, a random number is generated and if random.random() < p, an edge is added between both nodes
- prints node labels, node pairs with edges, number of nodes and number of edges


**BFS traversal:** -> bfs(graph, start): 
- implements BFS algorithm and uses a queue to explore nodes level by level. A set tracks visited nodes, and a dictionary stores parent-child relationships, used for forming the BFS tree.
- prints the order in which nodes are visited and returns parent dictionary

**BFS Tree Printing** -> printBFS(parent, start): 
- converts the parent dictionary produced by BFS into a tree structure using ASCII characters to visually represent parent-child relationships.

**Multi-Source BFS** -> multiBFS(G, *start_nodes):
- allows BFS to be executed from multiple starting nodes
- verifies input node exists in graph; if not error message relayed. ex: "Node 50 does not exist in the graph"
- runs bfs(graph, start) and printBFS(parent, start): tree for all start nodes
- example output: <img width="1759" height="709" alt="image" src="https://github.com/user-attachments/assets/93352caf-6066-4432-ab7f-61c97329b0a6" />


**Analysis** -> analysis(G):
- connected components: counts and lists connected components
- cycle detection: detects whether a cycle exists and prints which nodes are in a cycle
- isolated nodes: identifies and prints nodes with a degree of 0
- graph density: existing edges/maximum possible edges
- average shortest path length: computed only if graph is connected

**Graph Visualization**
plot(G) function visualizes the generated graph using a spring layout 
- all nodes and edges are drawn with labels and a legend is provided to distinguish normal nodes from isolated nodes.
- visualization window is opened

**Main**
- parses arguments
- invalid arguments and invalid values for parameters result in raised errors.

  
Command Line → argparse → Parsed Namespace → Graph Input/Generation → BFS → Analysis → Visualization → Export


