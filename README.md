# Automated MongoDB Query Generator with LLM & Vector Search

This project is an end-to-end solution that allows users to ask questions in natural language and automatically generate and execute MongoDB queries using a fine-tuned LLM (e.g., DeepSeek Coder). It leverages vector search for context retrieval and displays query results via a user-friendly Streamlit interface.

---

## Key Features

- **Vector Search**: Built using SentenceTransformer to embed and retrieve relevant context from product descriptions.
- **MongoDB Atlas**: Used as the primary data store with pre-inserted structured data.
- **LLM Integration**: Uses DeepSeek Coder for generating MongoDB `.find()` and aggregation queries.
- **Post-processing**: Converts date and discount fields to their correct types before executing queries.
- **Streamlit UI**: Interactive web app with three tabs:
  - Ask Custom Questions
  - View Predefined FAQs
  - Test Cases
- **Persistent Logging**: Saves generated queries in `.txt` files and results in `.csv`.

---

## How It Works

### 1. Data Preparation (in `notebook.ipynb`)
- Load your product CSV data.
- Preprocess the fields like `LaunchDate` and `Discount`.
- Insert cleaned data into MongoDB Atlas.
- Create a vector index for the `description` field.

### 2. Streamlit App (`app.py`)
- User enters a question.
- Vector search retrieves relevant context.
- LLM generates MongoDB query using the custom prompt.
- Mongo query is parsed, cleaned, and executed.
- Results are displayed in a DataFrame.
- Queries are saved in `saved_queries/`, and results in `saved_results/`.

---

## ✅ Example

**Question:** What are the products with a price greater than $50?

**Generated Query:**
```json
{
  "filter": { "Price": { "$gt": 50 } },
  "projection": {
    "ProductID": 1,
    "ProductName": 1,
    "Price": 1,
    "_id": 0
  }
}
```
