# Legal Document Embedding & Search with FAISS

This project processes legal sections from JSON files, generates embeddings using the Qwen1.5-0.5B tokenizer, and indexes them using FAISS for efficient similarity search.

## Features
- Loads legal sections from JSON files.
- Uses Qwen1.5-0.5B tokenizer to generate embeddings.
- Stores embeddings in a FAISS index for quick retrieval.
- Saves metadata alongside embeddings for reference.
- Provides downloadable FAISS index and metadata.

## Setup & Installation
### Prerequisites
Ensure you have the required libraries installed:
```bash
pip install faiss-cpu langchain transformers
```

### Run the Script
1. Clone the repository:
```bash
git clone https://github.com/yourusername/legal-faiss-index.git
cd legal-faiss-index
```
2. Set up the directory for legal data:
```python
import os
DATA_DIR = "./legal_data"
os.makedirs(DATA_DIR, exist_ok=True)
```
3. Place your JSON legal documents in the `legal_data/` directory.
4. Run the script:
```python
python legal_indexing.py
```

## File Structure
```
/legal-faiss-index
│── legal_indexing.py    # Main script to generate embeddings & FAISS index
│── legal_metadata.json  # Stores metadata of legal sections
│── legal_index.faiss    # FAISS index storing embeddings
│── legal_data/          # Folder containing JSON legal documents
```

## Example JSON Format
Each JSON file should contain an array of legal sections:
```json
[
  {
    "section": "1",
    "section_title": "Introduction",
    "section_desc": "This section provides an introduction to the act."
  }
]
```

## How It Works
1. The script loads all legal sections from JSON files.
2. It tokenizes and generates embeddings using `Qwen1.5-0.5B`.
3. Embeddings are stored in FAISS for efficient similarity search.
4. Metadata is saved separately for reference.
5. The FAISS index and metadata JSON are available for download.

## FAISS Search Example
To load and search in FAISS:
```python
import faiss
import numpy as np
import json

# Load FAISS index
index = faiss.read_index("legal_index.faiss")

# Load metadata
with open("legal_metadata.json", "r") as f:
    metadata = json.load(f)

# Perform a search
query_embedding = get_embedding("Search Query Here")
dists, indices = index.search(np.array([query_embedding], dtype="float32"), k=5)

# Retrieve top results
for i in indices[0]:
    print(metadata[i])
```

## Contribution
Feel free to fork and contribute! Open issues for any questions or improvements.

## License
MIT License

## Acknowledgments
- [FAISS](https://github.com/facebookresearch/faiss) for vector search
- [Transformers](https://huggingface.co) for NLP models
- This project utilizes datasets from another GitHub repository for model training. Special thanks to the original dataset creator. 🎖 [https://github.com/civictech-India/Indian-Law-Penal-Code-Json/tree/main]
