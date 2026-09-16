# 🎙️ Voice Assistant

<p align="center">
  <strong>Talk naturally. Search, learn, and get things done.</strong>
</p>

<p align="center">
  An intelligent voice-first assistant built with Python, Flask, JavaScript, and speech technologies.
</p>

<p align="center">

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Backend-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6%2B-F7DF1E?style=for-the-badge&logo=javascript&logoColor=000000)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![OIBSIP](https://img.shields.io/badge/Oasis%20Infobyte-OIBSIP-6C63FF?style=for-the-badge)](https://oasisinfobyte.com/)

</p>

<p align="center">
<strong>Oasis Infobyte Internship (OIBSIP)</strong> · Python Programming · Task 1
</p>

---

## Overview

**Voice Assistant** is a voice-driven application that allows users to communicate with an assistant using natural-language commands.

Instead of typing a command or navigating through multiple screens, the user can simply speak a request. The application recognizes the input, identifies the requested action, performs the task, and returns the result through the interface and voice feedback.

The project demonstrates the practical combination of:

**Speech Recognition → Command Processing → Intent Detection → Task Execution → Voice Response**

---

## What Can It Do?

| Capability | What it does |
|---|---|
| 🎤 Voice Input | Captures spoken commands |
| 💬 Conversation | Displays user requests and assistant responses |
| 🔎 Web Search | Searches the web for a requested topic |
| 🌤️ Weather | Retrieves live weather information |
| 🧠 Knowledge | Answers supported general and technical questions |
| ⏰ Reminders | Creates timed reminders with audible alerts |
| ✉️ Email | Sends email through SMTP |
| ⚙️ Custom Commands | Supports configurable commands |
| 🕐 Date & Time | Provides current date and time |
| 🎨 Themes | Supports System, Light, and Dark modes |

---

## How It Works

```text
                    ┌──────────────────┐
                    │       USER       │
                    │  Voice / Action  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Speech Recognition│
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Command Handling │
                    │ Intent Detection │
                    └────────┬─────────┘
                             │
            ┌────────────────┼────────────────┐
            │                │                │
            ▼                ▼                ▼
         Search          Weather          Knowledge
            │                │                │
            └────────────────┼────────────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
          Reminder         Email        Custom Command
              │              │              │
              └──────────────┼──────────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Assistant Result │
                    │   Text + Voice   │
                    └──────────────────┘
