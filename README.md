# 🎙️ Voice English Agent

A real-time AI voice agent that listens to your spoken English, converts it into text, improves the wording while preserving your original meaning, and speaks the result back using a natural-sounding English voice.

The goal is to make spoken English sound **clearer, more natural, and more fluent** without changing what the speaker actually intended to say.

---

## ✨ Features

* 🎤 **Real-time speech recognition**

  * Converts microphone input into text using Deepgram Speech-to-Text.
* 🧠 **AI English processing**

  * Corrects grammar and sentence structure.
  * Improves unnatural phrasing.
  * Preserves the speaker's original meaning.
* 🔊 **Natural voice generation**

  * Converts the improved script into high-quality spoken English.
  * Uses Deepgram Text-to-Speech.
* ⚡ **Streaming architecture**

  * Designed for low-latency voice interaction.
  * Processes speech incrementally rather than waiting for an entire conversation.
* 🎭 **Speaking styles**

  * Natural
  * Casual
  * Professional
  * Clear / Easy to understand
* 🇺🇸 **English voice styles**

  * Designed to support different English accents and voices.
* 📝 **Transcript visibility**

  * Shows the original transcript and the improved version.
* 🔄 **Conversation flow**

  * Supports continuous speaking and listening.

---

## 🧠 How It Works

```text
                  🎤 Microphone
                       │
                       ▼
              ┌─────────────────┐
              │   Deepgram STT  │
              │ Speech-to-Text  │
              └────────┬────────┘
                       │
                       ▼
                Raw Transcript
                       │
                       ▼
              ┌─────────────────┐
              │  English Agent  │
              │                 │
              │ Grammar         │
              │ Fluency         │
              │ Natural wording │
              │ Context         │
              └────────┬────────┘
                       │
                       ▼
                 Clean Script
                       │
                       ▼
              ┌─────────────────┐
              │  Deepgram TTS   │
              │  Text-to-Speech │
              └────────┬────────┘
                       │
                       ▼
                  🔊 Voice Output
```

### Example

**You say:**

> Yesterday I go to the store and I buy some things.

**Raw transcript:**

```text
Yesterday I go to the store and I buy some things.
```

**AI-generated script:**

```text
Yesterday, I went to the store and bought a few things.
```

**Voice agent:**

🔊 Speaks the improved sentence naturally.

---

## 🏗️ Architecture

```text
┌───────────────────────────────────────────────┐
│                  Web Client                   │
│                                               │
│  React / Next.js                              │
│  ├── Microphone                               │
│  ├── Live transcript                          │
│  ├── Improved script                          │
│  └── Audio player                             │
└──────────────────────┬────────────────────────┘
                       │
                    WebSocket
                       │
                       ▼
┌───────────────────────────────────────────────┐
│                FastAPI Server                 │
│                                               │
│  ┌──────────────┐                             │
│  │ Audio Stream │                             │
│  └──────┬───────┘                             │
│         ▼                                     │
│  ┌──────────────┐                             │
│  │ Deepgram STT │                             │
│  └──────┬───────┘                             │
│         ▼                                     │
│  ┌──────────────┐                             │
│  │ English Agent│                             │
│  │     + LLM    │                             │
│  └──────┬───────┘                             │
│         ▼                                     │
│  ┌──────────────┐                             │
│  │ Deepgram TTS │                             │
│  └──────┬───────┘                             │
│         ▼                                     │
│      Audio Stream                             │
└──────────────────────┬────────────────────────┘
                       │
                       ▼
                    🔊 User
```

---

## 🛠️ Tech Stack

### Frontend

* React
* TypeScript
* Web Audio API
* WebSocket

### Backend

* Python
* FastAPI
* WebSocket
* AsyncIO

### AI

* Deepgram Speech-to-Text
* LLM for English transformation
* Deepgram Text-to-Speech

---

## 📁 Project Structure

```text
voice-english-agent/
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── App.tsx
│   │
│   ├── package.json
│   └── tsconfig.json
│
├── backend/
│   ├── app/
│   │   ├── agents/
│   │   │   └── english_agent.py
│   │   │
│   │   ├── services/
│   │   │   ├── deepgram_stt.py
│   │   │   └── deepgram_tts.py
│   │   │
│   │   ├── websocket/
│   │   │   └── voice.py
│   │   │
│   │   └── main.py
│   │
│   ├── requirements.txt
│   └── .env.example
│
├── .gitignore
├── README.md
└── LICENSE
```

---

## ⚙️ Environment Variables

Create a `.env` file in the backend:

```env
DEEPGRAM_API_KEY=your_deepgram_api_key
LLM_API_KEY=your_llm_api_key
```

Never commit API keys to Git.

---

## 🚀 Getting Started

### 1. Clone the repository

```cmd
git clone https://github.com/YOUR_USERNAME/voice-english-agent.git
cd voice-english-agent
```

### 2. Start the backend

```cmd
cd backend

python -m venv .venv
.venv\Scripts\activate

pip install -r requirements.txt

uvicorn app.main:app --reload
```

The API will be available at:

```text
http://localhost:8000
```

### 3. Start the frontend

Open another terminal:

```cmd
cd frontend
npm install
npm run dev
```

Then open the URL shown by Vite.

---

## 🎯 English Processing Modes

The English Agent can transform speech according to different modes.

### Natural

Makes the sentence sound like natural everyday English.

```text
Input:
I have went there yesterday.

Output:
I went there yesterday.
```

### Professional

Makes the sentence appropriate for work, meetings, and professional communication.

```text
Input:
I don't think this solution is gonna work.

Output:
I don't think this solution will work.
```

### Casual

Keeps the speech relaxed and conversational.

```text
Input:
I would like to know what you think about it.

Output:
I'd like to hear what you think about it.
```

### Clear

Prioritizes simple and easy-to-understand English.

```text
Input:
We should probably reconsider the implementation
because there are several potential issues.

Output:
We should reconsider the implementation because
there are several issues.
```

---

## 🧠 Agent Behavior

The English Agent should follow these principles:

1. **Preserve meaning**
2. **Do not invent information**
3. **Do not change names, numbers, URLs, or technical terms**
4. **Correct grammatical errors**
5. **Improve unnatural phrasing**
6. **Preserve the speaker's personality**
7. **Avoid unnecessary rewriting**
8. **Return natural spoken English**
9. **Keep the response concise**
10. **Optimize for speech rather than written prose**

The agent should behave as an **English speaking assistant**, not as a traditional translator or text editor.

---

## ⚡ Real-Time Processing

The system is designed around streaming rather than batch processing.

Instead of:

```text
Speak
  ↓
Wait
  ↓
Transcribe everything
  ↓
Process everything
  ↓
Generate everything
  ↓
Play audio
```

the target architecture is:

```text
Speaking
   │
   ├──► Partial STT
   │
   ├──► Sentence boundary
   │
   ├──► LLM processing
   │
   └──► Streaming TTS
             │
             ▼
          🔊 Audio
```

This allows the agent to begin responding before the entire conversation has finished.

---

## 🔐 Privacy

Audio and transcripts may be processed by third-party AI services.

The application should:

* Never expose API keys to the browser.
* Keep provider credentials on the backend.
* Avoid storing raw audio unless explicitly enabled.
* Avoid storing transcripts by default.
* Clearly communicate when external AI services process user audio.

---

## 🗺️ Roadmap

### Phase 1 — MVP

* [ ] Microphone input
* [ ] Deepgram STT
* [ ] LLM English processing
* [ ] Deepgram TTS
* [ ] Basic React interface
* [ ] Audio playback

### Phase 2 — Real-Time Voice

* [ ] WebSocket audio streaming
* [ ] Streaming transcription
* [ ] Sentence detection
* [ ] Streaming TTS
* [ ] Interruption handling
* [ ] Latency measurement

### Phase 3 — Voice Intelligence

* [ ] Multiple English voices
* [ ] Speaking styles
* [ ] Accent selection
* [ ] Adjustable correction level
* [ ] Conversation context
* [ ] Pronunciation feedback
* [ ] Filler-word detection

### Phase 4 — Advanced Agent

* [ ] Voice activity detection
* [ ] Turn-taking
* [ ] Barge-in support
* [ ] Context-aware rewriting
* [ ] Personalized speaking style
* [ ] Conversation memory
* [ ] Real-time pronunciation coaching

---

## 📊 Performance Goals

The primary performance objective is **low perceived latency**.

Target:

```text
Speech
  ↓
STT
  ↓
Processing
  ↓
TTS
  ↓
Audio
```

The system should progressively reduce:

* Speech recognition latency
* LLM processing latency
* TTS time-to-first-byte
* Audio buffering latency
* End-to-end response latency

A useful metric is:

```text
Time to First Audio (TTFA)
```

measured from the end of a detected utterance to the first playable audio chunk.

---

## 🤝 Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Add tests where appropriate.
5. Open a pull request.

```cmd
git checkout -b feature/your-feature
git add .
git commit -m "feat: add your feature"
git push origin feature/your-feature
```

---

## 📄 License

This project is licensed under the MIT License.

---

## ⭐ Vision

The long-term goal is to build a **real-time English voice agent that acts as a bridge between what a person wants to say and how a fluent English speaker would naturally say it**.

It should not simply translate words.

It should understand the speaker's intent, produce natural English, and communicate that meaning through a convincing, fluent voice — while keeping the interaction fast enough to feel like a real conversation.

## 🚧 Project Status

This project is currently under active brainstorming.