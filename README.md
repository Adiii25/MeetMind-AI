# MeetMind AI

**An AI-Powered Meeting Intelligence Platform**

MeetMind AI transforms audio recordings of meetings, interviews, and podcasts into searchable, speaker-labelled transcripts. It combines automatic speech recognition, speaker diarization, transcript alignment, vector search, and Retrieval-Augmented Generation (RAG) to make conversations easier to understand and explore.

Upload an audio recording, let the AI process the conversation, and ask natural-language questions to retrieve information from the meeting.

---

## Features

- **Automatic Transcription** — Converts audio recordings into text using Whisper.
- **Speaker Diarization** — Identifies different speakers and labels their conversation segments using Pyannote Audio 3.1.
- **Speaker Alignment** — Combines transcription and speaker timestamps into structured, speaker-labelled conversations.
- **Multi-Level RAG Indexing** — Stores document, segment, and chunk-level information in ChromaDB.
- **AI-Powered Q&A** — Ask natural-language questions about recorded conversations.
- **Streaming Responses** — Generates answers token by token.
- **Persistent Chat History** — Maintains conversation sessions using SQLite.
- **Transcript Editing** — Edit speaker names and transcript text.
- **Incremental Reindexing** — Rebuilds the search index after transcript modifications.
- **Meeting Knowledge Retrieval** — Retrieves relevant information with speaker and timestamp references.
- **Downloadable Transcripts** — Export aligned JSON, transcription results, and diarization data.
- **Authentication** — JWT-based authentication for REST endpoints.
- **Modern Web Interface** — Next.js, React, and Tailwind CSS frontend.
- **REST API and WebSockets** — FastAPI backend for processing and real-time communication.
- **Command-Line Interface** — Supports batch processing, indexing, and querying.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [System Architecture](#2-system-architecture)
3. [Technology Stack](#3-technology-stack)
4. [Repository Structure](#4-repository-structure)
5. [Installation](#5-installation)
6. [Environment Variables](#6-environment-variables)
7. [Running the Application](#7-running-the-application)
8. [Processing Pipeline](#8-processing-pipeline)
9. [RAG and Query System](#9-rag-and-query-system)
10. [API Documentation](#10-api-documentation)
11. [Docker Deployment](#11-docker-deployment)
12. [Troubleshooting](#12-troubleshooting)
13. [Development Roadmap](#13-development-roadmap)
14. [Running Tests](#14-running-tests)
15. [Acknowledgements and License](#15-acknowledgements-and-license)

---

## 1. Project Overview

MeetMind AI is a self-hosted meeting intelligence system designed to transform unstructured audio conversations into structured and searchable knowledge.

### Core Capabilities

**1. Speech Recognition**

Uses OpenAI Whisper to convert spoken conversations into written transcripts.

**2. Speaker Identification**

Uses Pyannote Audio to identify different speakers and determine when each person speaks.

**3. Transcript Alignment**

Combines speech recognition output with speaker diarization timestamps to generate speaker-labelled conversation segments.

**4. Intelligent Knowledge Retrieval**

Uses ChromaDB and sentence embeddings to organize meeting information into multiple searchable levels.

**5. Retrieval-Augmented Generation**

Uses RAG to retrieve relevant meeting information before generating answers through a language model.

**6. Interactive Meeting Assistant**

Allows users to ask questions about processed recordings and receive answers based on the conversation.

**7. Meeting Management**

Provides transcript editing, chat history, downloadable outputs, and meeting-level information management.

---

## 2. System Architecture

### Full Processing Pipeline

```text
             AUDIO UPLOAD
                   |
                   v
          SPEECH TRANSCRIPTION
                Whisper
                   |
                   v
          SPEAKER DIARIZATION
                Pyannote
                   |
                   v
           TRANSCRIPT ALIGNMENT
                   |
                   v
          STRUCTURED TRANSCRIPT
                   |
                   v
             RAG INDEXING
                ChromaDB
                   |
                   v
          VECTOR EMBEDDINGS
                   |
                   v
          SEARCHABLE KNOWLEDGE
                   |
                   v
            AI QUESTION ANSWERING
                   |
                   v
             FINAL RESPONSE
```

### Query Processing Pipeline

```text
        User Question
              |
              v
       Query Embedding
              |
              v
       Vector Retrieval
              |
              v
        MMR Reranking
              |
              v
       Context Selection
              |
              v
        LLM Generation
              |
              v
       Streaming Response
```

### Main Components

| Component | Responsibility |
|---|---|
| Whisper | Speech-to-text conversion |
| Pyannote | Speaker diarization |
| Alignment Service | Combines transcript and speaker information |
| ChromaDB | Vector database |
| Sentence Transformers | Text embeddings |
| RAG Pipeline | Context retrieval and answer generation |
| FastAPI | Backend API |
| Next.js | Frontend application |
| SQLite | Persistent application data |

---

## 3. Technology Stack

### Artificial Intelligence and Machine Learning

- Python
- OpenAI Whisper
- Pyannote Audio
- Sentence Transformers
- Large Language Models
- Retrieval-Augmented Generation
- Natural Language Processing

### Backend

- Python
- FastAPI
- WebSockets
- JWT Authentication
- SQLite

### Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS

### Vector Database and Storage

- ChromaDB
- SQLite
- JSON / JSONL

### Development and Deployment

- Git
- GitHub
- Docker
- Docker Compose
- FFmpeg
- Pytest
- Jest
- Playwright

---

## 4. Repository Structure

```text
MeetMind-AI/
│
├── meetbot/
│   ├── adapters/
│   │   ├── llm/
│   │   └── transcribers/
│   │
│   ├── services/
│   │   ├── transcriber.py
│   │   ├── diarizer.py
│   │   ├── aligner.py
│   │   ├── formatters.py
│   │   ├── query_service.py
│   │   │
│   │   └── rag/
│   │       ├── indexer.py
│   │       ├── chunker.py
│   │       ├── retriever.py
│   │       ├── reranker.py
│   │       ├── selector.py
│   │       └── summarizer.py
│   │
│   ├── workers/
│   ├── web/
│   ├── db/
│   ├── utils/
│   ├── cli.py
│   └── config.py
│
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   ├── components/
│   │   └── lib/
│   │
│   ├── tests/
│   └── package.json
│
├── tests/
├── models/
├── results/
├── scripts/
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── pyproject.toml
├── .env.example
├── .gitignore
├── LICENSE
└── README.md
```

*Note: This structure describes the inherited project layout. Update it to match the actual directories and files in your repository.*

---

## 5. Installation

### Prerequisites

| Requirement | Description |
|---|---|
| Python 3.12 | Backend environment |
| Node.js | Frontend development |
| npm | Frontend dependencies |
| FFmpeg | Audio processing |
| Git | Version control |
| Hugging Face Account | Access to gated models |
| CUDA | Optional GPU acceleration |

### Install FFmpeg

**Windows**

Install FFmpeg and add its `bin` directory to your system PATH.

**Ubuntu / Debian**

```bash
sudo apt update
sudo apt install ffmpeg
```

**macOS**

```bash
brew install ffmpeg
```

### Clone the Repository

```bash
git clone https://github.com/Adiii25/MeetMind-AI.git

cd MeetMind-AI
```

### Create a Python Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```powershell
venv\Scripts\activate
```

Activate it on Linux/macOS:

```bash
source venv/bin/activate
```

### Install PyTorch

CPU version:

```bash
pip install torch torchvision torchaudio
```

For NVIDIA GPU acceleration, install the appropriate PyTorch CUDA build from the official PyTorch installation instructions.

### Install Backend Dependencies

```bash
pip install -r requirements.txt
```

Install the project in editable mode:

```bash
pip install -e .
```

### Install Frontend Dependencies

```bash
cd frontend

npm install
```

---

## 6. Environment Variables

Create a `.env` file in the project root.

```env
# Hugging Face Authentication
HF_API_TOKEN=your_huggingface_token

# Transcription Configuration
TRANSCRIPTION_BACKEND=huggingface
WHISPER_MODEL=openai/whisper-large-v3

# Speaker Diarization
DIARIZATION_MODEL=pyannote/speaker-diarization-3.1

# Embedding Configuration
EMBEDDING_MODEL=./models/sarashina-embedding-v1-1b

# LLM Configuration
USE_LOCAL_LLM=false
HF_MODEL=deepseek-ai/DeepSeek-V3-0324
HF_PROVIDER=auto

# Vector Database
VECTOR_DB_PATH=./db/sample

# RAG Configuration
RAG_TOP_K=4
RAG_RECALL_N=50
RAG_MAX_CONTEXT_CHUNKS=6

# Application Configuration
WEB_HOST=0.0.0.0
WEB_PORT=8080
```

Never commit your actual `.env` file or API credentials to GitHub.

The above values reflect the inherited configuration. Consult the actual project configuration for supported variables and defaults.

---

## 7. Running the Application

### Start Backend

From the project root:

```bash
python -m meetbot.cli serve
```

Backend:

```text
http://localhost:8080
```

### Start Frontend

Open another terminal:

```bash
cd frontend

npm install

npm run dev
```

Frontend:

```text
http://localhost:3000
```

### Using the CLI

Process a meeting recording:

```bash
python -m meetbot.cli run path/to/meeting.mp3
```

Query an indexed meeting:

```bash
python -m meetbot.cli query db/abcd1234 "What were the main action items?"
```

For available options:

```bash
python -m meetbot.cli --help
```

---

## 8. Processing Pipeline

### Stage 1: Audio Transcription

Whisper converts audio into text segments.

The system supports local and Hugging Face inference configurations.

### Stage 2: Speaker Diarization

Pyannote Audio identifies different speakers and produces timestamped speaker intervals.

Example:

```text
00:00 - 00:10 | Speaker 1
00:10 - 00:18 | Speaker 2
00:18 - 00:25 | Speaker 1
```

### Stage 3: Transcript Alignment

The alignment service combines transcription and diarization outputs.

Example:

```json
[
  {
    "start": 0.0,
    "end": 10.0,
    "speaker": "Speaker 1",
    "text": "Welcome everyone to the meeting."
  },
  {
    "start": 10.0,
    "end": 18.0,
    "speaker": "Speaker 2",
    "text": "Let's discuss the project."
  }
]
```

### Stage 4: RAG Indexing

The transcript is converted into searchable vector representations.

The indexing system organizes information into:

- Document-level information
- Speaker-level segments
- Smaller overlapping text chunks

This enables retrieval at different levels of detail.

---

## 9. RAG and Query System

MeetMind AI uses Retrieval-Augmented Generation to answer questions using information from processed meeting recordings.

### How RAG Works

1. The user enters a question.
2. The question is converted into an embedding.
3. Relevant transcript information is retrieved from ChromaDB.
4. Relevant results are reranked.
5. The selected information is passed to an LLM.
6. The LLM generates an answer using the retrieved context.

### Example

**User Question:**

"What were the main decisions taken during the meeting?"

**AI Assistant:**

The retrieved meeting context is used to generate an answer describing the decisions discussed.

### Retrieval Levels

| Level | Purpose |
|---|---|
| Document | Broad meeting-level information |
| Segment | Speaker-specific conversation |
| Chunk | Detailed factual retrieval |

The system also supports streaming responses through WebSockets.

---

## 10. API Documentation

The FastAPI backend exposes REST and WebSocket endpoints.

### REST API

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/jobs/{id}/status` | Get processing status |
| POST | `/api/jobs/{id}/query` | Ask questions about a meeting |
| GET | `/api/jobs/{id}/download` | Download processed output |
| POST | `/api/jobs/{id}/reindex` | Rebuild the vector index |
| POST | `/api/jobs/{id}/cancel` | Cancel a processing job |
| POST | `/api/jobs/{id}/restart` | Restart a failed job |

### WebSocket API

| Endpoint | Description |
|---|---|
| `/ws/jobs/{id}` | Real-time processing progress |
| `/ws/chat/{id}` | Streaming AI responses |

For complete request parameters and response formats, refer to the backend API implementation.

---

## 11. Docker Deployment

The project includes Docker configuration for containerized deployment.

### Build Backend

```bash
docker build -t meetmind-backend .
```

### Build Frontend

```bash
cd frontend

docker build -t meetmind-frontend .
```

### Run Using Docker Compose

```bash
docker compose up -d
```

View logs:

```bash
docker compose logs -f
```

Stop services:

```bash
docker compose down
```

---

## 12. Troubleshooting

### FFmpeg Not Found

Install FFmpeg and ensure it is available through your system PATH.

### Hugging Face Authentication Error

Check your `HF_API_TOKEN` and ensure you have accepted the relevant model access conditions.

### Pyannote Model Download Failure

Verify access to the Pyannote speaker diarization model on Hugging Face.

### CUDA Out of Memory

Try reducing embedding batch size or switching model execution to CPU.

### Frontend Connection Error

Ensure the backend is running on port 8080 and that the frontend API configuration points to the correct address.

### Missing Python Dependencies

Activate your virtual environment and reinstall dependencies:

```bash
pip install -r requirements.txt
```

---

## 13. Development Roadmap

The following improvements are planned for future development.

- [ ] Improve transcription accuracy and processing efficiency.
- [ ] Implement automatic meeting summarization.
- [ ] Extract important decisions from conversations.
- [ ] Generate meeting action items and deadlines.
- [ ] Improve speaker identification and transcript alignment.
- [ ] Add multilingual meeting support.
- [ ] Improve RAG retrieval quality and relevance.
- [ ] Add retrieval evaluation and answer faithfulness metrics.
- [ ] Implement cross-meeting semantic search.
- [ ] Build an advanced meeting analytics dashboard.
- [ ] Add exportable meeting reports.
- [ ] Improve application performance and scalability.

*Roadmap items are planned features, not currently completed functionality.*

---

## 14. Running Tests

### Backend Tests

```bash
python -m pytest tests/ -v
```

### Frontend Tests

```bash
cd frontend

npm run test
```

### End-to-End Tests

```bash
npm run test:e2e
```

Test availability depends on the test configuration and installed dependencies.

---

## 15. Acknowledgements and License

MeetMind AI builds upon the open-source **MeetBot** project by SIMETRAL55.

Original repository:

https://github.com/SIMETRAL55/MeetBot

The inherited implementation and applicable copyright notices are retained in accordance with the original MIT license.

MeetMind AI is being developed further with additional functionality, improvements, testing, and documentation.

**License:** MIT (subject to the retained original license and applicable notices).

---

## Project Status

**MeetMind AI — Under Active Development**

Building smarter ways to understand, search, and interact with conversations.

Developed by **Aditya Naruka**.

GitHub: https://github.com/Adiii25
