# apt-libravdbd

Debian package repository for **libravdbd** — the systemd daemon component of [LibraVDB](https://github.com/xDarkicex/libravdb), an AI-native vector database library for Go.

---

## Package Repository

This repo hosts pre-built `.deb` packages for **libravdbd**, providing an easy install path on Debian/Ubuntu systems.

### Repository Layout

| Path | Purpose |
|------|-|
| `dists/stable/Release` | APT repository metadata (InRelease, Release, Release.gpg) |
| `dists/stable/main/binary-amd64/` | amd64 .deb packages and metadata |
| `dists/stable/main/binary-arm64/` | arm64 .deb packages and metadata |
| `pool/main/stable/` | Source .deb binaries |
| `gpg.key` | Repository signing key |

### Installation

```bash
# Add the repository signing key
sudo apt-key add gpg.key

# Add to /etc/apt/sources.list
echo "deb [signed-by=/usr/share/keyrings/libravdbd.gpg] http://your-repo stable main" | sudo tee /etc/apt/sources.list.d/libravdbd.list

# Install
sudo apt update
sudo apt install libravdbd
```

### Available Versions

| Version | Architectures | Packages |
|---------|---------------|----------|
| **1.4.25** (latest) | amd64, arm64 | `libravdbd_1.4.25_amd64.deb`, `libravdbd_1.4.25_arm64.deb` |
| 1.4.24 | amd64, arm64 | |
| 1.4.23 | amd64, arm64 | |
| 1.4.22 | amd64, arm64 | |
| 1.4.21 | amd64, arm64 | |
| 1.4.20 | amd64, arm64 | |
| 1.4.19 | amd64, arm64 | |
| 1.4.18 | amd64, arm64 | |
| 1.4.17 | amd64, arm64 | |

Total: **9 tagged versions** across **2 architectures** = **18 .deb packages**.

### Package Metadata (latest)

```
Package:           libravdbd
Version:           1.4.25
Section:           utils
Priority:          optional
Architecture:      amd64, arm64
Maintainer:        xDarkicex <contact@darkicex.com>
Depends:           libc6 (>= 2.17), libgomp1
Filename:          pool/main/stable/libravdbd_1.4.25_amd64.deb
Size:              ~4.9 MB (amd64), ~4.9 MB (arm64)
SHA256:            varies per build
```

### Installed Files

| Path | Description |
|------|-------------|
| `/usr/bin/libravdbd` | Main daemon binary |
| `/usr/lib/libravdbd/provision.sh` | ML model provisioning script |
| `/usr/lib/systemd/user/libravdbd.service` | User systemd service unit |

### Usage

```bash
# Start the daemon
systemctl --user start libravdbd

# Check status
systemctl --user status libravdbd

# Provision ML models (requires sudo)
sudo /usr/lib/libravdbd/provision.sh --target /var/lib/libravdbd
```

---

## About LibraVDB

**Libravdbd** is the daemon layer for [LibraVDB](https://github.com/xDarkicex/libravdb), the core Go vector database library.

### LibraVDB Library

| Attribute | Value |
|-----------|-------|
| **Language** | Go (1.25+) |
| **License** | Apache 2.0 |
| **Current version** | 1.0.0 |
| **Dependencies** | Zero external Go dependencies |

### Core Features

- **Multiple Index Types**: HNSW, IVF-PQ, and Flat algorithms with automatic selection
- **Advanced Quantization**: Product Quantization (8x compression) and Scalar Quantization (4x)
- **Rich Metadata Filtering**: Complex AND/OR/NOT operations with type-safe schemas
- **Streaming Operations**: High-throughput batch processing with backpressure control
- **Memory Management**: Configurable limits, memory mapping (mmap), and automatic optimization
- **Persistent Storage**: Single-file binary persistence with WAL-backed durability and reopen/rebuild support
- **Write Concurrency**: Phase 1 bounded write admission for batch/streaming writers
- **Observability**: Prometheus metrics, health checks, and distributed tracing
- **Built-in Error Recovery**: Circuit breakers, graceful degradation, automatic recovery orchestration

### libravdbd Integration

The daemon exposes libravdb's capabilities via:

- **RPC interface** — remote vector operations (search, insert, delete, query)
- **ML embeddings** — ONNX Runtime-powered text/vector generation
- **Summarization** — automatic text summarization endpoints
- **Model provisioning** — `provision.sh` handles downloading and configuring ML models
- **Zero-config** — sensible defaults with `systemctl --user` lifecycle management

### Package History

Versions 1.4.17 through 1.4.25 represent incremental daemon releases. Each version ships both amd64 and arm64 builds. The repository supports the `stable` distribution branch.

---

*This repository is maintained by the LibraVDB project team. Questions and issues: [GitHub](https://github.com/xDarkicex/libravdb)*
