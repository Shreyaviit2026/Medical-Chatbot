# Medical Chatbot

A medical question-answering chatbot built with Flask, LangChain, Pinecone, and Groq. This RAG (Retrieval-Augmented Generation) application uses a medical knowledge base to provide accurate medical information and answer questions.

## 🚀 Features

- **RAG-based Medical QA**: Retrieval-Augmented Generation for accurate medical information
- **Fast LLM**: Powered by Groq's high-performance LLaMA-3.3-70B model
- **Vector Database**: Pinecone for efficient semantic search
- **Beautiful UI**: Modern, responsive chatbot interface
- **HuggingFace Embeddings**: Uses sentence-transformers for document embeddings
- **PDF Processing**: Automatically processes medical documents from PDFs

## 🛠️ Tech Stack

- **Backend**: Flask 3.1.1
- **LLM**: Groq (LLaMA-3.3-70B-Versatile)
- **Vector DB**: Pinecone
- **Embeddings**: HuggingFace (sentence-transformers/all-MiniLM-L6-v2)
- **LangChain**: RAG chains and document processing
- **Frontend**: Bootstrap 4, jQuery

## 📋 Prerequisites

- Python 3.8+
- Pinecone API Key ([Get it here](https://www.pinecone.io/))
- Groq API Key ([Get it here](https://console.groq.com/))

## 🔧 Installation

1. **Clone the repository**:

```bash
git clone https://github.com/your-username/medi-bot.git
cd medi-bot
```

2. **Create and activate a virtual environment**:

```bash
# Windows
python -m venv mediibot@medi-bot
.\mediibot@medi-bot\Scripts\Activate.ps1

# Linux/Mac
python -m venv mediibot@medi-bot
source mediibot@medi-bot/bin/activate
```

3. **Install dependencies**:

```bash
pip install -r requirements.txt
```

4. **Create a `.env` file** in the root directory:

```env
PINECONE_API_KEY="your_pinecone_api_key_here"
GROQ_API_KEY="your_groq_api_key_here"
HUGGINGFACE_API_KEY="your_huggingface_api_key_here"
```

5. **Prepare your medical documents**:
   - Place your medical PDF files in the `data/` directory
   - Currently configured for: `data/Medical_book.pdf`

## 🏃 Running the Application

### Step 1: Build the Vector Database (First time only)

This processes your PDFs and creates the searchable index:

```bash
python store_index.py
```

This script will:

- Load PDF files from the `data/` directory
- Split documents into chunks
- Generate embeddings using HuggingFace models
- Create a Pinecone index (if it doesn't exist)
- Upload documents to Pinecone vector database

**Note**: This may take several minutes depending on the size of your documents.

### Step 2: Run the Flask Application

```bash
python app.py
```

The application will start on `http://localhost:8080`

### Step 3: Access the Chatbot

Open your browser and navigate to:

```
http://localhost:8080
```

## 📁 Project Structure

```
medi-bot/
├── app.py                 # Flask application and API endpoints
├── store_index.py         # Script to process PDFs and create vector index
├── setup.py              # Package setup configuration
├── requirements.txt      # Python dependencies
├── .env                  # Environment variables (API keys)
├── data/
│   └── Medical_book.pdf  # Medical knowledge base documents
├── src/
│   ├── __init__.py
│   ├── helper.py         # Helper functions (PDF loader, embeddings, text splitter)
│   └── prompt.py         # System prompt for the chatbot
├── templates/
│   └── chat.html         # Chatbot UI template
└── static/
    └── style.css         # Custom styling
```

## 🔑 Configuration

### Pinecone Index Settings

In `store_index.py`, you can customize:

- **Index name**: Default is `"medical-chatbot"`
- **Dimension**: 384 (must match embedding model)
- **Metric**: Cosine similarity
- **Region**: AWS us-east-1 (change as needed)

### LLM Configuration

In `app.py`, you can adjust:

- **Model**: Currently using `llama-3.3-70b-versatile`
- **Retrieval**: Top 3 most relevant chunks (k=3)
- **Temperature**: Can be set for Groq model

### Prompt Customization

Edit `src/prompt.py` to customize the system prompt and chatbot behavior.

## 🧪 API Endpoints

- `GET /` - Serves the chatbot UI
- `POST /get` - Processes user messages and returns AI responses

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the MIT License.

## 👤 Author

**Shreya Keripale**

- Email: shreyakeripale21@gmail.com
- GitHub: [@your-username](https://github.com/your-username)

## 🙏 Acknowledgments

- LangChain for the RAG framework
- Groq for the fast LLM inference
- Pinecone for vector database infrastructure
- HuggingFace for embeddings models

## ⚠️ Disclaimer

**This is a demonstration project and should NOT be used for actual medical diagnoses or decisions. Always consult qualified healthcare professionals for medical advice.**

---

**Note**: Make sure to keep your `.env` file secure and never commit it to version control. Add it to `.gitignore`.
