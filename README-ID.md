<div align="center">
  <a href="README.md">English</a> | <a href="README-ID.md">Bahasa Indonesia</a>
</div>
<br/>

# 🛠️ Berkas Konfigurasi OpenCode

Repositori ini berisi berkas konfigurasi OpenCode pribadi saya. Pengaturan ini dioptimalkan untuk alur kerja khusus saya tetapi dirancang agar fleksibel—jangan ragu untuk menggunakannya sebagai referensi atau langsung menggunakannya dalam pengaturan Anda.

## 🚀 Cara Penggunaan

Ikuti langkah-langkah berikut untuk menerapkan konfigurasi:

1. Klon repositori ini.
2. Salin berkas dari `.config/opencode/*` ke direktori konfigurasi OpenCode lokal Anda.
3. Jalankan OpenCode.

### Mulai Cepat (Linux/macOS)

```bash
# Salin berkas konfigurasi
cp -r .config/opencode/* ~/.config/opencode/
```

### Mulai Cepat (Windows)

Jalur konfigurasi: `C:\Users\$USER$\.config\opencode`

```powershell
# Salin berkas konfigurasi
Copy-Item -Recurse .config\opencode\* C:\Users\$env:USERNAME\.config\opencode\
```

### Jalankan OpenCode
```bash
opencode
```

## Struktur Direktori Konfigurasi

![Contoh Struktur Direktori Linux](/Screenshoot/config-folder-linux.png)

## 📦 Ikhtisar Berkas Konfigurasi

| Berkas | Deskripsi |
|--------|-----------|
| [`opencode.json`](/.config/opencode/opencode.json) | Konfigurasi utama OpenCode dengan definisi provider & model |
| [`oh-my-opencode.json`](/.config/opencode/oh-my-opencode.json) | Full Gemini Preset — Orkestrasi Agen/Skills |
| [`oh-my-opencode-best-config.json`](/.config/opencode/oh-my-opencode-best-config.json) | Best Config Preset — Orkestrasi campuran Gemini + Claude |
| [`antigravity.json`](/.config/opencode/antigravity.json) | Konfigurasi autentikasi Antigravity |

## ⚙️ Model yang Didukung (opencode.json)

Konfigurasi `opencode.json` mencakup definisi model berikut:

**Model Antigravity (via Antigravity Auth):**
- **Gemini 3 Pro** — dengan varian thinking level `low` dan `high`
- **Gemini 3 Flash** — dengan varian thinking level `minimal`, `low`, `medium`, dan `high`
- **Claude Sonnet 4.5** — mode standar
- **Claude Sonnet 4.5 Thinking** — dengan varian thinking `low` (budget 8K) dan `max` (budget 32K)
- **Claude Opus 4.6 Thinking** — dengan varian thinking `low` (budget 8K) dan `max` (budget 32K)

**Model Gemini CLI (via Google AI Studio / Gemini CLI):**
- Gemini 2.5 Flash
- Gemini 2.5 Pro
- Gemini 3 Flash Preview
- Gemini 3 Pro Preview

## 🎭 Orkestrasi: oh-my-opencode

Saya telah menyediakan dua konfigurasi preset untuk Orkestrasi Agen/Skills `oh-my-opencode`. Anda dapat menukarnya tergantung pada strategi pilihan Anda:

### 1. Full Gemini Preset — [`oh-my-opencode.json`](/.config/opencode/oh-my-opencode.json)

Semua agen dan kategori menggunakan **model Gemini saja** via Antigravity. Dioptimalkan untuk kecepatan dan efisiensi biaya.

- **Agen berat** (sisyphus, build, plan, hephaestus, oracle, dll.) → `antigravity-gemini-3-pro` @ `high`
- **Agen ringan** (sisyphus-junior, librarian, executor, dll.) → `antigravity-gemini-3-flash` @ `medium`–`high`
- **Kategori** dipetakan ke tier model Gemini yang sesuai

### 2. Best Config Preset — [`oh-my-opencode-best-config.json`](/.config/opencode/oh-my-opencode-best-config.json)

**Strategi campuran** yang menggabungkan Claude Opus 4.6, Claude Sonnet 4.5, dan model Gemini untuk kualitas terbaik pada setiap tugas.

- **Agen kritis** (sisyphus, plan, prometheus, security-auditor) → `antigravity-claude-opus-4-6-thinking` @ `max`
- **Agen implementasi** (build, hephaestus, metis, reviewer, tester, refactorer) → `antigravity-claude-sonnet-4-5-thinking` @ `max`
- **Agen eksplorasi/visual** (oracle, explore, multimodal-looker, atlas) → `antigravity-gemini-3-pro/flash`
- **Kategori** menggunakan model terkuat per domain (misal: `ultrabrain` & `security` → Claude Opus 4.6)

### Penggunaan

Cukup salin konten berkas preset yang diinginkan dan ganti konten `oh-my-opencode.json` di direktori konfigurasi OpenCode Anda.

### 🔧 Fitur oh-my-opencode yang Dikonfigurasi

Kedua preset mencakup pengaturan fitur berikut:

| Fitur | Pengaturan | Deskripsi |
|-------|------------|-----------|
| `browser_automation_engine` | `playwright` | Automasi browser via Playwright |
| `sisyphus_agent` | aktif, planner aktif | Agen otonom dengan kemampuan perencanaan |
| `dynamic_context_pruning` | aktif, detail | Manajemen konteks cerdas dengan deduplikasi dan pembersihan error |
| `auto_resume` | aktif | Otomatis melanjutkan sesi yang terinterupsi |
| `ralph_loop` | nonaktif (100 maks iter) | Kontrol ralph loop |
| `background_task` | 4 konkurensi, timeout 5 menit | Manajemen tugas latar belakang |
| `notification` | paksa aktif | Notifikasi desktop |
| `git_master` | tanpa footer, tanpa co-authored-by | Format commit git yang bersih |

## 🔐 Konfigurasi Autentikasi Antigravity

Berkas [antigravity.json](/.config/opencode/antigravity.json) mewakili pengaturan autentikasi antigravity pribadi saya.

| Pengaturan | Nilai | Deskripsi |
|------------|-------|-----------|
| `account_selection_strategy` | `sticky` | Tetap pada akun yang sama sampai terkena rate-limit |
| `switch_on_first_rate_limit` | `true` | Otomatis pindah akun saat rate limit |
| `max_rate_limit_wait_seconds` | `0` | Tidak menunggu pada akun yang terkena rate-limit |
| `quota_fallback` | `true` | Beralih ke akun lain saat kuota habis |
| `pid_offset_enabled` | `true` | Gunakan offset PID untuk pemilihan akun |
| `soft_quota_threshold_percent` | `80` | Peringatan kuota lunak pada 80% penggunaan |
| `quota_refresh_interval_minutes` | `10` | Segarkan info kuota setiap 10 menit |

*   **Referensi:** Anda dapat menggunakannya sebagai referensi langsung atau memodifikasinya.
*   **Kustomisasi:** Untuk menyesuaikannya dengan benar, silakan merujuk ke skema resmi [di sini](https://raw.githubusercontent.com/NoeFabris/opencode-antigravity-auth/main/assets/antigravity.schema.json).

## 🔐 Antigravity Auth Tambah Akun

Untuk menambahkan akun baru ke konfigurasi Antigravity Anda, ikuti langkah-langkah berikut:

1.  **Mulai Proses Login**: Jalankan perintah `opencode auth login`. Pilih **Google** sebagai penyedia.
    ![Pilih Penyedia](/Screenshoot/antigravity-auth-add-account-1.png)

2.  **Pilih Metode Login**: Pilih **OAuth with Google (Antigravity)**.
    ![Pilih Metode Login](/Screenshoot/antigravity-auth-add-account-2.png)

3.  **Tambah Akun Baru**: Saat diminta untuk memilih akun, pilih **Add new account**.
    ![Tambah Akun Baru](/Screenshoot/antigravity-auth-add-account-3.png)

4.  **Selesaikan Autentikasi**: Ikuti petunjuk untuk membuka tautan di browser Anda, lakukan autentikasi, dan tempel URL pengalihan kembali ke terminal. Setelah selesai, akun Anda akan ditambahkan.
    ![Sukses](/Screenshoot/antigravity-auth-add-account-4.png)
