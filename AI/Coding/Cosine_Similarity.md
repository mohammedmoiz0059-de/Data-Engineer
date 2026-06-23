```python

import os
import numpy as np
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

def get_embedding(text):
    response = client.embeddings.create(
        model="text-embedding-3-small",
        input=text
    )
    return response.data[0].embedding

def cosine_similarity(vec_a, vec_b):
'''Vector list is converted to array to mathematical calculation
(A,B)=A.B / ∣∣A∣∣ *∣∣B∣∣
to calculate Magnite linalg(linear algorithm)  method is used from numpy)	​''' 
    a = np.array(vec_a)
    b = np.array(vec_b)
    return round(np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b)), 4)

sentence1 = "suspicious wire transfer flagged for review"
sentence2 = "suspicious wire transaction flagged for investigation"
sentence3 = "savings account interest rate update"

vector1 = get_embedding(sentence1)
vector2 = get_embedding(sentence2)
vector3 = get_embedding(sentence3)

score_1_2 = cosine_similarity(vector1, vector2)
score_1_3 = cosine_similarity(vector1, vector3)

print(f"\nSentence 1: {sentence1}")
print(f"Sentence 2: {sentence2}")
print(f"Sentence 3: {sentence3}")

print(f"\nSimilarity — S1 vs S2 (both fraud related): {score_1_2}")
print(f"Similarity — S1 vs S3 (unrelated):           {score_1_3}")
