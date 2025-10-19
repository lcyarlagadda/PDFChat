# Chat with PDFs Application

A Google Colab notebook that allows you to upload PDF files and ask questions about their content using AI models.

## Features

- 📄 Upload and process multiple PDF files
- 🔍 Semantic search using vector embeddings
- 💬 Ask questions in natural language
- 🤖 Support for both GPT-3.5-turbo and open-source models
- 📚 Source citations showing where answers came from

## How to Use

### Option 1: Open in Google Colab

1. Upload the `PDFChat.ipynb` file to your Google Drive
2. Open it with Google Colab
3. Run the cells sequentially from top to bottom
4. Upload your PDF files when prompted
5. Start asking questions!

### Option 2: Direct Upload to Colab

1. Go to [Google Colab](https://colab.research.google.com/)
2. File → Upload notebook
3. Select `PDFChat.ipynb`
4. Run the cells!

## Model Options

### GPT-3.5 (OpenAI)
- **Pros**: Higher quality answers, faster response time
- **Cons**: Requires OpenAI API key (costs money)
- **Setup**: Get an API key from [OpenAI Platform](https://platform.openai.com/api-keys)

### FLAN-T5-XXL (Open Source)
- **Pros**: Completely free, no API key needed, good quality
- **Cons**: May be slower than GPT-3.5
- **Setup**: No setup needed! Just set `USE_OPENAI = False`

## Configuration

In cell #6 (Step 3), you can configure:

```python
USE_OPENAI = False  # Set to True for GPT-3.5, False for open-source
```

## How It Works

1. **PDF Processing**: Extracts text from uploaded PDFs
2. **Text Chunking**: Splits text into manageable chunks (1000 characters with 200 overlap)
3. **Embeddings**: Converts text chunks to vector embeddings using sentence-transformers
4. **Vector Store**: Stores embeddings in FAISS for fast similarity search
5. **Question Answering**: Uses retrieval-augmented generation (RAG) to answer questions based on PDF content

## Example Questions

- "What are the main points discussed in this document?"
- "Can you summarize the findings about [topic]?"
- "What does the document say about [specific subject]?"
- "What are the key recommendations?"
- "Who are the authors and what are their conclusions?"

## Advanced Tips

### Better Answers

Adjust these parameters in the code:

- **chunk_size**: Increase to 1500-2000 for more context per chunk
- **chunk_overlap**: Increase to 300-400 for better continuity
- **k**: Increase number of chunks retrieved (default is 3)
- **temperature**: Lower (0.3-0.5) for more focused answers

### Save Your Vector Store

After processing PDFs, run the "Save Vector Store" cell to save your embeddings. This way, you can reload them later without reprocessing:

```python
# Save
vectorstore.save_local("pdf_vectorstore")

# Load later
vectorstore = FAISS.load_local("pdf_vectorstore", embeddings)
```

## Requirements

All requirements are automatically installed in the first cell:

- `langchain` - LLM orchestration framework
- `pypdf` - PDF text extraction
- `sentence-transformers` - Embeddings
- `faiss-cpu` - Vector store
- `openai` - GPT-3.5 (optional)
- `transformers` - HuggingFace models

## Troubleshooting

### "No API key" error with HuggingFace
- Most models work without an API key. If you get this error, you may need a HuggingFace token for gated models.
- Sign up at [HuggingFace](https://huggingface.co/) and get a token
- Uncomment the token input lines in Step 3

### Slow responses
- Open-source models can be slower than GPT-3.5
- Consider using GPT-3.5 if speed is important
- Or try a smaller model like `google/flan-t5-large` instead of `xxl`

### Poor answer quality
- Make sure your PDFs have extractable text (not just images)
- Try increasing the `k` parameter to retrieve more chunks
- Adjust chunk_size and chunk_overlap for better context

### Out of memory errors
- Colab's free tier has limited RAM
- Try processing fewer PDFs at once
- Use a smaller embedding model

## License

This project is open source and available for educational and commercial use.

## Contributing

Feel free to fork and improve this notebook! Some ideas:
- Add support for more document types (DOCX, TXT, etc.)
- Implement conversation memory for multi-turn chat
- Add a web UI using Gradio or Streamlit
- Support for image extraction from PDFs
- Multi-language support

## Credits

Built with:
- [LangChain](https://www.langchain.com/) - LLM application framework
- [FAISS](https://github.com/facebookresearch/faiss) - Vector similarity search
- [Sentence Transformers](https://www.sbert.net/) - Text embeddings
- [OpenAI](https://openai.com/) - GPT-3.5
- [HuggingFace](https://huggingface.co/) - Open-source models

