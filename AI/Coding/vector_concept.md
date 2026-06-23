```Python
import os
from openai import  OpenAI
from dotenv import load_dotenv

load_dotenv()
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

### Creates a Vector from Text

def get_embedding(text):
    response = client.embeddings.create(
        model="text-embedding-3-small",
        input=text
    )
    return response.data[0].embedding

sentence = "suspicious wire transfer flagged for review"

vector = get_embedding(sentence)

print(f"Sentence: {sentence}")
print(f"Number of dimensions: {len(vector)}")
print(f"First 5 numbers: {vector[:5]}")
