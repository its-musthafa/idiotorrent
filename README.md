# 🧠 Idiotorrent — A Lightweight Torrent

**“A torrent system for small files, built from scratch, with real P2P, a public tracker, and lightweight design. Not for pirating 50GB Linux ISOs. Just works.”**

---

## 🌐 What Is This?

**Idiotorrent** is a minimalist peer-to-peer file sharing protocol, inspired by BitTorrent but intentionally simplified. Built in Python, it is designed to:

- Share **small files** (less than ~20MB)
- Work in **LAN or small networks**
- Be **easy to understand, debug, and extend**
- Use a **public tracker** hosted on Firebase or Google Cloud Run

Not meant for production-scale files. Just simple, fast, and educational.

---

## 🔧 What We're Building

| Component | Description |
|----------|-------------|
| 🧱 Chunker + Metadata Tool | Break file into chunks, hash, save `.idtorrent` metadata |
| 💾 Seeder / Peer Client | Upload/download chunks over TCP |
| 🔄 Public Tracker (Cloud) | Stores active peers for each file |
| 🔌 Tracker API Client | Register peer and get peer list |
| 🧠 File Reassembler | Rebuild original file from chunks |
| 🧪 Optional: File Validation | Simple final hash comparison |
| 🧭 CLI UX | Easy commands to create, seed, download |
| 📦 Hosting Tool | (Optional) Upload-to-torrent web tool |

---

## 🧠 How It Works

### `.idtorrent` File Format (JSON)

```json
{
  "file_name": "example.jpg",
  "file_size": 204800,
  "chunk_size": 10240,
  "num_chunks": 20,
  "chunk_hashes": ["ab12...", "cd34...", "..."],
  "file_id": "sha1(file_name + size + hash_list)"
}
```

# 🌐 Tracker API Design

| Endpoint      | Method | Description                                  |
|---------------|--------|----------------------------------------------|
| /register_peer| POST   | Register peer for given file ID             |
| /get_peers    | GET    | Get active peer list for a file             |
| /prune_dead   | Internal | Tracker removes stale peers                 |

---

## Backed by Firebase or Google Cloud Run

- Simple REST API
- Can be scaled up later

---

### 🛠️ Stack

- **Language:** Python 3
- **Sockets:** TCP for chunk sharing
- **Tracker:** Firebase, Firestore, or Google Cloud Run + Flask
- **Data Format:** JSON .idtorrent metadata
- **Hashing:** SHA1 (per chunk)

---

### 🔮 Future Features (Optional)

| Feature                | Notes                                  |
|------------------------|----------------------------------------|
| Peer timeout cleanup    | Tracker purges dead peers              |
| Download resume         | Bitmap of completed chunks            |
| Web UI                 | Drag-and-drop torrent creation        |
| ESP8266 Seeder         | Experimental low-MB sharing           |
| Multi-threaded download | Speed-up with parallel requests       |
| Progress bar / stats   | Chunk download % view                 |

# 🧠 Why?

This project is designed to:

- Learn how peer-to-peer systems work
- Build your own protocol from scratch
- Provide an open-source base for education and experimentation
- Serve as a starting point for LAN-sharing tools, mesh networks, and embedded experiments

*“It’s called Idiotorrent because it does the job — no magic, no obfuscation. Just chunks, hashes, and socket pipes.”*
