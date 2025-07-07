# **Echoes: The Emotional Audio Time Machine**

Capture short ambient moments tied to emotion. Revisit them when you need to remember who you are.

---

## ⚙️ Stack Overview

| Layer         | Tech                                        |
| ------------- | ------------------------------------------- |
| Frontend      | React Native (Expo) or Vite + React         |
| API           | FastAPI or AWS Lambda + API Gateway         |
| Storage       | S3 (audio), DynamoDB (metadata)             |
| Auth          | Amazon Cognito                              |
| Notifications | EventBridge + SNS                           |
| Infra         | AWS CDK (Python/TypeScript)                 |
| AI (Phase 2)  | Bedrock (Claude/Whisper), OpenAI/AssemblyAI |

---

## 🖥 App Features

### 🎛 Main Screens

* **Home:** "I feel \_\_\_" → resurfaces matching memory
* **Record:** Pick emotion → record 10–30s clip
* **Echo List:** Scrollable + filterable memory archive
* **Playback:** Minimal full-screen player (emotion, time, place)

### 🧠 Backend Flow

1. Record audio in app
2. Upload to S3 via presigned URL
3. Metadata saved to DynamoDB

### Key Endpoints

* `POST /echoes/init-upload`
* `POST /echoes`
* `GET /echoes`
* `GET /echoes/random`

---

## 🗃 Data Model (DynamoDB)

```json
{
  "userId": "abc123",
  "echoId": "uuid-1234",
  "emotion": "Calm",
  "timestamp": "...",
  "s3Url": "...",
  "location": { "lat": ..., "lng": ... },
  "tags": ["river", "kids"],
  "transcript": "...",
  "detectedMood": "joy"
}
```

---

## ☁️ Infra Notes

* **S3:** Stores audio by user + echo ID
* **DynamoDB:** Metadata store with `userId` as partition key
* **Cognito:** Auth + scoped S3 access
* **Lambdas:** Upload, save, fetch, random

---

## 🧠 AI Enrichment (Phase 2)

| Feature                        | Tool               |
| ------------------------------ | ------------------ |
| Transcription                  | Whisper/Transcribe |
| Mood tagging                   | Claude             |
| Smart audio categorization     | AssemblyAI         |
| Emotional recall via search    | RAG + Pinecone     |
| Memory narration / stylization | Claude prompts     |


