# 🌍 Multilingual Multi-Agent Chat Application for Workplace

> Breaking down language barriers in global enterprises with AI-powered translation and intelligent assistance

A sophisticated LLM-based chat application designed to address language barriers and workplace inefficiencies in large, multilingual organizations.This application leverages multi-agent architecture to provide seamless communication across language boundaries.

---

## 📸 Project Overview

### Screenshots & Demo

![Application UI](https://i.postimg.cc/gJ5j0sYL/Screenshot-2024-09-01-at-12-25-24-AM.png)

**[View Full Demo Video](https://youtu.be/_i8WKbTXojM)**

---

## ✨ Features

### 🌐 Multilingual Translation
- **Real-time Language Support**: Users can read and write in their preferred languages
- **Intelligent Translation**: Language-specific agents automatically translate messages
- **Seamless Communication**: Break down language barriers across teams

### 🤖 Aya - Workplace AI Assistant
- **Integrated Assistant**: Available in all chats for common workplace tasks
- **Context-Aware**: Understands organizational processes and workflows
- **Always Available**: Provides instant support across the platform

### 📚 RAG-Based Q&A System
- **Knowledge Base Integration**: Responds to queries using relevant document context
- **Smart Retrieval**: Pulls information from internal knowledge base
- **Accurate Answers**: Provides context-backed responses to user questions

### 📖 Documentation-on-the-Go
- **Save to Knowledge Base**: Convert chat messages into documentation
- **Continuous Learning**: Build your knowledge base from real interactions
- **Reusable Content**: Aya learns and reuses documented solutions

### 📊 Smart Summarization
- **Quick Catch-Up**: Summarize entire chat threads instantly
- **Action Item Tracking**: Automatically identifies assigned tasks
- **Team Efficiency**: Helps teams stay synchronized

---

## 🛠️ LLM Backend Options

The application supports three different LLM backends to power the agentic workflow:

| Backend | Model | Use Case |
|---------|-------|----------|
| **Claude** | Anthropic Claude | Best performance, especially for translations |
| **ChatGPT** | OpenAI GPT-4/3.5 | Good balance of performance and cost |
| **Aya** | [Cohere Aya 23 8B](https://huggingface.co/CohereForAI/aya-23-8B) | Open-source alternative |

**Performance Ranking**: Claude > ChatGPT > Aya

---

## 🚀 Quick Start Guide

### Prerequisites
- Python 3.8+
- pip or conda
- API keys for selected LLM backend (Claude, OpenAI, or Hugging Face)

### Installation & Setup

#### 1. **Clone the Repository**
```bash
git clone https://github.com/Panth19/Multilingual-Chatbot.git
cd Multilingual-Chatbot
```

#### 2. **Set Python Path**
Update your `PYTHONPATH` to include the repository directory:

```bash
export PYTHONPATH="$(pwd):$PYTHONPATH"
```

**Windows (Command Prompt):**
```cmd
set PYTHONPATH=%cd%;%PYTHONPATH%
```

**Windows (PowerShell):**
```powershell
$env:PYTHONPATH = "$(Get-Location);$env:PYTHONPATH"
```

#### 3. **Install Dependencies**
```bash
pip install -r requirements.txt
```

#### 4. **Configure User List**
Create a `user_list.csv` file with users and their preferred languages:

```csv
user_id,username,preferred_language,department
1,john_doe,en,Engineering
2,marie_dupont,fr,Marketing
3,carlos_lopez,es,Sales
4,yuki_tanaka,ja,Product
```

**Supported Fields:**
- `user_id`: Unique identifier for the user
- `username`: Display name in the chat
- `preferred_language`: Language code (en, fr, es, ja, etc.)
- `department`: User's department (optional)

#### 5. **Prepare Knowledge Base**
Create a directory for your knowledge base documents:

```bash
mkdir -p ml_chat/playground/data
```

**Supported Document Formats:**
- PDF (.pdf)
- Text (.txt)
- Markdown (.md)
- Word (.docx)

#### 6. **Start the Server**
Launch the FastAPI server with your configuration:

```bash
python ml_chat/server/start_server.py \
  -u user_list.csv \
  --data_directory ./ml_chat/playground/data \
  --llm claude
```

**Available Options:**
- `-u, --users`: Path to user list CSV file (required)
- `--data_directory`: Path to knowledge base directory (optional)
- `--llm`: LLM backend selection: `openai`, `claude`, or `aya` (default: `openai`)
- `--port`: Server port (default: 8000)
- `--host`: Server host (default: 127.0.0.1)

#### 7. **Access the Chat UI**
Open your browser and navigate to the HTML files under the `App UI` directory:

```
http://localhost:8000/ui
```

Or open the HTML files directly in your browser:
```bash
# Navigate to the UI directory
cd ml_chat/ui
# Open index.html in your browser
```

---

## ⚙️ Configuration Guide

### Environment Variables

Create a `.env` file in the root directory:

```env
# LLM Configuration
OPENAI_API_KEY=your_openai_key_here
CLAUDE_API_KEY=your_claude_key_here
HUGGINGFACE_API_KEY=your_huggingface_key_here

# Server Configuration
SERVER_HOST=127.0.0.1
SERVER_PORT=8000

# Application Settings
LOG_LEVEL=INFO
DEBUG_MODE=False
```

### LLM Backend Setup

#### Claude (Recommended)
```bash
python ml_chat/server/start_server.py \
  -u user_list.csv \
  --llm claude \
  --data_directory ./ml_chat/playground/data
```
Requires: `CLAUDE_API_KEY` environment variable

#### ChatGPT
```bash
python ml_chat/server/start_server.py \
  -u user_list.csv \
  --llm openai \
  --data_directory ./ml_chat/playground/data
```
Requires: `OPENAI_API_KEY` environment variable

#### Aya
```bash
python ml_chat/server/start_server.py \
  -u user_list.csv \
  --llm aya \
  --data_directory ./ml_chat/playground/data
```
Requires: `HUGGINGFACE_API_KEY` environment variable

### Knowledge Base Configuration

The knowledge base system uses RAG (Retrieval-Augmented Generation) to enhance responses:

1. **Add Documents**: Place your documents in the `--data_directory`
2. **Supported Formats**: PDF, TXT, MD, DOCX
3. **Indexing**: Documents are automatically indexed on server startup
4. **Updates**: Add new documents without restarting (with watch mode enabled)

---

## 📁 Project Structure

```
Multilingual-Chatbot/
├── ml_chat/
│   ├── server/
│   │   ├── start_server.py          # Main server entry point
│   │   ├── agent_workflow.py        # Multi-agent orchestration
│   │   └── config.py                # Server configuration
│   ├── agents/
│   │   ├── translator_agent.py      # Language translation logic
│   │   ├── qa_agent.py              # RAG-based Q&A
│   │   └── summarizer_agent.py      # Content summarization
│   ├── ui/
│   │   ├── index.html               # Main chat interface
│   │   ├── styles.css               # UI styling
│   │   └── app.js                   # Frontend logic
│   └── playground/
│       └── data/                    # Knowledge base directory
├── user_list.csv                    # User configuration
├── requirements.txt                 # Python dependencies
└── README.md                        # This file
```

---

## 🔄 Workflow & Architecture

### Multi-Agent System Flow

```
User Message
    ↓
[Input Processor] → Detect Language
    ↓
[Translator Agent] → Translate to Default Language (if needed)
    ↓
[Main Agent Dispatcher]
    ├─→ [QA Agent] → Retrieve from Knowledge Base
    ├─→ [Task Agent] → Handle Workplace Tasks
    └─→ [Summarizer] → Generate Summaries
    ↓
[Response Translator] → Translate to User's Preferred Language
    ↓
User Response
```

### Key Components

1. **Translator Agents**: Language-specific agents for multilingual support
2. **Main Dispatcher**: Routes queries to appropriate agents
3. **RAG System**: Retrieves context from knowledge base for accurate Q&A
4. **Response Generator**: Creates context-aware responses
5. **UI Layer**: Web-based interface for chat interactions

---

## 📖 Usage Examples

### Example 1: Multilingual Team Chat

```
User 1 (English): "What's the deployment process?"
↓
Aya (RAG-based): Retrieves deployment documentation
↓
User 2 (French) receives: "Quel est le processus de déploiement?"
```

### Example 2: Save Documentation

```
User: "Here's how we handle authentication..."
↓
Aya: "Would you like me to save this to our knowledge base?"
↓
Aya adds to knowledge base
↓
Future queries can reference this documentation
```

### Example 3: Smart Summarization

```
User: "Summarize today's discussion"
↓
Aya: Analyzes conversation
↓
Response: 
  - Summary of key points
  - Action items assigned
  - Deadlines and owners
```

---

## 🐛 Troubleshooting

### Issue: PYTHONPATH Not Set Correctly
**Solution:**
```bash
# Verify PYTHONPATH includes the repo
echo $PYTHONPATH
# Should include your repository path
```

### Issue: Server Won't Start
**Check:**
- Is port 8000 available? Try: `lsof -i :8000`
- Are all dependencies installed? `pip install -r requirements.txt`
- Is the user_list.csv file valid? Check CSV format

### Issue: LLM Responses Are Slow
**Solutions:**
- Try switching to a faster backend (Claude is fastest)
- Ensure knowledge base documents are not too large
- Check API rate limits for your LLM provider

### Issue: Translation Accuracy Issues
**Solutions:**
- Ensure user preferred languages are correctly set in user_list.csv
- Use Claude backend for best translation quality
- Add more context to messages for better translations

---

## 🤝 Contributing

We welcome contributions! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 🙏 Acknowledgments

- Built as part of the [Aya Expedition](https://www.youtube.com/watch?v[...])
- Thanks to [Cohere for AI](https://www.cohere.com/) for the Aya model
- Special thanks to the multilingual NLP community

---

## 📞 Support & Contact

For questions, issues, or suggestions:
- **Issues**: [GitHub Issues](https://github.com/Panth19/Multilingual-Chatbot/issues)
- **Discussions**: [GitHub Discussions](https://github.com/Panth19/Multilingual-Chatbot/discussions)
- **Email**: Contact the project maintainer

---

## 📚 Additional Resources

- [Aya Model Documentation](https://huggingface.co/CohereForAI/aya-23-8B)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Retrieval-Augmented Generation (RAG) Guide](https://arxiv.org/abs/2005.11401)
- [Multi-Agent Systems in LLMs](https://arxiv.org/abs/2308.03688)

---

**Last Updated**: July 5, 2026

⭐ If you find this project helpful, please consider giving it a star!
