# 🤖 Advanced AI Content Generator & Automated Approval System

An end-to-end automation workflow built with **n8n** that leverages **OpenAI (GPT-4o & DALL-E 3)** and **Telegram Bot** to generate social media content with visual assets, featuring a **Human-in-the-Loop** approval mechanism.

---

## 📌 Project Overview

Posting konten berkualitas secara konsisten di media sosial membutuhkan waktu dan perencanaan. Proyek ini memotong alur kerja manual tersebut dengan otomatisasi berbasis AI, tetapi tetap menjaga kontrol penuh pengguna (*Human-in-the-Loop*) sebelum konten dipublikasikan.

### Key Features
* **Automated Scheduling:** Menjalankan pemrosesan otomatis sesuai jadwal menggunakan Cron/Schedule Trigger.
* **AI Copywriting (GPT-4o):** Membuat draft caption LinkedIn yang relevan, terstruktur, dan siap pakai lengkap dengan hashtag.
* **AI Image Generation (DALL-E 3):** Menghasilkan prompt visual Bahasa Inggris secara otomatis dari topik caption, lalu membuat banner HD (1024x1024).
* **Interactive Human-in-the-Loop Approval:** Mengirimkan hasil draft teks + gambar ke Telegram pengguna beserta Inline Keyboard (`Approve` / `Reject`).
* **Real-time Webhook Callback Handling:** Menangkap respon tombol klik Telegram secara *real-time* via Telegram Trigger & Switch logic untuk memproses aksi lanjutan.

---

## 🏗️ Architecture & Workflow Structure

[ Schedule Trigger ]
│
▼
[ Generate Caption & Prompt (GPT-4o) ]
│
▼
[ Generate Banner (DALL-E 3) ]
│
▼
[ Send Approval to Telegram ] ───( Telegram Message with Inline Buttons )
│
┌──────────────────────────────────────────────┘
│
▼
[ Telegram Trigger (Callback Query) ]
│
▼
[ Check Action (Switch Node) ]
├── (Approve) ──> [ Notify Approved & Publish ]
└── (Reject)  ──> [ Notify Rejected ]


---

## 🛠️ Tech Stack & Integrations

* **Automation Engine:** [n8n](https://n8n.io/)
* **AI Models:** OpenAI API (`gpt-4o`, `dall-e-3`)
* **Communication Platform:** Telegram Bot API
* **Data Format:** JSON & Webhook Callbacks

---

## 🚀 How to Import & Setup

### 1. Prerequisites
* Inisiasi akun n8n (Self-hosted / Cloud).
* OpenAI API Key.
* Telegram Bot Token (didapatkan via `@BotFather`).
* Telegram Chat ID kamu (didapatkan via `@userinfobot`).

### 2. Import Workflow into n8n
1. Salin seluruh isi file `workflow.json` dari repository ini.
2. Buka canvas n8n baru.
3. Tekan `Ctrl + V` (Windows) atau `Cmd + V` (Mac) untuk melakukan paste.

### 3. Credential Setup
1. **OpenAI Account:** Hubungkan API Key milikmu pada node **Generate Caption & Prompt (GPT-4o)** dan **Generate Banner (DALL-E 3)**.
2. **Telegram Account:** Hubungkan Telegram Bot Token milikmu pada node:
   * `Send Approval to Telegram`
   * `Telegram Trigger (Approval)`
   * `Notify Approved`
   * `Notify Rejected`
3. Isikan `Chat ID` Telegram kamu pada field `Chat ID` di node **Send Approval to Telegram**.

---

## 📸 Demo & Screenshots

| Canvas Workflow | Approval Preview di Telegram |
|---|---|
| ![Canvas Workflow](./assets/n8n-canvas.png) | ![Telegram Preview](./assets/telegram-preview.png) |

---

## 📝 Future Improvements
* [ ] Integrasi otomatisasi publikasi langsung ke API LinkedIn & Twitter/X saat status `Approved`.
* [ ] Penyimpanan riwayat log konten (Draft, Approved, Rejected) ke database PostgreSQL atau Google Sheets.
