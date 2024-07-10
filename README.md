# Crypto Price Prediction based on Twitter Influencer Sentiment Analysis.

This project is a part of the my research study, focusing on the analysis of social media influencers using network analysis techniques. The primary objective is to construct and visualize a directed graph that represents the relationships between influencers based on their follower counts.

## Contents

- **influencer_list_modified.csv**: The dataset containing influencer information.
- **CDS590.ipynb**: Jupyter Notebook containing the code for data processing, network construction, visualization, and analysis.

## Requirements

- Python 3.x
- pandas
- networkx
- matplotlib
## Overview Architecture
![image](https://github.com/alexleong4438/crypto_price_prediction_based_on_sentiment/assets/36787182/ea6b1f1b-86e9-4fe5-892e-178abc83f4a8)

## Usage

1. Load the Dataset:
    The dataset is loaded from a local file using pandas.
    ```python
    influencer_df = pd.read_csv("path_to_your_dataset/influencer_list_modified.csv", low_memory=False, keep_date_col=True, nrows=100000)
    influencer_df.head(10)
    ```
2. Data Processing:
   The data is processed to create a dictionary that organizes the influencer information.
    ```python
    username_dict = influencer_df["username"].tolist()
    follow_by_dict = influencer_df["total_follow_by"].tolist()
    followby_count = influencer_df["count"].tolist()
    iteration = influencer_df["iteration"].tolist()
    
    combined_dict = {}
    for key in username_dict:
        combined_dict[key] = []
        for value in follow_by_dict:
            combined_dict[key].append(value)
            follow_by_dict.remove(value)
            break

    for value1 in followby_count:
        combined_dict[key].append(value1)
        followby_count.remove(value1)
        break

    for value2 in iteration:
        combined_dict[key].append(value2)
        iteration.remove(value2)
        break
    ```   
3. Network Construction:
   Using NetworkX, an asymmetric directed graph is constructed to represent the influencer network.
   ```python
     import networkx as nx
    
    G_asymmetric = nx.DiGraph()
    count = 0
    for key, values in combined_dict.items():
        for value in values[:-2]:
            followby_list = value.split(",")

        for follower in followby_list:
            G_asymmetric.add_edge(follower, key)  
   ```

4. Visualization:
   The constructed graph is visualized using Matplotlib.
   ```python
   import matplotlib.pyplot as plt

    nx.spring_layout(G_asymmetric)
    nx.draw(G_asymmetric, with_labels=True)
    plt.figure(figsize=(1000, 1000))
    plt.show()
   ```
5. Graph Information:
   Print information about the graph.
   ```python
   print(nx.info(G_asymmetric))
   ```

   
