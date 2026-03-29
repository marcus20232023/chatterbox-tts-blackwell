# 🚀 Blackwell Deployment Guide

This guide covers deploying Chatterbox TTS API on **NVIDIA Blackwell architecture** (RTX 50XX series) GPUs.

## 📋 Prerequisites

- **GPU:** NVIDIA RTX 5080 / 5090 (Blackwell architecture)
- **Driver:** NVIDIA Driver 550+ with CUDA 12.4+
- **Docker:** Docker Engine 24.0+ with NVIDIA Container Toolkit
- **Memory:** 32GB+ RAM recommended (24GB+ GPU VRAM)

## 🐳 Quick Start (Blackwell)

```bash
# Clone the repository
git clone https://github.com/marcus20232023/chatterbox-tts-blackwell.git
cd chatterbox-tts-blackwell

# Copy Docker-optimized environment
cp .env.example.docker .env

# Start with Blackwell profile (GPU + Frontend)
docker compose -f docker/docker-compose.blackwell.yml --profile frontend up -d

# Watch initialization logs
docker logs -f chatterbox-tts-api-blackwell
```

## 🔧 Docker Compose Profiles

| Profile | Command | Use Case |
|---------|---------|----------|
| **Blackwell** | `docker-compose.blackwell.yml` | RTX 5080/5090 (recommended) |
| GPU | `docker-compose.gpu.yml` | Generic NVIDIA GPU |
| UV + GPU | `docker-compose.uv.gpu.yml` | Faster builds with uv |
| CPU | `docker-compose.cpu.yml` | No GPU available |

## 📊 Performance Benchmarks (RTX 5080)

| Text Length | Generation Time | Real-time Factor |
|-------------|----------------|------------------|
| 50 chars | ~1.2s | 0.3x |
| 200 chars | ~3.5s | 0.4x |
| 1000 chars | ~12s | 0.5x |

*Real-time factor < 1.0 means faster than real-time speech*

## 🌐 Access Points

After deployment:
- **Frontend UI:** http://localhost:4321
- **API Endpoint:** http://localhost:4123
- **API Docs:** http://localhost:4123/docs
- **Alternative Docs:** http://localhost:4123/redoc

## 🔍 Verify Deployment

```bash
# Check container status
docker ps | grep chatter

# Test API health
curl http://localhost:4123/health

# Test speech generation
curl -X POST http://localhost:4123/v1/audio/speech \
  -H "Content-Type: application/json" \
  -d '{"input": "Blackwell deployment successful!"}' \
  --output test.wav

# Play test audio
ffplay -nodisp -autoexit test.wav
```

## 🛠️ Troubleshooting

### GPU Not Detected
```bash
# Verify NVIDIA Container Toolkit
docker run --rm --gpus all nvidia/cuda:12.4.0-base-ubuntu22.04 nvidia-smi

# Should show your GPU. If not, reinstall toolkit:
# https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html
```

### Out of Memory
```bash
# Reduce chunk size in .env
MAX_CHUNK_LENGTH=200
LONG_TEXT_CHUNK_SIZE=2000

# Restart containers
docker compose -f docker/docker-compose.blackwell.yml down
docker compose -f docker/docker-compose.blackwell.yml up -d
```

### Model Download Fails
```bash
# Clear model cache
docker volume rm chatterbox-tts-api_chatterbox-models

# Restart to re-download
docker compose -f docker/docker-compose.blackwell.yml up -d
```

## 📝 Environment Variables (Blackwell)

```bash
# Server
PORT=4123
HOST=0.0.0.0

# TTS Parameters
EXAGGERATION=0.5
CFG_WEIGHT=0.5
TEMPERATURE=0.8

# Blackwell Optimization
DEVICE=cuda
MAX_CHUNK_LENGTH=280
LONG_TEXT_CHUNK_SIZE=2500

# Memory Management
MEMORY_CLEANUP_INTERVAL=5
CUDA_CACHE_CLEAR_INTERVAL=3
ENABLE_MEMORY_MONITORING=true

# Paths (Docker)
MODEL_CACHE_DIR=/cache
VOICE_LIBRARY_DIR=/voices
LONG_TEXT_DATA_DIR=/data/long_text_jobs
```

## 🔄 Updates

```bash
# Pull latest changes
git pull origin main

# Rebuild and restart
docker compose -f docker/docker-compose.blackwell.yml down
docker compose -f docker/docker-compose.blackwell.yml up -d --build
```

## 📊 Monitoring

```bash
# GPU usage
watch -n 1 nvidia-smi

# Container logs
docker logs -f chatterbox-tts-api-blackwell

# API statistics
curl http://localhost:4123/v1/status/statistics

# Memory status
curl http://localhost:4123/memory
```

## 🎯 Production Tips

1. **Use persistent volumes** - Models and voices are cached in Docker volumes
2. **Enable GPU monitoring** - Track VRAM usage with `nvidia-smi`
3. **Tune chunk sizes** - Balance latency vs. quality for your use case
4. **Set up log rotation** - Prevent disk space issues from logs
5. **Use reverse proxy** - Add Nginx/Traefik for SSL and load balancing

## 📚 Additional Resources

- [Full API Documentation](README.md)
- [Voice Library Management](docs/VOICE_LIBRARY_MANAGEMENT.md)
- [Streaming API Guide](docs/STREAMING_API.md)
- [Multilingual Support](docs/MULTILINGUAL.md)
- [Memory Management](docs/MEMORY_MANAGEMENT.md)

---

**Deployed on:** RTX 5080 Blackwell  
**Maintained by:** @marcus20232023  
**License:** MIT
