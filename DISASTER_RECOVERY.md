# Christensen & Sons — Disaster Recovery & Stack Configuration

> **If you lose the TensorDock VM, this document has everything you need to rebuild from scratch in under 30 minutes.**

---

## 1. TensorDock VM Specifications

| Component | Value |
|---|---|
| **Provider** | TensorDock |
| **Location** | Tier 3 Data Center, Prague, Czech Republic |
| **Instance ID** | `c2b77dbe-22fc-43de-a002-26ae86e0b896` |
| **Public IP** | `80.188.223.202` |
| **CPU** | 14 cores |
| **GPU** | 1× NVIDIA A100 80GB (Compute 8.0) |
| **RAM** | 128 GiB |
| **Disk** | 300 GiB SSD |
| **NVIDIA Driver** | 565.57.01 |
| **OS** | Ubuntu (Python 3.12.3) |

### Port Forwards

| External Port | Internal Port | Service |
|---|---|---|
| `10232` | `11434` | **Ollama API** (OpenAI-compatible) |
| `10233` | `8000` | **ChromaDB** (vector database) |
| `10262` | `22` | **SSH** |
| `10263` | `8888` | Jupyter (unused) |

### SSH Access
```bash
ssh -p 10262 -i ~/.ssh/id_ed25519 user@80.188.223.202
```

---

## 2. Ollama Configuration

### Service File: `/etc/systemd/system/ollama.service`
```ini
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/local/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

[Install]
WantedBy=default.target
```

### Override: `/etc/systemd/system/ollama.service.d/override.conf`
```ini
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="OLLAMA_KEEP_ALIVE=24h"
Environment="OLLAMA_MAX_LOADED_MODELS=5"
Environment="OLLAMA_NUM_PARALLEL=2"
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
Environment="OLLAMA_GPU_OVERHEAD=2147483648"
```

### Key Settings Explained
- `OLLAMA_KEEP_ALIVE=24h` — Models stay loaded in VRAM for 24 hours (no cold starts)
- `OLLAMA_MAX_LOADED_MODELS=5` — Up to 5 models in VRAM simultaneously
- `OLLAMA_NUM_PARALLEL=2` — 2 concurrent inference requests per model
- `OLLAMA_FLASH_ATTENTION=1` — Flash attention enabled (faster, less VRAM)
- `OLLAMA_KV_CACHE_TYPE=q8_0` — 8-bit KV cache (saves ~40% context VRAM)
- `OLLAMA_GPU_OVERHEAD=2147483648` — 2 GB reserved for system/CUDA overhead

---

## 3. Model Stack (12 Models)

### Active Agent Models (5 chat + 1 embedding)

| Spoof Name | True Model | Renderer | Context | VRAM Est. | Paperclip Agent |
|---|---|---|---|---|---|
| `gpt-4o` | **Nemotron 30B** (nemotron-3-nano) | nemotron-3-nano | **131072** (128K) | ~26 GB | Clara Muse (CEO) |
| `gpt-4-turbo` | **Qwen3.6-35B-A3B** | qwen3.5 | **65536** (64K) | ~25 GB | Viktor Forge (CTO) |
| `gpt-4` | **Gemma 4 E2B** | gemma4 | **4096** (4K) | ~6 GB | Niko Relay (CD) |
| `code-reviewer` | **Qwen3 8B** | qwen3 (chat template) | default | ~5 GB | Marcus Christensen (CDS) |
| `gpt-4o` *(shared)* | **Nemotron 30B** *(same endpoint)* | nemotron-3-nano | 128K | 0 extra | Elias Redstone (CLO) |
| `nomic-embed-text` | **nomic-embed-text** | — | **8192** | ~0.3 GB | Shared RAG/ChromaDB |

### Additional Models (loaded but not assigned to Paperclip agents)

| Name | True Model | Size | Notes |
|---|---|---|---|
| `gpt-4o-mini` | Qwen3.6-35B-A3B (same blob as gpt-4-turbo) | 23 GB | Duplicate alias |
| `deepseek-r1:14b` | DeepSeek R1 14B | 9 GB | Reasoning model |
| `gemma4:e4b` | Gemma 4 E4B | 9.6 GB | Larger Gemma variant |
| `nemotron-3-nano` | Nemotron 30B (base, no alias) | 24 GB | Base model |
| `qwen3:8b` | Qwen3 8B (base, no alias) | 5.2 GB | Base model |
| `qwen3.6:35b-a3b` | Qwen3.6-35B-A3B (base, no alias) | 23 GB | Base model |

### Total Disk: ~75 GB for all model weights

---

## 4. Model Parameter Details

### gpt-4o (Clara Muse — Nemotron 30B)
```
RENDERER nemotron-3-nano
PARSER nemotron-3-nano
PARAMETER num_ctx 131072
PARAMETER temperature 1
PARAMETER top_p 1
```

### gpt-4-turbo (Viktor Forge — Qwen3.6-35B-A3B)
```
RENDERER qwen3.5
PARSER qwen3.5
PARAMETER num_ctx 65536
PARAMETER presence_penalty 1.5
PARAMETER repeat_penalty 1
PARAMETER temperature 1
PARAMETER top_k 20
PARAMETER top_p 0.95
PARAMETER min_p 0
```

### gpt-4 (Niko Relay — Gemma 4 E2B)
```
RENDERER gemma4
PARSER gemma4
PARAMETER num_ctx 4096
PARAMETER temperature 1
PARAMETER top_k 64
PARAMETER top_p 0.95
```

### code-reviewer (Marcus Christensen — Qwen3 8B)
```
Uses standard Qwen3 chat template with tool calling support
(im_start/im_end token format with XML tool_call tags)
```

### nomic-embed-text (Shared Embeddings)
```
PARAMETER num_ctx 8192
Output: 768-dimensional vectors
```

---

## 5. ChromaDB Configuration

### Service File: `/etc/systemd/system/chromadb.service`
```ini
[Unit]
Description=ChromaDB Vector Database
After=network.target ollama.service

[Service]
Type=simple
User=user
ExecStart=/home/user/.local/bin/chroma run --host 0.0.0.0 --port 8000 --path /home/user/chromadb-data
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

### Key Details
- **Version**: ChromaDB 1.5.8
- **Data Directory**: `/home/user/chromadb-data/`
- **SQLite DB**: `/home/user/chromadb-data/chroma.sqlite3`
- **API Version**: v2 (`/api/v2/`)
- **Collection**: `agent_memory` (cosine similarity)
- **Embedding Model**: nomic-embed-text via Ollama (`localhost:11434/api/embed`)

### How to Embed a Document
```python
import chromadb, requests

client = chromadb.HttpClient(host="localhost", port=8000)
col = client.get_collection("agent_memory")

# Get embedding from nomic
resp = requests.post("http://localhost:11434/api/embed", json={
    "model": "nomic-embed-text",
    "input": "Your text here"
})
embedding = resp.json()["embeddings"][0]

# Store in ChromaDB
col.add(
    ids=["unique-id"],
    embeddings=[embedding],
    documents=["Your text here"],
    metadatas=[{"agent": "agent-name", "type": "task_completion"}]
)
```

### How to Query Memory
```python
# Embed the query
resp = requests.post("http://localhost:11434/api/embed", json={
    "model": "nomic-embed-text",
    "input": "What did Viktor build?"
})
query_embedding = resp.json()["embeddings"][0]

# Search ChromaDB
results = col.query(query_embeddings=[query_embedding], n_results=5)
```

---

## 6. Paperclip AI Connection

### GCP Paperclip Server
| Component | Value |
|---|---|
| **Project** | `cloudagentics` |
| **Zone** | `us-central1-a` |
| **VM Name** | `paperclip-server` |
| **Dashboard** | `http://35.193.223.245:3100` |

### How Models Connect to Paperclip
```
Paperclip (GCP) → OPENAI_BASE_URL=http://80.188.223.202:10232/v1 → Ollama (TensorDock)
```
Paperclip sends standard OpenAI-format chat completion requests to the Ollama endpoint. Ollama routes them to the correct model based on the `model` field in the request.

### Agent → Model Mapping
| Paperclip Agent | model field | Ollama routes to |
|---|---|---|
| Clara Muse | `gpt-4o` | Nemotron 30B |
| Elias Redstone | `gpt-4o` | Nemotron 30B (shared) |
| Viktor Forge | `gpt-4-turbo` | Qwen3.6-35B-A3B |
| Marcus Christensen | `code-reviewer` | Qwen3 8B |
| Niko Relay | `gpt-4` | Gemma 4 E2B |

### Roblox Studio Bridge
```
Roblox Studio (local) ← SSH tunnel → Paperclip Server (GCP)
Command: gcloud compute ssh paperclip-server --project=cloudagentics --zone=us-central1-a -- -R 3002:localhost:3002
```

---

## 7. Backup System

### What's Backed Up
- `/home/user/chromadb-data/` — All ChromaDB vector data
- `/etc/systemd/system/chromadb.service` — ChromaDB service config
- `/etc/systemd/system/ollama.service` — Ollama service config
- `/etc/systemd/system/ollama.service.d/override.conf` — Ollama tuning
- All Ollama Modelfiles — exported to `/home/user/backups/modelfiles/`

### Backup Schedule
- **Frequency**: Daily at 4:00 AM (server time, Prague CET/CEST)
- **Retention**: Last 7 backups
- **Location**: `/home/user/backups/`
- **Log**: `/home/user/backups/backup.log`
- **Script**: `/home/user/backup_memory.sh`

### Crontab Entry
```
0 4 * * * /home/user/backup_memory.sh >> /home/user/backups/backup.log 2>&1
```

### Manual Backup
```bash
ssh -p 10262 -i ~/.ssh/id_ed25519 user@80.188.223.202 "/home/user/backup_memory.sh"
```

### Download Backup to Local Machine
```bash
scp -P 10262 -i ~/.ssh/id_ed25519 user@80.188.223.202:/home/user/backups/agent_memory_LATEST.tar.gz ./
```

---

## 8. Full Rebuild Procedure

If the VM is deleted, follow these steps on a new TensorDock A100 80GB:

### Step 1: Install Ollama
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### Step 2: Pull All Models
```bash
ollama pull nemotron-3-nano
ollama pull qwen3.6:35b-a3b
ollama pull qwen3:8b
ollama pull gemma4:e2b
ollama pull nomic-embed-text
ollama pull deepseek-r1:14b
ollama pull gemma4:e4b
```

### Step 3: Create Spoofed Aliases
```bash
# Clara/Elias — gpt-4o → Nemotron 30B
cat << 'EOF' > /tmp/gpt-4o.Modelfile
FROM nemotron-3-nano
PARAMETER num_ctx 131072
PARAMETER temperature 1
PARAMETER top_p 1
EOF
ollama create gpt-4o -f /tmp/gpt-4o.Modelfile

# Viktor — gpt-4-turbo → Qwen3.6-35B-A3B
cat << 'EOF' > /tmp/gpt-4-turbo.Modelfile
FROM qwen3.6:35b-a3b
PARAMETER num_ctx 65536
PARAMETER presence_penalty 1.5
PARAMETER repeat_penalty 1
PARAMETER temperature 1
PARAMETER top_k 20
PARAMETER top_p 0.95
PARAMETER min_p 0
EOF
ollama create gpt-4-turbo -f /tmp/gpt-4-turbo.Modelfile

# Also create gpt-4o-mini as same model
ollama create gpt-4o-mini -f /tmp/gpt-4-turbo.Modelfile

# Niko — gpt-4 → Gemma 4 E2B
cat << 'EOF' > /tmp/gpt-4.Modelfile
FROM gemma4:e2b
PARAMETER num_ctx 4096
PARAMETER temperature 1
PARAMETER top_k 64
PARAMETER top_p 0.95
EOF
ollama create gpt-4 -f /tmp/gpt-4.Modelfile

# Marcus — code-reviewer → Qwen3 8B
cat << 'EOF' > /tmp/code-reviewer.Modelfile
FROM qwen3:8b
EOF
ollama create code-reviewer -f /tmp/code-reviewer.Modelfile
```

### Step 4: Configure Ollama Service
```bash
sudo mkdir -p /etc/systemd/system/ollama.service.d
sudo cat << 'EOF' > /etc/systemd/system/ollama.service.d/override.conf
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="OLLAMA_KEEP_ALIVE=24h"
Environment="OLLAMA_MAX_LOADED_MODELS=5"
Environment="OLLAMA_NUM_PARALLEL=2"
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
Environment="OLLAMA_GPU_OVERHEAD=2147483648"
EOF
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

### Step 5: Install & Configure ChromaDB
```bash
pip install chromadb
mkdir -p /home/user/chromadb-data

# If restoring from backup:
tar xzf agent_memory_BACKUP.tar.gz -C /

# Create systemd service
sudo cat << 'EOF' > /etc/systemd/system/chromadb.service
[Unit]
Description=ChromaDB Vector Database
After=network.target ollama.service

[Service]
Type=simple
User=user
ExecStart=/home/user/.local/bin/chroma run --host 0.0.0.0 --port 8000 --path /home/user/chromadb-data
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now chromadb
```

### Step 6: Create ChromaDB Collection (if new, not restoring)
```python
import chromadb
client = chromadb.HttpClient(host="localhost", port=8000)
client.get_or_create_collection(
    name="agent_memory",
    metadata={"hnsw:space": "cosine"}
)
```

### Step 7: Set Up Port Forwards on TensorDock Dashboard
- `NEW_PORT → 11434` (Ollama)
- `NEW_PORT → 8000` (ChromaDB)
- `NEW_PORT → 22` (SSH)

### Step 8: Update Paperclip
Update `OPENAI_BASE_URL` in Paperclip to point to the new IP and Ollama port.

### Step 9: Install Backup Cron
```bash
# Upload backup_memory.sh to /home/user/
chmod +x /home/user/backup_memory.sh
(crontab -l 2>/dev/null; echo '0 4 * * * /home/user/backup_memory.sh >> /home/user/backups/backup.log 2>&1') | crontab -
```

---

## 9. VRAM Budget

| Model | VRAM |
|---|---|
| Nemotron 30B (128K ctx) | ~26 GB |
| Qwen3.6-35B-A3B (64K ctx) | ~25 GB |
| Gemma 4 E2B (4K ctx) | ~6 GB |
| Qwen3 8B (default ctx) | ~5 GB |
| nomic-embed-text (8K ctx) | ~0.3 GB |
| GPU overhead reserved | 2 GB |
| **Total** | **~64.3 GB** |
| **Available** | **~15.7 GB** |
| **A100 Capacity** | **80 GB** |

Current actual VRAM usage (from `nvidia-smi`): **69,082 MiB / 81,920 MiB**

---

## 10. Cost Summary

| Component | Cost |
|---|---|
| TensorDock Compute | $1.158/hr |
| TensorDock Storage | $0.015/hr |
| **TensorDock Total** | **$1.173/hr ($28.15/day, $844/mo)** |
| GCP Paperclip VM | ~$0.067/hr ($49/mo) |
| **Grand Total** | **~$893/mo** |

---

*Last updated: April 19, 2026*
*Backup location: `/home/user/backups/` on TensorDock*
*This document: `christensen-and-sons/DISASTER_RECOVERY.md`*
