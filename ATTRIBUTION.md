# Attribution & Credits

This project builds upon the excellent work of several open source contributors:

## 🙏 Primary Inspiration

### [travisvn/chatterbox-tts-api](https://github.com/travisvn/chatterbox-tts-api)
- **Original Author:** @travisvn
- **License:** MIT
- **Contribution:** This project is a fork and enhancement of the original Chatterbox TTS API
- **Key Features Inherited:** FastAPI structure, OpenAI compatibility, Docker deployment, voice cloning

### [Resemble AI - Chatterbox](https://github.com/resemble-ai/chatterbox)
- **Original Creator:** Resemble AI
- **License:** MIT
- **Contribution:** Core TTS model and architecture
- **Model Used:** `chatterbox-tts` package (multilingual fork)

### [chatterbox-multilingual](https://github.com/travisvn/chatterbox-multilingual)
- **Maintainer:** @travisvn (fork of ResembleAI's original)
- **License:** MIT
- **Contribution:** Multilingual support (22 languages)
- **Current Version:** `exp` branch

## 🚀 What's Different in This Fork

This repository (`marcus20232023/chatterbox-tts-blackwell`) includes:

1. **Blackwell GPU Optimization** - RTX 5080/5090 specific Docker profiles
2. **Enhanced Frontend** - React + Vite UI with streaming support
3. **Voice Library Management** - Upload, store, and reuse custom voices by name
4. **Long Text Processing** - Automatic chunking for texts up to 100K characters
5. **Memory Management** - Advanced CUDA cache clearing and monitoring
6. **Production Deployment** - Battle-tested on RTX 5080 for 5+ weeks

## 📦 Current Model Status

### Using: `chatterbox-multilingual` (NOT Turbo yet)
```
chatterbox-tts @ git+https://github.com/travisvn/chatterbox-multilingual.git@exp
```

**Why not Turbo?**
- `ResembleAI/chatterbox-turbo` is optimized for speed but lacks multilingual support
- `chatterbox-multilingual` provides 22 languages with voice cloning
- **Future:** Turbo support planned (see TODO below)

### Model Comparison

| Feature | Multilingual (Current) | Turbo (Planned) |
|---------|----------------------|-----------------|
| Languages | 22 | English only |
| Speed | ~0.4x real-time | ~0.1x real-time |
| Voice Cloning | ✅ Yes | ✅ Yes |
| Quality | High | Very High |
| GPU Memory | ~8GB | ~12GB |

## 🔮 Future Plans

### Chatterbox Turbo Integration
- [ ] Add Turbo model support as optional backend
- [ ] Benchmark Turbo vs Multilingual performance
- [ ] Add model selection via environment variable
- [ ] Support Turbo's enhanced voice cloning

### Acknowledgments
- [travisvn/chatterbox-tts-api](https://github.com/travisvn/chatterbox-tts-api) - Original API structure
- [ResembleAI/chatterbox](https://github.com/resemble-ai/chatterbox) - Core TTS model
- [devnen/Chatterbox-TTS-Server](https://github.com/devnen/Chatterbox-TTS-Server) - Inspiration for web UI

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

**Note:** The underlying Chatterbox TTS model is also MIT licensed (Resemble AI).

---

**Maintained by:** @marcus20232023  
**Deployed on:** RTX 5080 Blackwell  
**Location:** Regina, Saskatchewan, Canada 🇨🇦
