# BCPSC Robot

## 1. Project Overview

### 1.1 Project Name
> **BCPSC Robot**

### 1.2 Description
> The BCPSC Robot is a humanoid robot powered by AI, created by students from Bogura Cantonment Public School and College (BCPSC). It is designed to act as an intelligent, interactive representative of the school, capable of answering questions about BCPSC's staff, facilities, and institution using a custom knowledge base. It can hold bilingual conversations (English and Bangla), recognize familiar faces, make eye contact, and use hand gestures.

### 1.3 Goals & Objectives
- Create an intelligent, interactive representative of BCPSC capable of answering questions using school data.
- Develop real skills in areas like AI, robotics, electronics, and 3D design.
- Produce a fully functional humanoid robot for exhibitions to showcase student-led engineering in Bangladesh.
- Demonstrate that advanced robotics and AI are achievable with limited resources and strong determination.

### 1.4 Key Features
- **Bilingual Conversation:** Understands and speaks both English and Bangla natively using offline speech recognition models.
- **Face Recognition & Eye Tracking:** Uses real-time face detection (YuNet) to track faces and simulate natural gaze behavior and blinking.
- **Institutional Knowledge (RAG):** Answers questions specifically about BCPSC (staff, teachers, contact info) using a structured Retrieval-Augmented Generation dataset.
- **Natural Physical Expression:** Features a five-fingered hand with 20+ gestures, a physics-based moving jaw, and eye servos integrated with the AI for expressive communication.
- **AI Brain:** Runs a FastAPI microservice using Gemini's function-calling API to handle school database lookups, news, weather, and dynamic responses.

---

## 2. Requirements & Architecture

### 2.1 Hardware Components
- **Microcontrollers:** 
  - **ESP32 (Main):** Manages eye and jaw servos, processes JSON commands from Raspberry Pi.
  - **ESP8266:** Dedicated controller for the five finger servos.
  - **ESP32 (Drive System):** Controls DC motors for mobility with a wireless joystick interface and hardware deadman switch.
- **Processing:** Raspberry Pi 5 handles all AI, vision, speech recognition, and system coordination tasks.
- **Mechanical:** Custom 3D printed hybrid structure combining EZ-Robot and InMoov platforms.
- **Power System:** Custom veroboard circuit with a series battery setup and buck converters for safe voltage distribution.

### 2.2 Software & Tools
- **Speech Recognition:** Vosk (English) and BanglaSpeech2Text (Bangla) running simultaneously offline.
- **Text-to-Speech:** Coqui TTS (Bangla) and offline TTS models.
- **Vision Tracking:** YuNet ONNX for face detection, OpenCV CSRT tracker.
- **AI & Logic:** FastAPI, Gemini function-calling, local RAG pipeline with sentence-transformer embeddings, Redis caching.
- **Firmware:** C++ using ArduinoJson, ESPAsyncWebServer for REST APIs.

---

## 3. Team Contributions

- **Raiyan Bin Rashid:** Software Lead & AI System Development (AI brain, RAG, Speech, microservice, hand gesture coding).
- **Jotirmoy Bhowmik:** Software & System Integration (Movement control logic, face recognition, hardware-software syncing).
- **Farsad E Hossain:** Hardware Architecture, 3D Design & Mechanical Preparation (Full 3D modeling, printing, structural assembly).
- **Naif Bin Nasim:** Hardware & Power Distribution (Safe power circuits, soldering, component wiring).
- **Fairuz Lubna Karim:** Visual Design & Presentation (Visual finishing for exhibition).
- **Nahin Rahman:** Hardware Support (Assembly, installation, and troubleshooting).

---

## 4. Technical Challenges & Solutions

### 4.1 Hardware Challenges
- **Challenge:** Merging two different open-source humanoid platforms (EZ-Robot & InMoov) into a single cohesive, symmetrical structure.
- **Solution:** Complete redesign of joints and mounting points through iterative 3D printing and fit testing.

### 4.2 Software Challenges
- **Challenge:** Audio feedback loop (microphone picking up the robot's own TTS output).
- **Solution:** Managed timing relationships between TTS playback and STT capture so the system pauses listening while speaking.
- **Challenge:** Misrecognition of Bangla proper nouns (names of teachers).
- **Solution:** Developed a `PostSTTProcessor` using Levenshtein distance, SequenceMatcher, and semantic embeddings to correct text before AI processing.

### 4.3 AI & Integration
- **Challenge:** Preventing the AI from generating incorrect or made-up information about the school.
- **Solution:** Implemented a robust RAG pipeline relying exclusively on local, verified JSON databases before consulting online models.

---

## 5. Directory Structure
This repository organizes the project into the following key domains:

- `/Electronics/` - Power distribution schemas, veroboard layouts, and wiring diagrams.
- `/Firmware/` - C++ code for the ESP32 and ESP8266 microcontrollers.
- `/Mechanical Design/` - 3D models and printing specifications.
- `/Software/` - Raspberry Pi 5 vision, speech, AI brain, and API microservice codebase.

---

## 6. Future Improvements

- **More Natural Movement:** Expand gesture libraries, introduce coordinated upper-body motion, and improve gaze context awareness.
- **Better Speech Quality:** Fine-tune Bangla acoustic models to local accents and implement speaker diarization.
- **Battery Management:** Integrate a battery management system (BMS) with real-time monitoring and hot-swappable packs.
- **Mobile Application:** Develop a dedicated mobile app for non-technical users to control and configure the robot easily.
