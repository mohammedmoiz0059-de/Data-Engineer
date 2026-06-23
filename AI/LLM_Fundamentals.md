- Language Model
- Large Language Model (LLM)
- Tokens
- Context Window
- Transformers
- Fine-Tuning
- Hallucination

#### LLM — Large Language Model
**One line**   
A neural network trained on billions of text to predict the next word — and through that, learns to reason, summarise, classify and generate.   
**Analogy**  
A brilliant intern who has read every book, paper and website ever written — but has never worked at your specific bank.   
**Banking use case**  
Transaction classification, fraud narrative summarisation, customer query answering, policy Q&A.   
**Interview answer**  
"An LLM is a neural network trained on massive text data to understand and generate language. In banking we use it to classify transactions, summarise fraud reports, and answer compliance questions — tasks that previously required human analysts."  

Think of an LLM as an extremely smart intern who:  
- Has read the entire internet    
- Has zero memory between conversations       
- Only knows what you tell them in the current message     
- Will confidently guess if they don't know — that's **hallucination**  

Every time you call the API, it's a fresh conversation with no memory of the last call. That's why we build RAG — to give it memory and company knowledge.

**3 things that control LLM behaviour — memorise these:**   
Parameter   What it doesBanking usesystem promptGives the model its role and rules  "You are a banking risk analyst.   Never give investment advice.   
"temperature0 = deterministic, 1 = creativeRisk classification → 0. Report writing → 0.3   
max_tokens  Limits response lengthShort answers → 200. Full reports → 1000   

**Tokens**  are the basic units of text that a model processes.   
It can be whole word, part of word and mostly it 3/4 of the word.     

Why???
 LLMs doesnt understand words, it has to be converted into vectors.  

**Chunk**
A chunk is a group of text that you create, usually for embedding, semantic search, or RAG.     

 A token is a unit of text processed by the model, while a chunk is a larger segment of text containing many tokens. In RAG and semantic search, documents are split into chunks, and embeddings are typically generated for each chunk rather than for each individual token.




**Context window** The context window is the amount of information the model can "see" in a single conversation turn   
for 128k - 128000 tokens -> approx 90k -100k english words.


A 128k-token context window means the model can process and attend to up to 128,000 tokens in a single request, including the prompt, conversation history, retrieved documents, and generated output. Larger context windows allow the model to work with longer documents and maintain more conversational context.   



"Your RAG system has a 500-page document. The context window is only 128K tokens. How do you handle it?"   
Answer: You don't send the whole document. You chunk it, embed it, store it in a vector DB, and retrieve only the 3-5 most relevant chunks at query time. That is literally why RAG exists — to work around context window limits.   


#### Temperature
**One line**   
Controls how creative vs precise the LLM is. A dial between predictable and random.  
**Analogy**  
A ceiling fan speed dial. Low speed — calm, predictable, precise. High speed — energetic, creative, unpredictable.   
**Banking use case**  
Temperature 0 for compliance answers — always precise. Temperature 0.7 for customer email drafting — more natural tone.   
Low temperature (0 to 0.3)
Deterministic, consistent, factual. Use for: classification, compliance, data extraction.   
High temperature (0.7 to 1.0)   
Creative, varied, natural. Use for: email drafting, summarisation, customer communication.   
**Interview answer**  
"Temperature controls the randomness of the LLM output. For compliance and classification tasks in banking I set it close to 0 — we need consistent, precise answers every time. For customer-facing communication I raise it slightly so responses sound more natural."   

