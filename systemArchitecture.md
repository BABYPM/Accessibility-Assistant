# System Architecture – Accessibility Assistant

### Overview
Accessibility Assistant is a **multi-layered AI accessibility system** that connects to the device’s operating system, reads UI structures in real time, and converts them into interactive, voice-based guidance.  
It combines **computer vision**, **natural language processing**, and **voice control** to enable smooth, intuitive user interaction across any app.


## Architecture Layers

### 1. **Interface & OS Layer**
- **Components:** Accessibility API hooks (Android, Windows, macOS)
- **Function:** Provides system-level access to UI hierarchies, content descriptions, and user focus events.
- **Purpose:** Allows the assistant to “see” and interpret what’s currently displayed on the screen.

### 2. **AI Interpreter Layer**
- **Components:** TensorFlow.js, OpenCV, ML Kit  
- **Function:** Analyzes visual layouts, detects elements (buttons, text fields, icons), and categorizes content.
- **Purpose:** Converts raw UI data into structured, labeled information for understanding.

### 3. **NLP & Context Engine**
- **Components:** Custom LLM, Whisper API, Dialogflow  
- **Function:** Interprets user voice commands and contextualizes system responses.
- **Purpose:** Converts AI understanding into natural, conversational voice guidance.

### 4. **Speech Processing Layer**
- **Components:** Web Speech API (TTS), Vosk (STT)  
- **Function:** Handles voice input and output — recognizes commands and speaks responses.
- **Purpose:** Provides a two-way conversational bridge between user and system.


### 5. **Learning & Personalization Layer**
- **Components:** SQLite (local), Firestore (cloud)  
- **Function:** Stores user preferences, frequently used apps, and interaction patterns.
- **Purpose:** Enables adaptive learning to tailor future responses and shortcuts.


### 6. **Frontend / User Interface**
- **Framework:** Electron.js / React Native  
- **Function:** Provides visual dashboard and configuration panel for setup and logs.
- **Purpose:** Allows partially sighted users or caregivers to configure settings.

## Data Flow

1. **User speaks a command** → “Open WhatsApp.”  
2. **Speech Recognition Layer** converts voice to text.  
3. **NLP Engine** interprets the intent and sends it to the **AI Interpreter Layer**.  
4. **Interpreter Layer** scans the device UI → identifies the WhatsApp icon.  
5. **Backend** executes navigation via OS accessibility APIs.  
6. **Speech Synthesis** reads confirmation aloud: “Opening WhatsApp.”


## Communication Diagram
```mermaid
graph TD
A[User Voice Input] --> B[Speech-to-Text Engine (Vosk)]
B --> C[NLP Context Engine]
C --> D[AI Interpreter Layer (TensorFlow/OpenCV)]
D --> E[OS Accessibility APIs]
E --> F[Action Execution / App Control]
F --> G[Response Generator (LLM)]
G --> H[Text-to-Speech Output]

Added system architecture documentation

