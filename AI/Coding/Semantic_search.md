```python

import os
import chromadb
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

chroma_client = chromadb.PersistentClient(path="./bankmind_db") # It makes memory permanent 

collection = chroma_client.get_or_create_collection( # uses existing db or creates new
    name="banking_policies",
    metadata={"hnsw:space": "cosine"}
)

def get_embedding(text):
    response = client.embeddings.create(
        model="text-embedding-3-small",
        input=text
    )
    return response.data[0].embedding

documents = [
    {
        "id": "pol_001",
        "text": "Transactions above $10,000 must be reported to FinCEN under the Bank Secrecy Act.",
        "metadata": {"category": "compliance", "regulation": "BSA"}
    },
    {
        "id": "pol_002",
        "text": "KYC procedures require verifying customer identity using government-issued photo ID before account opening.",
        "metadata": {"category": "kyc", "regulation": "AML"}
    },
    {
        "id": "pol_003",
        "text": "Suspicious activity reports must be filed within 30 days of detecting potentially fraudulent transactions.",
        "metadata": {"category": "fraud", "regulation": "BSA"}
    },
    {
        "id": "pol_004",
        "text": "Mortgage applications require debt-to-income ratio below 43% and minimum credit score of 620.",
        "metadata": {"category": "lending", "regulation": "internal"}
    },
    {
        "id": "pol_005",
        "text": "Wire transfers to high-risk jurisdictions require enhanced due diligence and compliance officer approval.",
        "metadata": {"category": "compliance", "regulation": "OFAC"}
    },
]


print("Storing policies in ChromaDB...")

for doc in documents:
    collection.upsert(
        ids=[doc["id"]],
        documents=[doc["text"]],
        embeddings=[get_embedding(doc["text"])],
        metadatas=[doc["metadata"]]
    )

print(f"Stored {collection.count()} policies\n")

#User Query -> Embedded -> 
def semantic_search(query, n_results=2): 
    query_vector = get_embedding(query)

    results = collection.query(
        query_embeddings=[query_vector],
        n_results=n_results,
        include=["documents", "metadatas", "distances"]
    )

    print(f"Query: '{query}'")
    print("-" * 55)

    for i, (doc, meta, dist) in enumerate(zip(
            results["documents"][0],
            results["metadatas"][0],
            results["distances"][0]
    )):
        similarity = round(1 - dist, 3)
        print(f"\nResult {i + 1} — similarity: {similarity}")
        print(f"Category : {meta['category']}")
        print(f"Regulation: {meta['regulation']}")
        print(f"Policy   : {doc}")


semantic_search("What do I do when customer deposits large amount of cash?")
semantic_search("How do I verify who my customer is?")
semantic_search("Can someone with bad credit get a mortgage?")
semantic_search("Sending money to a risky country")
