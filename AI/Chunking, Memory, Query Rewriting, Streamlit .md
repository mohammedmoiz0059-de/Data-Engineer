#### Chunking : Breaking large documents into smaller, semantically coherent pieces before embedding.
Analogy   
A librarian bringing you exactly page 47 — the specific section you need — not the entire 200 page manual.   
Why needed   
- One vector cannot capture 200 pages precisely. Small focused chunks = precise retrieval. Also — embedding model has 8191 token limit.   
- Too large chunks    
- Vector captures everything loosely. Retrieval imprecise. Like bringing entire manual.   
- Too small chunks   
- Vector loses context. A sentence alone may be meaningless without surrounding paragraphs.       
Production standard: 500 to 1000 tokens per chunk. Paragraph based chunking for policy documents.
**Interview answer**
"Chunking breaks large documents into smaller pieces before embedding — because one vector cannot capture a 200 page document precisely.       
For banking policy RAG I use paragraph based chunking — each paragraph covers one complete idea, making retrieval precise.     
A query about SAR filing deadlines retrieves exactly the SAR paragraph, not the entire BSA manual."        


#### Chunk Overlap : Repeating the last few sentences of one chunk at the start of the next — preserving context across boundaries.     
Analogy   
A book chapter that begins with a one line summary of the previous chapter — so you understand the context even if you start mid-book.       
Why needed     
"This requirement applies to..." — without overlap, what requirement? Context lost at chunk boundary. Overlap carries it forward.     
- Without overlap     
Chunk 2 starts with "This applies to all transactions" — applies to what? Meaning broken.     
- With overlap   
Chunk 2 repeats last sentence of chunk 1 — "This applies to all transactions" now has clear reference.    
Production standard: 50 to 200 token overlap. Balance between context preservation and redundancy.   
**Interview answer**
"Overlap repeats the last few sentences of one chunk at the start of the next.
This preserves context across chunk boundaries. Without overlap, a chunk starting with 'this requirement applies to all transactions above $5,000' has no context — what requirement? With overlap, the previous chunk's last sentence is included, making the reference clear."

#### 4 Chunking Strategies    
1. Fixed size    
Cut every N tokens regardless of meaning. Fast. Simple. Can break mid-sentence. Good for prototypes only.   
2. Sentence chunking  
Cut at full stops. Each chunk = complete sentences. Better than fixed. Inconsistent chunk sizes.  
3. Paragraph chunking    
Cut at paragraph boundaries. Each chunk = one complete idea. Best for banking policy documents.   
4. Recursive with overlap   
Paragraph chunking + overlap between chunks. Production standard. Preserves meaning and context.

**Interview answer**    
"There are four main chunking strategies — fixed size, sentence, paragraph, and recursive with overlap. For banking compliance documents I use recursive chunking with overlap.    
Policy manuals are written in paragraphs where each paragraph covers one regulation. Paragraph boundaries are natural semantic boundaries. Overlap between chunks preserves context across boundaries."      
  
#### Conversation Memory: Storing full conversation history and passing it to the LLM on every call — enabling multi-turn conversations.
Analogy   
An analyst with a notepad — writes every question and answer. Reads notepad before responding to next question. Never has amnesia.   
Banking use case
"What documents for Letter of Credit?" → "How long do I keep those documents?" — "those documents" only makes sense with memory.    
How it works   
messages = [system prompt] + conversation_history + current question. LLM receives all three together.    
Production consideration   
Long conversations hit context window limit. Fix by keeping last N messages or summarising old history.    
In Streamlit — use st.session_state to persist history across reruns. Without it history resets every interaction.    
**Interview answer**
"I implemented conversation memory by maintaining a message history list in Streamlit session state. Every user question and assistant answer is appended to this list.     
Each LLM call receives system prompt plus full history plus current question — enabling follow up questions like 'how long do I keep those documents' to correctly reference documents from the previous answer.   
In production I limit history to last 10 messages to avoid hitting the context window."    

#### Query Rewriting:  Before searching — use LLM to rewrite vague follow up questions into complete standalone questions.    
Problem it solves    
"How long do I keep those documents?" — "those documents" is too vague for semantic search. Retrieval fails.    
How it works    
Pass conversation history + vague question to LLM → LLM rewrites to "How long do I keep Letter of Credit documents under BSA?" → precise retrieval.    
Rewritten query used for    
Retrieval only — precise search needs precise query.    
Original query used for   
Generation — LLM answers what analyst actually asked.    
Common mistake: using rewritten query for generation. Always answer the original question — just retrieve with the rewritten one.   
**Interview answer**   
"Query rewriting solves the vague follow up problem in multi-turn RAG.      
A question like 'how long do I keep those documents' fails semantic search because 'those documents' has no meaning without context.    
Before retrieval I pass the conversation history and vague question to the LLM and ask it to rewrite as a complete standalone question.    
The rewritten query is used for retrieval only — the original question is still used for generation so the analyst gets a natural answer."   


#### Streamlit: Python library that converts scripts into interactive web applications — no HTML, CSS or JavaScript needed.
Analogy    
A car body around your engine. Same RAG pipeline engine — now with steering wheel, seats and windows anyone can use.    
Banking use case    
Compliance officers interact via browser — type questions, get answers. No terminal, no Python, no code.   
5 key commands    
st.title() — heading. st.write() — text. st.chat_input() — input box. st.chat_message() — chat bubble. st.session_state — persistent memory.    
How to run   
streamlit run app.py — not python app.py. Opens browser at localhost:8501 automatically.   
Streamlit reruns entire script on every interaction. Use st.session_state for anything that must persist — conversation history, user preferences, loaded data.    
Interview answer   
"I built a Streamlit frontend for BankMind — it converts the Python RAG pipeline into a browser based chat interface.    
Compliance officers type questions in plain English and get grounded answers with policy citations — no coding required.    
I used st.session_state to persist conversation history across Streamlit reruns, st.chat_message for the chat UI, and st.expander to show retrieved policy sources on demand.    
