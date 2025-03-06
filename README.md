# Dynamic Embeddings Model

In this notebook, we will develop a dynamic embeddings model that selects the appropriate element on the fly based on the query and the retrieved document. We will use various libraries such as `sentence-transformers`, `requests`, `BeautifulSoup`, and `duckduckgo_search` to achieve this. The notebook will cover the following steps:

1. Install necessary libraries.
2. Load and preprocess the data.
3. Define a class to fetch web content using DuckDuckGo search.
4. Encode the text using a pre-trained SentenceTransformer model.
5. Calculate pairwise distances between embeddings.
6. Visualize the results with a plot.

## Jupyter Notebooks

<div id="notebook-content"></div>

<script>
  fetch('embeddings.html')
    .then(response => response.text())
    .then(data => {
      document.getElementById('notebook-content').innerHTML = data;
    });
</script>


# Summary

In this notebook, we developed a dynamic embeddings model that selects the appropriate element on the fly based on the query and the retrieved document. We covered the following steps:

1. Installed necessary libraries.
2. Loaded and preprocessed the data.
3. Defined a class to fetch web content using DuckDuckGo search.
4. Encoded the text using a pre-trained SentenceTransformer model.
5. Calculated pairwise distances between embeddings.
6. Visualized the results with a scatter plot, including a legend to show the original labels.

This approach allows us to dynamically select and process relevant documents based on the query, leveraging the power of pre-trained embeddings and distance metrics.