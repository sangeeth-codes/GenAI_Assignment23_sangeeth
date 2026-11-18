# Assignment 23 — OpenAI & Retrieval-Augmented Generation (RAG)

This project demonstrates how to build retrieval-based applications with OpenAI and LangChain. It covers basic OpenAI prompting, document retrieval, advanced retrieval strategies, and a YouTube transcript RAG chatbot.

## Project Overview

The notebook `Assignment23.ipynb` contains the implementation for all 10 assignment tasks.

### Tasks Covered

#### Part 1 — Getting Started with OpenAI
- Configured the OpenAI API key using a `.env` file.
- Initialized the `gpt-4o-mini` chat model.
- Sent a basic prompt and displayed the model response.

#### Part 2 — Retriever-Based RAG
- Retrieved Wikipedia documents using LangChain's `WikipediaRetriever`.
- Created embeddings with OpenAI's `text-embedding-3-small`.
- Stored documents in a FAISS vector store.
- Performed similarity-based retrieval.

#### Part 3 — Advanced Retrieval Strategies
- **MMR retrieval:** Compared maximum marginal relevance retrieval with standard similarity search.
- **Multi-query retrieval:** Used an LLM to generate alternative search queries and retrieve relevant documents.
- **Contextual compression:** Used `ContextualCompressionRetriever` with `LLMChainExtractor` to reduce retrieved content while retaining query-relevant information.

#### Part 4 — YouTube Content RAG Chatbot
- Loaded a YouTube transcript using LangChain's `YoutubeLoader`.
- Split the transcript using `RecursiveCharacterTextSplitter`.
- Generated embeddings and indexed the chunks in FAISS.
- Built a retriever and a prompt-grounded question-answering chatbot.
- Maintained conversation history for follow-up questions.
- Tested factual, follow-up, and out-of-context questions.

## Technologies and Libraries

- Python
- OpenAI API (`gpt-4o-mini`, `text-embedding-3-small`)
- LangChain, LangChain Community, LangChain Classic
- FAISS
- Wikipedia Retriever
- YouTube Loader and YouTube Transcript API
- `python-dotenv`

## Project Structure

```text
GenAI_Assignment23_sangeeth/
├── Assignment23.ipynb
├── README.md
├── .env              # Local API key; do not commit
└── .gitignore
```

The Python virtual-environment folders (`include`, `lib`, `share`, etc.) are local environment files and should not be committed to GitHub.

## Setup and Execution

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd GenAI_Assignment23_sangeeth
```

### 2. Create and activate a virtual environment

For macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install the required packages

```bash
pip install -U langchain langchain-community langchain-openai langchain-classic langchain-text-splitters
pip install -U faiss-cpu wikipedia youtube-transcript-api python-dotenv
```

If the notebook reports a missing package, install it in the same environment used by the Jupyter kernel.

### 4. Configure the OpenAI API key

Create a `.env` file in the project folder:

```text
OPENAI_API_KEY=your_openai_api_key
```

The notebook loads the key with `python-dotenv`. Never paste a real API key into the notebook or commit the `.env` file to GitHub.

### 5. Run the notebook

Open `Assignment23.ipynb` in VS Code or Jupyter and execute the cells in order. The notebook uses an OpenAI API key and may incur API usage charges for chat completions and embedding generation.

## YouTube Video Used

The chatbot uses the transcript from:

[YouTube video](https://youtu.be/dBzMhxa1u94)

The transcript was split into 13 chunks using:
- Chunk size: 1,000 characters
- Chunk overlap: 150 characters

The chunks were embedded with `text-embedding-3-small` and stored in FAISS.

## RAG Chatbot Evaluation

The chatbot was tested with five questions covering:
1. The purpose of Skoda's GOAT event.
2. The cars featured and their shared engine specifications.
3. A follow-up question identifying the sedan.
4. A question about information not available in the video.
5. Why the Kushaq was considered suitable for the racetrack.

The chatbot generally retrieved relevant transcript information, used conversation history for follow-up questions, and indicated when requested information was not available in the transcript.

### Observed Limitation

The transcript contained an apparent duplication in the list of car models. The chatbot repeated the information as it appeared in the transcript. This illustrates that RAG answer quality depends partly on source-document quality. Generated answers should also be checked against the retrieved context.

## Security

- Keep `.env` out of version control.
- Never upload API keys, tokens, or other secrets.
- Do not commit virtual-environment folders or notebook checkpoint files.

## Author

Sangeeth
