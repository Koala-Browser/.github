# Koala Browser Project

<div align="center">
  <img src="https://raw.githubusercontent.com/koala-browser/.github/main/assets/koala-logo.png" width="128" height="128" alt="Koala Browser Logo" />
  <p><strong>A Modern, High-Assurance Hybrid Browser</strong></p>
  <p>JavaFX 21 UI Shell • JCEF Chromium Subprocesses • AES-256-GCM Vault • DNS-over-HTTPS</p>
</div>

---

### 🏛️ High-Level Architecture Overview

Koala Browser utilizes a multi-process architecture decoupling the presentation and session supervision layers from untrusted DOM/V8 execution contexts:

- **Host Process (Java 21 / JavaFX)**: Handles chrome controls (Omnibox, TabStrip, Downloads), SQLite session persistence (HikariCP, WAL mode), and DNS-over-HTTPS network mediation.
- **Engine Subprocesses (CEF / Native Blink)**: Runs in OS-isolated sandboxes (seccomp-bpf, Windows Job Objects, macOS App Sandbox) executing JavaScript, rasterization, and media decoding.

### 📦 Key Repositories

- [`koala-browser`](https://github.com/koala-browser/koala-browser): Main multi-module Maven source code.
- [`jcef-binaries`](https://github.com/koala-browser/jcef-binaries): Native platform builds (`x86_64`, `aarch64`).
- [`adblock-lists`](https://github.com/koala-browser/adblock-lists): Synchronized EasyList rule sets and Bloom filter tries.

### 🛡️ Security & Invariants
- Mandatory TLS 1.3 / strict HTTPS upgrades
- AES-256-GCM encrypted persistence integrated with native OS keyrings (DPAPI / Keychain / SecretService)
- Non-blocking SQLite WAL writes with strict frame rate preservation (60+ FPS)
