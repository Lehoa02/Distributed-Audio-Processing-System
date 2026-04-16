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
```

---

## ⚙️ Run Locally

```bash
git clone https://github.com/Lehoa02/CompSci_421_GroupProject.git
cd CompSci_421_GroupProject

python -m venv .venv
source .venv/bin/activate   # or .venv\Scripts\activate on Windows

pip install -r requirements.txt
```

### Update Redis in celery_app.py:
```
REDIS_URL = "redis://<YOUR_HOST>:6379/0"
```

### Start worker:
```
celery -A celery_app.celery_app worker --loglevel=INFO
```

### Run app:
```
python app.py
```

---

## RUN JOBS

### Async (recommended):
```
python async_submit.py
```

### Sync:
```
python submit_jobs.py
```

---

### Demo:
<img width="1512" height="739" alt="Screenshot 2026-04-16 at 4 07 30 PM" src="https://github.com/user-attachments/assets/41a32274-e9dd-4946-8f13-bcff84c0a622" />
<img width="1512" height="739" alt="Screenshot 2026-04-16 at 4 07 30 PM copy" src="https://github.com/user-attachments/assets/bbd5db35-51d6-49b4-a1d4-f3d3ad564ae5" />


