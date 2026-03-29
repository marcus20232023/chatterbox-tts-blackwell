# Chatterbox TTS Deployment Summary

## Current Status (2026-03-29)

### ✅ Running Services
```
Container: chatterbox-tts-api-blackwell
- Port: 4123 (host) → 4123 (container)
- Image: docker-chatterbox-tts:latest (24.3GB)
- Status: Running (healthy)
- Uptime: 5 weeks

Container: chatterbox-tts-frontend
- Port: 4321 (host) → 80 (container)
- Status: Running
- Uptime: 5 weeks
```

### 📦 Local Repository Structure
```
/home/marc/chatterbox-tts-turbo/
├── app/                    # FastAPI backend
│   ├── api/
│   │   └── endpoints/
│   │       ├── speech.py   # TTS endpoints
│   │       ├── voices.py   # Voice management
│   │       └── long_text.py # Long text processing
│   ├── core/
│   │   └── tts_model.py    # TTS model wrapper
│   └── ...
├── frontend/               # React + Vite UI
│   ├── src/
│   ├── public/
│   ├── Dockerfile
│   └── package.json
├── docker/
│   ├── docker-compose.yml
│   ├── docker-compose.gpu.yml
│   ├── docker-compose.blackwell.yml
│   ├── Dockerfile
│   └── Dockerfile.blackwell
├── voices/                 # Voice samples
├── models/                 # Model cache
├── data/                   # Long text jobs
├── main.py                 # Entry point
├── pyproject.toml
└── README.md
```

### 🌐 GitHub Repository Comparison

#### Current GitHub Repo: `chatterbox-tts-turbo-server`
- **URL:** https://github.com/marcus20232023/chatterbox-tts-turbo-server
- **Created:** March 15, 2026
- **Last Push:** March 15, 2026
- **Size:** 871 KB
- **Structure:** Simplified Express.js wrapper
  - `server.js` - Express proxy (977 lines)
  - `public/` - Static frontend
  - `package.json` - Dependencies
  - `start.sh` - Startup script

**This does NOT match the full Docker deployment!**

#### What Should Be on GitHub
The GitHub repo should contain the **full Chatterbox TTS API** implementation:
- FastAPI backend with all endpoints
- React/Vite frontend with advanced features
- Docker configurations (GPU, CPU, Blackwell profiles)
- Voice cloning and long text processing
- Complete documentation

### 🎯 Recommended Actions

#### Option 1: Update Existing Repo (Recommended)
```bash
cd /home/marc/chatterbox-tts-turbo
git remote set-url origin git@github.com:marcus20232023/chatterbox-tts-turbo-server.git
git add -A
git commit -m "Full Chatterbox TTS deployment with Docker support"
git push -f origin main
```

#### Option 2: Create New Repo
```bash
cd /home/marc/chatterbox-tts-turbo
git remote set-url origin git@github.com:marcus20232023/chatterbox-tts-api.git
git push -u origin main
```

#### Option 3: Archive and Start Fresh
1. Archive current `chatterbox-tts-turbo-server` on GitHub
2. Create new repo `chatterbox-tts-api` or `chatterbox-tts-docker`
3. Push full implementation

### 📋 Files to Include in GitHub Repo

**Core Files:**
- ✅ `app/` - Full FastAPI backend
- ✅ `frontend/` - React UI (optional, can be submodule)
- ✅ `docker/` - All Docker configs
- ✅ `main.py`, `start.py` - Entry points
- ✅ `pyproject.toml`, `requirements.txt` - Dependencies
- ✅ `README.md` - Full documentation
- ✅ `.env.example` - Configuration template
- ✅ `LICENSE` - MIT License

**Exclude from Git:**
- ❌ `models/` - Too large, use .gitignore
- ❌ `voices/` - User data, use .gitignore
- ❌ `data/` - Runtime data, use .gitignore
- ❌ `.venv/` - Virtual environment
- ❌ `*.wav`, `*.mp3` - Audio files

### 🔧 Docker Deployment Commands

```bash
# Start with GPU support
cd /home/marc/chatterbox-tts-turbo/docker
docker-compose -f docker-compose.gpu.yml up -d

# Start with Blackwell profile
docker-compose -f docker-compose.blackwell.yml up -d

# View logs
docker logs -f chatterbox-tts-api-blackwell
docker logs -f chatterbox-tts-frontend

# Stop services
docker-compose -f docker-compose.blackwell.yml down
```

### 🌍 Access Points
- **API:** http://192.168.1.3:4123
- **Frontend UI:** http://192.168.1.3:4321
- **API Docs:** http://192.168.1.3:4123/docs

### 📊 Next Steps
1. Decide on repo naming strategy
2. Update .gitignore for large files
3. Push full implementation to GitHub
4. Update README with Docker deployment instructions
5. Add GitHub Actions for auto-build Docker images
