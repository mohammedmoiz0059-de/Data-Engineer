#### Vector
One line  
An ordered list of numbers that represents a point in multi-dimensional space — the address of a meaning.  
Analogy   
GPS coordinates — but instead of locating a place on earth, they locate a sentence in meaning-space.   
Banking use case   
"Suspicious wire transfer" becomes 1536 numbers — its precise address in meaning-space alongside all other fraud-related concepts.   
Key detail: text-embedding-3-small produces 1536 dimensions. text-embedding-3-large produces 3072. More dimensions = more precise but more expensive.   
Interview answer  
"A vector is a list of numbers that represents the meaning of text as coordinates in a high-dimensional space. Similar meaning produces similar coordinates — like how all Indians are located near India on a world map. In BankMind every policy document and every transaction description is converted into a 1536-dimensional vector."   

#### Embedding  
One line   
The process of converting text into a vector using a neural network trained on billions of sentences.   
Analogy   
The senior expert librarian who has read every document and knows where every concept lives — she gives you the address.   
How it learned similarity   
**Distributional hypothesis** — words appearing in the same context get similar coordinates. AML and anti-money laundering always appear together, so they land nearby.   
**LLM vs embedding model**     
LLM generates text. Embedding model generates vectors. Different tools, different jobs.   
Model used   
text-embedding-3-small — OpenAI's balanced model. Fast, affordable, 1536 dimensions.   
Interview answer   
"An embedding model converts text into a vector — a list of numbers capturing its meaning. It learned similarity from billions of sentences using the distributional hypothesis — words appearing in the same context get similar coordinates. So AML and anti-money laundering end up at nearly identical coordinates even though they share no letters."

#### Cosine Similarity   
One line   
Measures the angle between two vectors — smaller angle means more similar meaning.    
Analogy   
Two people pointing arms in a room — cosine similarity measures the angle between their arms. Direction only, not arm length.    
Formula   
(A · B) / (‖A‖ × ‖B‖) — dot product divided by product of magnitudes.   
Score 1.0   
Identical meaning. 0° angle.   
Score 0.0  
Completely unrelated. 90° angle.  
Score -1.0   
Opposite meaning. 180° angle.   
Why cosine not Euclidean distance? Cosine ignores length — a short query and a long document about the same topic still score high. Only direction (meaning) matters. 
Interview answer  
"Cosine similarity measures the angle between two vectors — the smaller the angle, the more similar the meaning. It gives a score from -1 to 1. We use cosine rather than straight-line distance because we care about semantic direction, not length — a short query and a long policy document about the same topic should score high similarity."   

#### Semantic Search vs Keyword Search   
Keyword search (BM25)   
Matches exact words. Fast. Fails on synonyms, jargon, paraphrasing. Junior analyst searching "9800 cash" — finds nothing.   
Semantic search   
Matches meaning via vectors and cosine similarity. Senior analyst instinct — finds "structuring" policy even when you typed "9800 cash deposit."   
Interview answer   
"Keyword search matches exact words — it fails completely in banking where the same concept has dozens of names. Semantic search converts both the query and documents into vectors and finds the closest meaning using cosine similarity. A compliance officer searching 'customer depositing just under the limit' correctly retrieves the structuring policy — zero shared words, high semantic similarity."   
infrastructure
#### Vector Database   
One line   
Purpose-built database for storing vectors and finding the nearest ones fast — using approximate nearest neighbour search.   
Analogy   
Finding a friend in a new locality — don't knock every door, ask the first person, follow directions, arrive in a few steps.   
Why not normal DB   
Normal DB checks every row exactly. 3.6 billion vectors = 1 hour per query. Vector DB uses HNSW = milliseconds.   
ChromaDB    Local, free, great for learning and prototypes.   
Pinecone Cloud, production scale, billions of vectors.
pgvector PostgreSQL extension — if bank already uses Postgres.  
Interview answer   
"A vector database stores high-dimensional vectors and retrieves the nearest ones using approximate nearest neighbour search. A normal database would need to compare every vector exactly — at billions of records that takes hours. A vector database uses HNSW indexing to navigate intelligently — like asking for directions instead of knocking every door — and finds the nearest vectors in milliseconds."
infrastructure  
#### HNSW — Hierarchical Navigable Small World
One line  
Graph-based algorithm inside vector databases — multi-layer navigation gives fast approximate nearest neighbour search.  
Analogy    
Landing in a new city — big jumps at top layer to get to right area, smaller precise steps at bottom layer to find exact location.   
Complexity   
O(log n) — search time grows very slowly even as vectors grow to billions.   
Interview answer   
"HNSW is the indexing algorithm inside ChromaDB and most vector databases. It builds a multi-layer graph — upper layers make big jumps across the vector space, lower layers make precise small steps. This gives O(log n) search complexity — meaning it finds nearest neighbours in milliseconds even across billions of vectors."

#### RAG — Retrieval Augmented Generation
One line   
Find relevant documents first using semantic search, then pass them to the LLM as context to generate a grounded answer.   
Analogy   
A brilliant lawyer who searches her legal library before every argument — answers grounded in specific documents, not just memory.   
Three steps   
Retrieve — find relevant documents. Augment — pass as context to LLM. Generate — LLM answers from that context.   
Why RAG over bare LLM  
Bare LLM hallucinates, has knowledge cutoff, doesn't know internal policies. RAG grounds answers in documents you control.  
Why critical in banking  
Auditable answers. Every response cites its source document. Regulators can verify. No hallucinated regulations.  
Key word: AUDITABLE. In banking every AI decision needs a paper trail. RAG makes every answer traceable to a specific document.  
Interview answer   
"RAG solves the problem that LLMs don't know your company's internal knowledge. It has three steps — retrieve relevant documents from your knowledge base using semantic search, augment the LLM's input with those documents as context, then generate an answer grounded in that context. In banking this is critical because every answer becomes auditable — you can show exactly which policy document the AI used to reach its conclusion."

#### When RAG fails — 4 failure modes   
1. Wrong embedding model   
Generic model doesn't understand banking jargon. SAR and suspicious activity report not recognised as same concept.   
2. Missing context   
Document never added to knowledge base or outdated. RAG retrieves closest wrong thing. Confident wrong answer.   
3. Poor query quality   
Vague user question produces vague embedding. Wrong retrieval. Generic answer. Fix with query rewriting.   
4. Bad chunking   
Document split in wrong place — chunk loses context. "This applies to..." — applies to what? Meaning broken.   
Interview answer   
"RAG fails in four ways — wrong embedding model that misses domain jargon, missing or outdated documents in the knowledge base, vague user queries that produce poor retrieval, and bad document chunking where splitting in the wrong place destroys context. In a production banking system all four need active monitoring and maintenance."    
