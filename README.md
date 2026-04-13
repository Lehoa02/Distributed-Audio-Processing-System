# 🎧 Distributed Audio Processing System

A scalable system for processing audio files in parallel using Celery workers, Redis, and a Flask API. The application extracts audio features such as spectral centroid, bandwidth, and loudness, and visualizes them through a web interface.

---

## 🚀 Project Overview

This project processes `.wav` audio files using a distributed architecture:

- **Flask** → Handles file uploads and API requests  
- **Celery** → Executes audio processing tasks in parallel  
- **Redis** → Acts as the message broker  
- **Async uploader (aiohttp + asyncio)** → Sends multiple files concurrently  
- **Frontend** → Displays extracted audio features  

The system is designed to improve performance by enabling asynchronous uploads and parallel task execution.

📄 Based on project documentation: :contentReference[oaicite:0]{index=0}

---

## ⚙️ Key Features

- Parallel audio processing using Celery workers  
- Asynchronous file uploads for improved throughput  
- Feature extraction (DFT-based):
  - Spectral centroid
  - Bandwidth
  - Loudness
- Real-time dashboard visualization  
- Scalable architecture using message queues  

---

## 🧠 System Design

### Architecture Choice (CAP Theorem)

We prioritize:

- **Availability**
- **Partition Tolerance**

This means:
- The system continues accepting uploads even if workers or Redis are temporarily unavailable  
- Tasks are processed once the connection is restored  

---

### Database & Messaging

- **Redis** → message broker for Celery  
- **Kafka (conceptual / optional)** → event streaming and data pipeline  

The system avoids strict relational constraints and focuses on high-throughput data processing.

---

### Async Processing

Originally, the system used synchronous uploads.  
It was upgraded to:

```bash
aiohttp + asyncio
