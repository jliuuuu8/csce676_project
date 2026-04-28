# Echo Chamber Detection in Large-Scale Social Networks

## 📖 Overview

This project investigates whether large social networks exhibit **echo chamber behavior**, where users primarily interact within tightly connected communities rather than across diverse groups. Utilizing the SNAP Ego-Twitter dataset, I analyze structural patterns in the Twitter network to determine whether meaningful community structure exists. If such structure exists, then how does that information flow between various groups.

👉 Start with the following notebook: **main_notebook.ipynb**

📹 Advertisement Video: https://www.youtube.com/watch?v=TvkBkBJWwAA&t=1s

--- 

## ❓Research Questions
- Do large social networks exhibit tightly clustered communities?
- Are tese communities structurally isolated or still interconnected?
- Are there "bridge users" that connect separate communities?

---

## 🗂️ Dataset
- **SNAP Ego-Twitter Dataset**
- Link: https://snap.stanford.edu/data/wiki-Vote.html
- File: twitter_combined.txt.gz

### Preprocessing:
- Loaded raw edge list into a directed graph (follower relationships)
- Extracted largest weakly connected component (main interaction)
- Converted to undirected graph for community analysis

---

## 🔬 Research Approach

### Phase 1: Structural Analysis
- Computed global graph properties: graph size, density, reciprocity
- Degree distributions (in/out degree)

### Phase 2: Community Detection
- Louvain(primary method)
- Label Propagation (comparison)
- Greedy Modularity was considered for a comparison community detection method, but it was computationally expensive and not scalable to the graph.

### Phase 4: Bridge User Detection

- Features:
    - Degree
    - Distinct Neighbor Communities
    - Betweenness
    - Clustering Coefficient
- Node2Vec used to learn vector representataions of nodes based on graph structure
- K-Means clustering applied to embeddings to group similar nodes
- Compared embedding clusters with Louvain communities using:
    - ARI (Adjusted Rand Index)
    - NMI (Normalized Mutual Information)
    - Silhouette Score
- Isolation Forest for detecting structural anomalies

### Phase 5: Validation of Results
- Degree-preserving randomized baseline
- Compared modularity and structure to random graph


## 🔍 Key Results

- High modularity **(~0.80)** indicates strong community separation
- **~87%** of edges stay within communities
- Randomized baseline destroys graph structure and confirms that communities are meaningful
- Presence of **bridger users** connect multiple communities together
- Communities are tightly connected but not fully isolated

👀 Conclusion:
- The network exhibits strong echo-chamber like structure, but allows for selective cross-community interaction.

## 🐍 Python Version
- Python 3.12.13

## Reproduce the Work
This project was developed in Google Colab. Therefore, the easiest way to reproduce the project is to rerun the notebook in Colab.

### Option 1: Google Colab

1. Open 'main_notebook.ipynb' in Google Colab.
2. Run all cells from top to bottom

### Option 2: Run Locally on VS Code

Python 3.12 is required

1. Have Python 3.12 already installed on local machine. Open the VS Code terminal and run the command at the bottom.
```bash 
 winget install Python.Python.3.12 --scope machine 
```

2. Clone GitHub repository:
```bash
git clone https://github.com/jliuuuu8/csce676_project.git
```

3. Open project folder in VS Code and click on "main_notebook.ipynb"

4. Install all the required dependencies by pasting the command into the VS Code terminal
```bash
py -3.12 -m pip install -r requirements.txt
```

5. Click "Run All"
    - When selecting the kernel, make sure to choose any Python 3.12 version. Picking anything else will cause the code to break.

## 📦Key Dependencies
- networkx 3.6.1
- numpy 1.26.4
- pandas 2.2.2
- matplotlib 3.10.0
- scikit-learn 1.6.1
- node2vec 0.5.0

## Repository Structure

