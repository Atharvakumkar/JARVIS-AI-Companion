# JARVIS AI Companion (Modified Fork)

A modern AI companion interface built with Flask and Google ADK, featuring a real-time conversational UI, session-based chat handling, and a futuristic split-screen interface inspired by virtual AI assistant systems.

This repository is a modified fork of the original project created by **weimeilin79**. The base implementation and core idea belong to the original author. This version includes UI restructuring, layout modifications, interface refinements, and custom changes made for personal experimentation and learning.

---

## Original Project Credit

Original Repository Owner: **weimeilin79**

This project is not fully built from scratch by me. I forked the original repository and customized multiple parts of the application including frontend structure, layout behavior, and interaction flow.

---

# Table of Contents

* [Architecture](#architecture)
* [Execution Flow](#execution-flow)
* [Project Structure](#project-structure)
* [Tech Stack](#tech-stack)
* [Prerequisites](#prerequisites)
* [Setup & Installation](#setup--installation)
* [Configuration](#configuration)
* [Implementation Details](#implementation-details)
* [Frontend Modifications](#frontend-modifications)
* [Observability & Debugging](#observability--debugging)
* [Author](#author)
* [License](#license)

---

# Architecture

The application follows a lightweight AI web application architecture using Flask as the backend server and Google ADK for conversational agent orchestration.

## Components

* **Flask Backend** — Handles routing, API endpoints, and frontend rendering
* **Google ADK Runner** — Manages conversational AI execution and agent orchestration
* **Character Agent (`character.py`)** — Defines the AI companion personality and root agent configuration
* **Frontend UI** — Split-screen futuristic interface built with HTML, CSS, and JavaScript
* **Session Management** — Maintains isolated conversations using session IDs
* **Async Chat Pipeline** — Processes user messages asynchronously for streaming-like conversational behavior

---

# Execution Flow

```text
User opens web interface
        |
        v
Flask renders index.html
        |
        v
User sends message from frontend UI
        |
        v
POST request sent to /chat endpoint
        |
        v
Flask retrieves or creates session
        |
        v
Google ADK Runner processes message
        |
        v
AI response generated asynchronously
        |
        v
Response returned as JSON
        |
        v
Frontend updates conversation UI
```

---

# Project Structure

```text
JARVIS-AI-Companion/
|
|-- app.py                     # Main Flask application and chat API
|-- character.py              # AI character/agent configuration
|-- requirements.txt          # Python dependencies
|-- init.sh                   # Initialization helper script
|-- setupAPIkey.sh            # API key setup script
|-- set_env.sh                # Environment variable setup
|
|-- templates/
|   |-- index.html            # Main futuristic chat interface
|
|-- static/                   # Static frontend assets
|
|-- skills/                   # Custom skills/extensions for the AI agent
|
|-- .agents/                  # Agent-related configuration files
```

---

# Tech Stack

## Backend

* Python 3.x
* Flask
* AsyncIO
* Google ADK
* Google Generative AI SDK

## Frontend

* HTML5
* CSS3
* Vanilla JavaScript
* Responsive Split-Screen Layout

## AI Components

* InMemoryRunner
* Session-based conversational pipeline
* Character-driven AI architecture

---

# Prerequisites

Before running the application, ensure the following are installed:

* Python 3.10+
* pip
* Virtual Environment support (`venv`)
* Google AI API credentials

---

# Setup & Installation

## 1. Clone the Repository

```bash
git clone <your-forked-repository-url>
cd JARVIS-AI-Companion
```

## 2. Create a Virtual Environment

```bash
python -m venv .venv
```

## 3. Activate the Environment

### Linux / macOS

```bash
source .venv/bin/activate
```

### Windows

```powershell
.venv\Scripts\activate
```

## 4. Install Dependencies

```bash
pip install -r requirements.txt
```

## 5. Configure API Keys

Set your Google AI credentials using environment variables or helper scripts.

Example:

```bash
export GOOGLE_API_KEY="your_api_key"
```

Or use the provided helper scripts:

```bash
bash setupAPIkey.sh
bash set_env.sh
```

## 6. Run the Application

```bash
python app.py
```

The application will start on:

```text
http://127.0.0.1:5000
```

---

# Configuration

## Main Application

The Flask application is initialized inside `app.py`.

Key functionality includes:

* Flask route management
* Session creation and retrieval
* Async message processing
* JSON response handling
* Frontend rendering

## AI Character

`character.py` contains:

* Root agent configuration
* Personality definition
* Agent instructions
* Behavioral customization

---

# Implementation Details

## Asynchronous Chat Handling

The `/chat` endpoint is implemented asynchronously:

```python
@app.route('/chat', methods=['POST'])
async def chat():
```

This enables smoother response handling while interacting with the AI agent.

---

## Session-Based Conversations

Each conversation uses a unique `session_id` allowing multiple isolated chat sessions.

```python
session_id = request.json.get('session_id', 'default_session')
```

---

## Dynamic Session Creation

The backend automatically creates sessions if they do not exist:

```python
await runner.session_service.create_session(...)
```

This prevents manual session initialization.

---

## AI Response Streaming Logic

The Google ADK runner processes messages asynchronously:

```python
async for event in runner.run_async(...)
```

Responses are accumulated dynamically before returning to the frontend.

---

# Frontend Modifications

This modified fork includes several frontend and layout adjustments compared to the original implementation.

## Custom Changes Made

* Redesigned split-screen layout
* Dedicated avatar display panel
* Separate interaction panel for chat input/output
* Reduced whitespace and improved screen utilization
* Futuristic UI styling using gradients and glassmorphism-inspired elements
* Improved responsive behavior
* Refined typography and spacing
* Enhanced visual hierarchy for AI interaction

## UI Characteristics

* Dark futuristic theme
* Circular animated avatar section
* Real-time conversational interface
* Monospace terminal-inspired typography
* Minimal and cinematic design language

---

# Observability & Debugging

The application currently runs using Flask development mode:

```python
app.run(debug=True)
```

This provides:

* Automatic reload during development
* Console error logging
* Traceback visibility for debugging
* Real-time backend logs

For production deployments, a dedicated WSGI server such as Gunicorn is recommended.

---

# Author

## Original Project

* weimeilin79

## Modified Fork & Customizations

* Atharva Kumkar

---

# License

This repository follows the licensing terms of the original project repository.

If redistributing or publishing this modified version publicly, ensure that proper credit is given to the original author and that the original license terms are respected.
