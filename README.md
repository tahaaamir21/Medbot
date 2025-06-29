# 🏥 MedBot - Medical Assistant Chatbot

A powerful AI-powered medical assistant chatbot built with Streamlit, LangChain, and FAISS vector storage. MedBot provides accurate medical information by searching through a comprehensive medical knowledge base and citing sources for transparency.

## ✨ Features

- **Medical Knowledge Base**: Powered by medical textbooks and encyclopedias
- **Source Citations**: Every response includes references to source documents
- **Real-time Chat Interface**: Modern, responsive web interface built with Streamlit
- **Fast Retrieval**: Efficient vector search using FAISS
- **Professional UI**: Clean, medical-themed design with smooth animations

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- Hugging Face API token
- Medical PDF documents for the knowledge base

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd medbot
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   Create a `.env` file in the project root:
   ```env
   HF_TOKEN=your_huggingface_token_here
   ```

4. **Prepare your medical documents**
   - Place your medical PDF files in the `data/` directory
   - Supported formats: PDF files
   - Example files: medical textbooks, encyclopedias, research papers

5. **Create the vector database**
   ```bash
   python create_memory.py
   ```

6. **Run the application**
   ```bash
   streamlit run medibot.py
   ```

7. **Open your browser**
   Navigate to `http://localhost:8501` to access the chatbot

## 📁 Project Structure

```
medbot/
├── data/                    # Medical PDF documents
│   ├── Pathoma.pdf
│   └── The_GALE_ENCYCLOPEDIA_of_MEDICINE_SECOND.pdf
├── vectorstore/            # FAISS vector database
│   └── db_faiss/
├── medibot.py             # Main Streamlit application
├── create_memory.py       # Script to create vector database
├── connect_memory_with_llm.py  # Testing script for QA chain
├── requirements.txt       # Python dependencies
└── README.md             # This file
```

## 🔧 Configuration

### Model Settings

The application uses the following default configurations:

- **Embedding Model**: `sentence-transformers/all-MiniLM-L6-v2`
- **Language Model**: `mistralai/Mistral-7B-Instruct-v0.3`
- **Chunk Size**: 500 characters
- **Chunk Overlap**: 50 characters
- **Retrieval**: Top 3 most relevant documents

### Customization

You can modify these settings by editing the constants in the respective files:

- `medibot.py`: Main application settings
- `create_memory.py`: Document processing settings
- `connect_memory_with_llm.py`: LLM and retrieval settings

## 📖 Usage

### Web Interface

1. **Start the application**: Run `streamlit run medibot.py`
2. **Ask questions**: Type medical questions in the chat interface
3. **View responses**: Get detailed answers with source citations
4. **Clear chat**: Use the sidebar button to start a new conversation

### Command Line Testing

For testing the QA system directly:

```bash
python connect_memory_with_llm.py
```

This will prompt you to enter a query and display the response with source documents.

## 🛠️ Technical Details

### Architecture

- **Frontend**: Streamlit web interface
- **Backend**: Python with LangChain framework
- **Vector Database**: FAISS for efficient similarity search
- **Language Model**: Hugging Face hosted Mistral-7B-Instruct
- **Embeddings**: Sentence Transformers for document vectorization

### Data Processing Pipeline

1. **Document Loading**: PDF files are loaded using PyPDFLoader
2. **Text Chunking**: Documents are split into manageable chunks
3. **Embedding Generation**: Text chunks are converted to vectors
4. **Vector Storage**: Embeddings are stored in FAISS database
5. **Retrieval**: Similar chunks are retrieved for user queries
6. **Response Generation**: LLM generates answers based on retrieved context

### Key Components

- **RetrievalQA Chain**: Combines document retrieval with question answering
- **Custom Prompt Template**: Ensures responses are based only on provided context
- **Source Document Tracking**: Maintains references to original documents
- **Error Handling**: Graceful handling of API failures and edge cases

## 🔒 Security & Privacy

- **No Data Storage**: User conversations are not permanently stored
- **Source Transparency**: All responses include source citations
- **Medical Disclaimer**: Clear warnings about not providing medical advice
- **API Security**: Hugging Face tokens are stored securely in environment variables

## ⚠️ Important Disclaimers

**Medical Information Only**: This chatbot is designed for educational and informational purposes only. It does not provide medical advice, diagnosis, or treatment recommendations.

**Professional Consultation**: Always consult with qualified healthcare professionals for medical decisions, diagnosis, and treatment.

**Accuracy**: While the system strives for accuracy, medical information should be verified with authoritative sources.

## 🐛 Troubleshooting

### Common Issues

1. **Vector store not found**
   - Ensure you've run `create_memory.py` first
   - Check that PDF files exist in the `data/` directory

2. **Hugging Face API errors**
   - Verify your `HF_TOKEN` is set correctly in `.env`
   - Check your Hugging Face account has sufficient credits

3. **Memory issues with large documents**
   - Reduce chunk size in `create_memory.py`
   - Consider using smaller documents or splitting large PDFs

4. **Slow response times**
   - Reduce the number of retrieved documents (k parameter)
   - Consider using a faster embedding model

### Performance Optimization

- **Chunk Size**: Smaller chunks (300-500 chars) for precise retrieval
- **Overlap**: 10-20% overlap to maintain context
- **Retrieval Count**: 3-5 documents for balanced speed/accuracy
- **Caching**: Streamlit's `@st.cache_resource` for vector store loading

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.


---

**Remember**: This tool is for educational purposes only. Always consult healthcare professionals for medical advice.
