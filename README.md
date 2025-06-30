# YouTube Chatbot Assistant 🤖

> An AI-powered Chrome extension that lets you chat with YouTube videos using advanced language models

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/python-v3.8+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.68+-green.svg)](https://fastapi.tiangolo.com/)
[![Chrome Extension](https://img.shields.io/badge/Chrome-Extension-blue.svg)](https://developer.chrome.com/docs/extensions/)

## 🌟 Overview

YouTube Chatbot Assistant is a Chrome extension that transforms how you interact with YouTube videos. Simply ask questions about any video you're watching, and get intelligent, context-aware answers powered by Google's Gemini AI. Perfect for students, researchers, content creators, and anyone who wants to quickly understand video content.

## ✨ Features

- **🎯 Smart Q&A**: Ask natural language questions about any YouTube video
- **🚀 Real-time Processing**: Get instant answers using video transcripts
- **🎨 Beautiful UI**: Modern, responsive interface with smooth animations
- **🔒 Privacy First**: All processing happens locally and through secure APIs
- **📱 Easy to Use**: Simple Chrome extension popup interface
- **🌐 Universal Support**: Works with all YouTube videos that have transcripts
- **⚡ Fast Performance**: Optimized for quick response times
- **🎪 Multiple Formats**: Supports regular videos, YouTube Shorts, and embedded videos

## 🏗️ Architecture

```
YouTube Chatbot Assistant/
├── 🖥️ Backend (FastAPI)
│   ├── AI Processing (Gemini)
│   ├── Transcript Extraction
│   └── RESTful API
├── 🔌 Chrome Extension
│   ├── Content Script
│   ├── Popup Interface
│   └── Background Processing
└── 🤖 AI Integration
    ├── LangChain Framework
    ├── Google Gemini AI
    └── Smart Prompt Engineering
```

## 🚀 Quick Start

### Prerequisites

- **Python 3.8+** installed on your system
- **Google Cloud API Key** with Gemini AI access
- **Chrome browser** (or Chromium-based browser)
- **Git** for cloning the repository

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/youtube-chatbot-assistant.git
cd youtube-chatbot-assistant
```

### 2. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Create environment file
echo "GOOGLE_API_KEY=your_google_api_key_here" > .env
```

### 3. Get Google AI API Key

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. Copy the key and replace `your_google_api_key_here` in your `.env` file

### 4. Start the Backend Server

```bash
python main.py
```

The server will start at `http://127.0.0.1:8000`

### 5. Install Chrome Extension

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable **Developer mode** (toggle in top-right corner)
3. Click **Load unpacked**
4. Select the `extension` folder from this project
5. The extension icon should appear in your Chrome toolbar

### 6. Start Chatting!

1. Navigate to any YouTube video
2. Click the extension icon in your toolbar
3. Type your question and press Enter
4. Get instant AI-powered answers!

## 📖 Usage Examples

### Basic Usage
```
User: "What is the main topic of this video?"
AI: "This video discusses advanced machine learning techniques, 
     specifically focusing on transformer architectures and their 
     applications in natural language processing."
```

### Detailed Questions
```
User: "Can you explain the third point mentioned around minute 5?"
AI: "Around the 5-minute mark, the speaker discusses gradient descent 
     optimization, explaining how it helps neural networks learn by 
     adjusting weights based on error calculations..."
```

### Summary Requests
```
User: "Give me a 3-point summary of this tutorial"
AI: "Here's a 3-point summary:
     1. Introduction to React hooks and their benefits
     2. Practical examples of useState and useEffect
     3. Best practices for managing component state"
```

## 🛠️ API Documentation

### Base URL
```
http://127.0.0.1:8000
```

### Endpoints

#### `GET /`
Health check endpoint
```json
{
  "status": "healthy",
  "message": "YouTube Chatbot API is running"
}
```

#### `POST /ask`
Ask a question about a YouTube video
```json
{
  "video_id": "dQw4w9WgXcQ",
  "question": "What is this video about?"
}
```

**Response:**
```json
{
  "answer": "This video is Rick Astley's famous song 'Never Gonna Give You Up'...",
  "video_id": "dQw4w9WgXcQ",
  "transcript_length": 1542
}
```

#### `GET /test/{video_id}`
Test if a video has available transcripts
```json
{
  "video_id": "dQw4w9WgXcQ",
  "transcript_available": true,
  "transcript_length": 1542,
  "preview": "Never gonna give you up, never gonna let you down..."
}
```

## 🔧 Configuration

### Backend Configuration
Edit environment variables in `backend/.env`:
```env
GOOGLE_API_KEY=your_google_api_key_here
```

### Extension Configuration
The extension automatically detects YouTube video IDs from:
- Standard URLs: `youtube.com/watch?v=VIDEO_ID`
- Short URLs: `youtu.be/VIDEO_ID`
- Shorts: `youtube.com/shorts/VIDEO_ID`
- Embedded videos: `youtube.com/embed/VIDEO_ID`

## 📂 Project Structure

```
youtube-chatbot-assistant/
├── 📁 backend/
│   ├── main.py              # FastAPI application
│   ├── requirements.txt     # Python dependencies
│   └── .env                 # Environment variables
├── 📁 extension/
│   ├── manifest.json        # Extension configuration
│   ├── popup.html          # Extension popup UI
│   ├── popup.js            # Popup functionality
│   ├── content.js          # Content script for YouTube
│   └── styles.css          # UI styling
├── .gitignore              # Git ignore rules
└── README.md               # This file
```

## 🔍 Technical Details

### AI Processing Pipeline
1. **Video ID Extraction**: Automatically detects YouTube video ID from current tab
2. **Transcript Retrieval**: Uses YouTube Transcript API to get video captions
3. **AI Processing**: Processes user questions using Google Gemini AI via LangChain
4. **Response Generation**: Returns contextual answers based on video content

### Key Technologies
- **Backend**: FastAPI, Python 3.8+
- **AI**: Google Gemini AI, LangChain
- **Extension**: Chrome Extension Manifest V3
- **UI**: Modern CSS with glassmorphism design
- **APIs**: YouTube Transcript API, Google AI API

### Security Features
- Environment variable protection for API keys
- CORS middleware for secure cross-origin requests
- Input validation and error handling
- No data persistence (privacy-focused)

## 🚨 Troubleshooting

### Common Issues

#### "Backend server not running"
**Solution**: Make sure the FastAPI server is running on port 8000
```bash
cd backend
python main.py
```

#### "No transcript found"
**Solution**: Some videos don't have transcripts. Try with videos that have captions enabled.

#### "Invalid API key"
**Solution**: Check your Google AI API key in the `.env` file
```bash
# Check if .env file exists and contains your key
cat backend/.env
```

#### Extension not working
**Solution**: 
1. Refresh the YouTube page
2. Reload the extension in `chrome://extensions/`
3. Check browser console for errors (F12)

### Debug Mode

Enable debug logging in the backend:
```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

## 🤝 Contributing

We welcome contributions! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Make your changes** and test thoroughly
4. **Commit your changes**: `git commit -m 'Add amazing feature'`
5. **Push to the branch**: `git push origin feature/amazing-feature`
6. **Open a Pull Request**

### Development Setup
```bash
# Install development dependencies
pip install -r requirements-dev.txt

# Run tests (if available)
pytest

# Format code
black backend/
```

## 📋 Roadmap

- [ ] **Multi-language support** - Support for non-English videos
- [ ] **Video summaries** - Generate automatic video summaries
- [ ] **Bookmark system** - Save interesting Q&A pairs
- [ ] **Export functionality** - Export conversations to text/PDF
- [ ] **Voice input** - Ask questions using voice commands
- [ ] **Advanced search** - Search within video transcripts
- [ ] **Playlist support** - Ask questions across multiple videos

## 🎯 Use Cases

### 📚 Education
- **Students**: Quickly understand lecture content and get clarifications
- **Teachers**: Create quiz questions based on educational videos
- **Researchers**: Extract key information from academic presentations

### 💼 Professional
- **Content Creators**: Analyze competitor videos and trends
- **Marketers**: Extract insights from marketing videos
- **Developers**: Get quick explanations from coding tutorials

### 🎨 Entertainment
- **Movie Reviews**: Get detailed analysis of review videos
- **Gaming**: Understand gameplay mechanics and strategies
- **Music**: Learn about songs, artists, and music theory

## 🙏 Acknowledgments

- **Google AI** for providing the Gemini AI API
- **YouTube** for the Transcript API
- **LangChain** for the excellent AI framework
- **FastAPI** for the amazing web framework
- **Chrome Extensions** team for the robust extension platform

## 📞 Support & Contact

- **Email**: jha2004ayush@gmail.com

## 🌟 Show Your Support

If this project helped you, please consider:
- ⭐ **Starring** the repository
- 🐛 **Reporting** any bugs you find
- 💡 **Suggesting** new features
- 🤝 **Contributing** to the codebase
- 📢 **Sharing** with others who might find it useful

---

<div align="center">
  <p><strong>Made with ❤️ for the YouTube community by Ayush Jha</strong></p>
  <p>
    <a href="#top">Back to Top ⬆️</a>
  </p>
</div>
