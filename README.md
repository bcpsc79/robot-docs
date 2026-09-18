# BCPSC Robot

## 1. Project Overview

### 1.1 Description
The BCPSC Robot is a humanoid robot powered by AI, created by students from Bogura Cantonment Public School and College (BCPSC). Designed to act as an intelligent, interactive representative of the school, it can answer questions about BCPSC using a custom knowledge base, hold bilingual conversations (English and Bangla), recognize familiar faces, make eye contact, and use hand gestures.

### 1.2 Goals & Objectives
- Create an intelligent representative of BCPSC capable of answering questions using school data.
- Develop real skills in AI, robotics, electronics, and 3D design.
- Produce a fully functional humanoid robot to showcase student-led engineering in Bangladesh.
- Demonstrate that advanced robotics and AI are achievable with limited resources and strong determination.

### 1.3 Key Features
- **Bilingual Conversation:** Understands and speaks both English and Bangla natively using offline speech recognition models.
- **Face Recognition & Eye Tracking:** Uses real-time face detection to track faces and simulate natural gaze behavior.
- **Institutional Knowledge (RAG):** Answers questions specifically about BCPSC using a structured Retrieval-Augmented Generation dataset.
- **Natural Physical Expression:** Features a five-fingered hand with 20+ gestures, a physics-based moving jaw, and active eye servos.
- **AI Brain:** Runs a FastAPI microservice using Gemini's function-calling API to dynamically select tools (school lookup, news, hardware control).

---

## 2. Directory Structure & Documentation
This repository is organized into a pure file structure to separate domains. Each folder contains its own `README.md` documenting its architecture, challenges, solutions, learnings, and future improvements:

- **[`/Software/`](./Software/README.md)** - Documentation for the Raspberry Pi 5 vision, speech, AI brain, and API microservice.
- **[`/Firmware/`](./Firmware/README.md)** - Documentation for the C++ code running on the ESP32 and ESP8266 microcontrollers.
- **[`/Electronics/`](./Electronics/README.md)** - Documentation for the veroboard power distribution and voltage schemas.
- **[`/Mechanical Design/`](./Mechanical%20Design/README.md)** - Documentation for the 3D models and hybrid structural design.

---

## 3. Team & Contributions

- **Raiyan Bin Rashid:** Software Lead & AI System Development
- **Jotirmoy Bhowmik:** Software & System Integration
- **Farsad E Hossain:** Hardware Architecture, 3D Design & Mechanical Preparation
- **Naif Bin Nasim:** Hardware & Power Distribution
- **Fairuz Lubna Karim:** Visual Design & Presentation
- **Nahin Rahman:** Hardware Support

---

## 4. Project Timeline (211 Days)

- **Phase 1: Research & Planning (July - Aug 2025)** - Studied EZ-Robot/InMoov, defined robot capabilities, planned the 5-layer architecture.
- **Phase 2: Hardware Development (Aug - Oct 2025)** - Completed 3D modeling, printing, and assembly. Built the veroboard power system.
- **Phase 3: Software & AI Development (Sep - Dec 2025)** - Iterated Brain 1 (Ollama), Brain 2 (RAG & PostSTT), and Brain 3 (Gemini Function Calling API).
- **Phase 4: Integration & Testing (Nov 2025 - Jan 2026)** - Solved the audio feedback loop, connected Raspberry Pi to ESP32 over JSON protocol.
- **Phase 5: Optimization & Final Deployment (Jan - Feb 23, 2026)** - Codebase organized, docs written, ready for Science Fair exhibition.

---

## 5. Overarching Learnings
- **Continuous Coordination:** Because hardware and software were developed simultaneously, decisions in one domain constantly affected the other. The team learned to communicate changes across dependencies quickly and clearly.
- **Handling Leadership Gaps:** The team learned that a complex project doesn't pause when senior direction is unavailable; self-organization and peer-coordination are critical.
- **Ruthless Prioritization:** The requirement to have an exhibition-ready robot by a fixed date imposed discipline, teaching the team to defer non-essential improvements and focus purely on stability.
