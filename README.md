# 🎙️ Voice Assistant

<p align="center">
  <img src="https://img.icons8.com/fluency/96/microphone.png" width="90" alt="Voice Assistant Logo">
</p>

<p align="center">
  <strong>Intelligent Voice Interaction for Everyday Tasks</strong>
</p>

<p align="center">
  A Python and Flask-based voice assistant that understands natural-language commands,
  performs useful tasks, and responds through both text and voice.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5">
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3">
</p>

<p align="center">
  <strong>Oasis Infobyte Internship (OIBSIP)</strong><br>
  Python Programming · Task 1 — Voice Assistant
</p>

---

## About

Voice Assistant is a Python-based application created to make computer interaction more natural and convenient through voice commands.

Instead of typing every request manually, the user can speak naturally. The application recognizes the voice input, identifies the requested task, performs the appropriate action, and provides the result through the web interface and voice feedback.

The project combines speech recognition, text-to-speech, command processing, APIs, automation, email communication, and a responsive web interface into one application.

---

## Why This Project?

Voice interaction provides a simple and hands-free way to access common computer functions.

The assistant brings several useful tasks together in one place, reducing the need to repeatedly switch between different applications or websites.

It can be useful for:

- Hands-free interaction
- Quick access to information
- Natural-language communication
- Everyday productivity
- Centralized assistant utilities
- Learning and experimenting with voice-based applications

---

## Key Features

| Feature | Description |
|---|---|
| 🎤 Voice Input | Accepts spoken commands through a microphone |
| 🗣️ Voice Response | Provides spoken feedback using text-to-speech |
| 💬 Conversation | Displays user requests and assistant responses |
| 🕐 Date & Time | Provides the current date and time |
| 🔎 Web Search | Searches the web for requested topics |
| 🌤️ Weather | Retrieves live weather information |
| 🧠 Knowledge | Answers supported general and technical questions |
| ⏰ Reminders | Creates timed reminders with audible alerts |
| ✉️ Email | Sends emails through SMTP |
| ⚙️ Custom Commands | Supports configurable commands |
| 🌓 Themes | Supports System, Light, and Dark modes |
| ⚠️ Error Handling | Handles speech and microphone errors gracefully |

---

## How It Works

```text
User Voice
    ↓
Speech Recognition
    ↓
Command Processing
    ↓
Intent Identification
    ↓
Task Execution
    ↓
Response Generation
    ↓
Text + Voice Feedback

## Technology Stack

Backend

Python
Flask

## Frontend

HTML5
CSS3
JavaScript

## Voice
Speech Recognition
Text-to-Speech
Browser Speech Recognition
Browser Speech Synthesis
pyttsx3

## Services
OpenWeatherMap API
SMTP

## Development
Git
GitHub
JSON
Environment Variables
Python Virtual Environment

## Project Structure
VoiceAssistant/
│
├── app.py
├── voice_assistant.py
├── commands.json
├── requirements.txt
├── README.md
├── .gitignore
├── .env.example
├── mic_test.py
│
├── templates/
│   └── index.html
│
└── static/
    ├── style.css
    └── app.js


## File Overview
File	Purpose
app.py	Flask application and backend functionality
voice_assistant.py	Desktop voice-assistant implementation
commands.json	Custom command configuration
templates/index.html	Main web interface
static/style.css	Interface styling and responsive design
static/app.js	Browser interaction and voice functionality
requirements.txt	Python dependencies
.env.example	Environment configuration template
mic_test.py	Microphone testing utility
.gitignore	Prevents local and sensitive files from being committed


## Developer : kunchala shailaja

