# Software Documentation

## Overview
The BCPSC Robot's software stack operates on a **Raspberry Pi 5** and uses a modular architecture built across several subsystems to manage AI, speech, and computer vision locally.

**Lead Developer:** Raiyan Bin Rashid

## Architecture

### 1. Vision System
- **Face Detection:** Runs YuNet (ONNX) in real-time (at 320x240 resolution for optimal ARM performance).
- **Face Tracking:** Uses OpenCV's CSRT tracker to prevent flicker between detection frames.
- **Identity Matching:** Uses DeepFace with Facenet512 to recognize known faces.
- **Gaze & Pose:** Identifies the target person and tracks facial landmarks to determine gaze direction, smoothly mapping it to servo angles via a critically-damped smoothing filter.

### 2. Speech-to-Text (STT)
- **Bilingual Processing:** Two offline recognizers run in parallel. Vosk handles English, and BanglaSpeech2Text handles Bangla.
- **Audio Management:** Precisely timed audio streaming loops prevent the microphone from capturing the robot's own Text-to-Speech output.

### 3. AI Brain (Generation 3)
- **Microservice:** Built as a FastAPI application utilizing the Gemini function-calling API. 
- **Tool Selection:** The model dynamically selects tools (database lookup, weather, news, or hardware control) rather than relying on pre-coded intent routing.
- **RAG Knowledge Base:** Structured JSON records of school staff and institutional data are indexed by role and name. Sentence-transformer semantic search enables rapid offline answers.
- **Performance:** Redis caching and Server-Sent Events (SSE) streaming ensure low-latency conversational responses.

### 4. Text-to-Speech (TTS)
- **Bangla Voice:** Synthesis uses the Coqui TTS library with `mobassir94/bangla-tts`.
- **Optimization:** Text inputs are cleaned of mixed Unicode. Repeated phrases are cached as hashed audio to provide instant responses.

## Challenges & Solutions
1. **Audio Feedback Loop:** The robot's own TTS was being picked up by its microphone. **Solution:** The timing relationship between the TTS playback and the STT capture was strictly managed to pause listening while speaking.
2. **Misrecognition of Bangla Names:** STT systems consistently misheard proper nouns. **Solution:** Developed a `PostSTTProcessor` using Levenshtein distance, SequenceMatcher, and semantic embeddings to correct text *before* AI processing.
3. **AI Hallucinations:** The AI fabricated answers about BCPSC. **Solution:** Implemented a robust RAG pipeline relying exclusively on verified local JSON databases, combined with heavily tuned confidence thresholds.
4. **Resource Constraints:** Heavy vision tasks caused latency on the ARM hardware. **Solution:** Dropped vision resolution to 320x240 and added the CSRT tracker to maintain continuity.

## Learnings
- **Software Engineering in Production:** Gained experience building robust Python backend services using FastAPI and `asyncio`.
- **RAG & AI Integration:** Learned the practical engineering behind RAG—structuring databases, building embedding indexes, and tuning API fallback logic.

## Future Improvements
- **Better Speech Quality:** Train a custom Bangla acoustic model on local Bogura accents and school-specific vocabulary.
- **Speaker Diarization:** Allow the robot to distinguish between different speakers to maintain coherent multi-person interactions.
- **Mobile Application Control:** Develop a dedicated app to allow non-technical users to access real-time telemetry, update the knowledge base, and trigger a presentation mode for live exhibitions.

## Branches Reference
- `Brain-Update` & `brain-update-try1`: AI logic and FastAPI microservice code.
- `tts`: Text-to-speech implementation.