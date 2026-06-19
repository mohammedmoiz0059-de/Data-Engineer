# Artificial Intelligence (AI) 🌐
**Making machines perform tasks requiring human intelligence**

│
├── **Traditional AI**
│   - Uses **human-written rules and logic**
│
│   └── **Rule-Based Systems**
│       - Systems that follow **predefined rules**
│
│       ├── **Expert Systems**
│       │   - Mimic decisions of **human experts**
│       │
│       └── **Search / Logic Systems**
│           - Problem solving using **rules and reasoning**
│
│
└── **Machine Learning (ML)**
    - Machines **learn patterns from data instead of explicit programming**
    │
    ├── **Learning Approaches (HOW models learn)**
    │
    │   ├── **Supervised Learning**
    │   │   - Learns from **labelled input/output data**
    │   │
    │   │   ├── **Regression**
    │   │   │   - Predicts **continuous numeric values**
    │   │
    │   │   └── **Classification**
    │   │       - Predicts **categories/classes**
    │   │
    │   ├── **Unsupervised Learning**
    │   │   - Finds **hidden patterns without labels**
    │   │
    │   │   ├── **Clustering**
    │   │   │   - Groups **similar data points**
    │   │
    │   │   └── **Dimensionality Reduction**
    │   │       - Reduces features while keeping important information
    │   │
    │   ├── **Semi-Supervised Learning**
    │   │   - Uses **small labelled + large unlabelled datasets**
    │   │
    │   ├── ⭐ **Self-Supervised Learning**
    │   │   - Creates **learning signals from data itself**
    │   │
    │   │   └── **LLM Pre-training**
    │   │       - Learns by predicting **tokens from massive text**
    │   │
    │   └── **Reinforcement Learning**
    │       - Learns using **rewards and penalties**
    │
    │       └── **RLHF (Reinforcement Learning from Human Feedback)**
    │           - Improves LLM responses using **human feedback**
    │
    │
    └── **Model Families / Architectures (WHAT the model is)**
        - Techniques used to **learn patterns**
        │
        ├── **Traditional Machine Learning Models**
        │   - Statistical / mathematical models
        │
        │   ├── **Linear Regression**
        │   │   - Predicts **numeric values**
        │
        │   ├── **Logistic Regression**
        │   │   - Predicts **probabilities/classes**
        │
        │   ├── **Decision Tree**
        │   │   - Makes decisions using **tree-like rules**
        │
        │   ├── **Random Forest**
        │   │   - Combines **multiple decision trees**
        │
        │   └── **KNN (K-Nearest Neighbors)**
        │       - Predicts using **nearest examples**
        │
        │
        └── **Deep Learning**
            - Machine Learning using **multi-layer neural networks**
            │
            └── **Neural Networks**
                - Connected **artificial neurons that learn patterns**
                │
                ├── **CNN (Convolutional Neural Network)**
                │   - Learns **spatial patterns**
                │
                │   Used for:
                │   - **Images**
                │   - **Computer Vision**
                │
                ├── **RNN / LSTM**
                │   - Learns **sequential patterns**
                │
                │   Used for:
                │   - **Text sequences**
                │   - **Time series**
                │
                ├── **GAN (Generative Adversarial Network)**
                │   - Two networks competing:
                │     **Generator vs Discriminator**
                │
                │   Used for:
                │   - **Image/Data generation**
                │
                └── ⭐⭐⭐ **Transformer**
                    - Neural network using **Attention Mechanism**
                    │
                    ├── **Encoder Models**
                    │   - Used for **understanding tasks**
                    │
                    │   Example:
                    │   - BERT
                    │
                    └── **Decoder Models**
                        - Used for **generation tasks**
                        │
                        └── ⭐⭐⭐ **Large Language Models (LLMs)**
                            - Transformer models trained on **massive text/code**
                            │
                            ├── **GPT**
                            │   └── **ChatGPT Application**
                            │
                            ├── **Claude**
                            ├── **Gemini**
                            ├── **Llama**
                            └── **Mistral**
                            │
                            ▼
                    ⭐ **Generative AI Applications**
                            │
                            ├── **Chatbots**
                            ├── **Coding Assistants**
                            ├── **Document Q&A**
                            └── **AI Agents**
                            │
                            ▼
                    ⭐⭐⭐ **RAG (Retrieval Augmented Generation)**
                    - Combines:
                      **LLM + External Knowledge/Data**