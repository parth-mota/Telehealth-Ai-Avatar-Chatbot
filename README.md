# Telehealth AI Avatar

A comprehensive n8n workflow that provides AI-powered telehealth consultations via Telegram, featuring specialist agents for triage, symptom analysis, diagnosis, treatment planning, mental health counseling, and prescription management.

## Features

- 🤖 **AI Doctor Avatar**: Dr. Sarah – a caring and experienced telehealth physician  
- 📱 **Telegram Integration**: Accepts text, audio, images, and documents  
- 🎯 **Specialized AI Agents**:  
  - Triage Specialist – Emergency assessment  
  - Symptom Analyzer – Pattern recognition and symptom analysis  
  - Diagnosis Assistant – Differential diagnosis  
  - Treatment Planner – Care plan creation  
  - Mental Health Counselor – Compassionate mental health support  
  - Prescription Manager – Medication safety and interactions  
- 🗣️ **Voice Response**: Text-to-speech via ElevenLabs  
- 🎥 **Video Avatar**: AI-generated video responses (D-ID or HeyGen)  
- 💬 **Conversational Memory**: Maintains patient context across conversations  
- 📄 **Multi-modal Input**: Handles text, voice messages, images, and PDF documents  

## Prerequisites

- [n8n](https://n8n.io/) – Workflow automation tool  
- API Keys for:  
  - [OpenAI](https://platform.openai.com/) – Audio generation  
  - [Google Gemini](https://ai.google.dev/) – LLM and multimodal AI  
  - [Telegram Bot](https://core.telegram.org/bots) – Messaging interface  
  - [ElevenLabs](https://elevenlabs.io/) – Text-to-speech  
  - [D-ID](https://www.d-id.com/) or [HeyGen](https://www.heygen.com/) – Video avatar (optional)  

## Setup Instructions

### 1. Import Workflow

1. Open n8n  
2. Click on **Workflows** → **Import from File**  
3. Select `Telehealth-AI-Avatar-SAFE.json`  

### 2. Configure Credentials

You'll need to set up the following credentials in n8n:

#### Telegram Bot

1. Create a bot via [@BotFather](https://t.me/botfather) on Telegram  
2. Copy the bot token  
3. In n8n: **Credentials** → **New** → **Telegram API**  
4. Paste your bot token  

#### Google Gemini

1. Get API key from Google AI Studio  
2. In n8n: **Credentials** → **New** → **Google PaLM API / Gemini**  
3. Enter your API key  

#### OpenAI (for audio generation)

1. Get API key from the OpenAI platform  
2. In n8n: **Credentials** → **New** → **OpenAI API**  
3. Enter your API key  

#### ElevenLabs (for text-to-speech)

1. Get API key from ElevenLabs  
2. In n8n: **Credentials** → **New** → **ElevenLabs API**  
3. Enter your API key  

#### D-ID or HeyGen (optional, for video avatars)

**D-ID:**

1. Sign up at D-ID  
2. Get your API key  
3. Update the HTTP Request nodes with your credentials  

**HeyGen:**

1. Sign up at HeyGen  
2. Get your API key  
3. Update the HTTP Request nodes with your credentials  

### 3. Update Workflow Configuration

After importing, update these nodes with your credentials:

- **Telegram Trigger** – Select your Telegram credential  
- **Get a file**, **Get a file1**, **Get a file2**, **Send an audio file**, **Send a video** – Select Telegram credential  
- **Google Gemini Chat Model** (all instances) – Select Google Gemini credential  
- **Analyze an image**, **Transcribe a recording** – Select Google Gemini credential  
- **Generate Audio** – Select OpenAI credential  
- **Convert text to speech** – Select ElevenLabs credential  
- **d-id request**, **d-id status** – Update with your D-ID API key  
- **HTTP Request4**, **HTTP Request5** – Update with your HeyGen API key  

### 4. Activate Workflow

1. Click the **Active** toggle in the top-right  
2. Your Telegram bot is now live  

## Usage

1. Start a chat with your Telegram bot  
2. Send messages describing symptoms or ask health questions  
3. The AI will analyze and respond with appropriate medical guidance  
4. Supported inputs:  
   - **Text messages** – Ask questions, describe symptoms  
   - **Voice messages** – Speak your symptoms  
   - **Images** – Send photos for analysis  
   - **Documents (PDF)** – Upload medical reports  

## Workflow Structure

### Input Processing

- **Telegram Trigger** – Receives messages  
- **patient context** – Extracts patient info and message type  
- **Switch** – Routes to appropriate handler (text / audio / image / document)  

### Content Extraction

- **Analyze an image** – Gemini vision for image analysis  
- **Transcribe a recording** – Gemini audio transcription  
- **Extract from PDF File** – PDF text extraction  

### AI Processing

- **Appointment System** (Main Agent) – Dr. Sarah coordinates specialist tools  
- **Triage Specialist Agent** – Emergency assessment  
- **Symptom Analyzer** – Symptom pattern analysis  
- **Diagnosis Assistant** – Identifies likely conditions  
- **Treatment Planner** – Creates care plans  
- **Mental Health Counselor** – Mental health support  
- **Prescription Manager** – Medication safety  

### Response Generation

- **Clear output** – Formats AI response  
- **Convert text to speech** – ElevenLabs TTS  
- **d-id request / d-id status** – D-ID avatar video (optional)  
- **HTTP Request4 / HTTP Request5** – HeyGen avatar video (optional)  
- **Send a video** – Delivers video response to Telegram  

### Memory

- **Chat Memory Manager** – Manages conversation history  
- **Simple Memory** (multiple instances) – Context for each specialist  

## Customization

### Modify Dr. Sarah's Personality

Edit the system message in the **Appointment System** node to change the AI doctor's personality, response style, or medical guidelines.

### Add New Specialist Agents

1. Create a new **Agent Tool** node  
2. Define the tool description and system message  
3. Connect a **Google Gemini Chat Model** and **Simple Memory**  
4. Link it to the main **Appointment System** agent  

### Change Voice

Update the `voice_id` in the **Convert text to speech** node or **d-id request** node to use different ElevenLabs voices.

### Adjust Response Mode

Set `mode` to:

- `"text"` – Text-only responses  
- `"audio"` – Audio responses  

Enable video nodes for avatar video responses if you want video.

## Environment Variables

For production deployments, use environment variables instead of hardcoded credentials:

