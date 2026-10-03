# humanizer-chatbot-id

Skill humanizer khusus **balasan chatbot berbahasa Indonesia** — membuat balasan bot terdengar seperti manusia yang sedang chat, bukan seperti AI.

Fork dari [blader/humanizer](https://github.com/blader/humanizer) (53.600+ stars, MIT), di-refactor total: pola strukturalnya dipertahankan, tapi seluruh kalibrasi diganti dengan **riset lapangan cara orang Indonesia mengetik di chat**.

> **English summary:** A humanizer skill for Indonesian chatbot replies. Forked from blader/humanizer and recalibrated with field research on how Indonesians actually type in chat (WhatsApp, Facebook, Reddit, Kaskus, Threads). Detects AI tells in bot replies (essay answers, template openers/closers, zero abbreviations, wrong register) and rewrites them to sound like a real person chatting.

## Kenapa ada skill ini

Balasan chatbot AI punya pola yang mudah dikenali manusia Indonesia:

- Jawaban esai satu bubble raksasa (padahal 83% pesan manusia = 1 kalimat)
- "Tentu! ... Semoga membantu! Ada lagi yang bisa saya bantu?" (tidak pernah dipakai manusia di chat)
- Nol singkatan, ejaan sempurna, kapital sempurna (= AI-tell instan di chat Indonesia)
- Langsung menjawab tanpa mengakui pesan user dulu (pola bot paling mudah dikenali)
- Register pengumuman/bot CS untuk obrolan santai

Skill ini mendeteksi 9 pola tersebut dan menulis ulang balasannya mengikuti pola chat natural.

## Riset di baliknya

| Sumber | Sampel |
|---|---|
| 2 grup WhatsApp Indonesia | ±10.800 pesan |
| 3 grup Facebook Indonesia | ±60 komentar |
| r/indonesia (Reddit) | ±60 komentar |
| Kaskus | 4 thread |
| Threads Indonesia | ±100 postingan |
| Scribd (dokumen formal, untuk pembanding) | ±20 dokumen |

Semua contoh di dokumen referensi bersifat ilustratif/parafrasa — tidak ada kutipan verbatim dan tidak ada data personal siapa pun.

## Isi repo

```
SKILL.md                  # skill utama: 9 pola AI + pola positif + cara kerja
README.md                 # file ini
LICENSE                   # MIT (dari blader/humanizer)
references/
  pola-bahasa-indonesia.md        # pola AI khusus Bahasa Indonesia
  gaya-sosmed-indonesia.md        # Facebook
  gaya-chat-whatsapp.md           # WhatsApp grup HackFest
  gaya-chat-whatsapp-idwebzone.md # WhatsApp grup IDwebZone
  gaya-reddit-indonesia.md        # Reddit r/indonesia
  gaya-kaskus.md                  # Kaskus
  gaya-threads-indonesia.md       # Threads
```

## Instalasi

```bash
# 1. Clone repo
git clone https://github.com/titodoni/humanizer-chatbot-id.git

# 2. Pasang ke direktori skills milik platform AI kamu (pilih salah satu):

# Claude Code
mkdir -p ~/.claude/skills
ln -s "$(pwd)/humanizer-chatbot-id" ~/.claude/skills/humanizer-chatbot-id

# OpenCode
mkdir -p ~/.config/opencode/skills
ln -s "$(pwd)/humanizer-chatbot-id" ~/.config/opencode/skills/humanizer-chatbot-id

# Muse (workspace)
ln -s "$(pwd)/humanizer-chatbot-id" ~/workspace/skills/humanizer-chatbot-id

# Kalau tidak mau symlink, copy biasa juga bisa:
# cp -r humanizer-chatbot-id ~/.claude/skills/
```

**Verifikasi:** buka `humanizer-chatbot-id/SKILL.md` — di baris paling atas frontmatter harus ada `name: humanizer-chatbot-id`. Kalau platform kamu punya perintah daftar skills, pastikan nama itu muncul.

**Tanpa platform skills:** copy seluruh isi `SKILL.md` ke system prompt / custom instructions chatbot kamu. File `references/` bersifat opsional tapi dianjurkan — tanpa itu, pola Indonesianya tetap jalan dari SKILL.md, hanya contoh detailnya berkurang.

## Cara pakai

Setelah terpasang, instruksikan agen/bot untuk memakai skill `humanizer-chatbot-id` setiap menulis atau mereview balasan chatbot berbahasa Indonesia. Contoh instruksi ke agen:

> Setiap menulis balasan chatbot, terapkan skill humanizer-chatbot-id: deteksi pola AI pada draf balasan, tulis ulang mengikuti pola chat natural Indonesia, kembalikan hanya teks final.

Dua mode output:

- **Default:** hanya teks balasan final, siap kirim. Tanpa penjelasan.
- **Mode review:** draf + daftar pola yang ditemukan + versi final.

## Contoh

**Sebelum** (pola AI):
> Tentu! Untuk mengatasi masalah tersebut, ada beberapa langkah yang bisa Anda coba. Pertama, periksa koneksi internet Anda. Kedua, restart aplikasi. Ketiga, hapus cache. Semoga membantu! Ada lagi yang bisa saya bantu?

**Sesudah:**
> wah nyebelin ya kalo kekunci gini. coba cek koneksinya dulu kak
>
> kalo masih error, restart aplikasinya aja. masih juga? hapus cache + update ke versi terbaru

## Batasan

- Khusus untuk **chat/percakapan**. Jangan dipakai untuk dokumen formal — untuk itu ada pola dokumen resmi di `references/` skill induk.
- Menerapkan semua pola sekaligus menghasilkan karikatur. Aturan praktis: 2–3 pola per balasan.
- Jangan meniru typo berat, spam hashtag, atau slang yang tidak dipahami persona bot-nya.

## Atribusi

Fork dari [blader/humanizer](https://github.com/blader/humanizer) v3.1.0 (MIT License). Pola struktural §9 diadaptasi dari sana; seluruh kalibrasi bahasa Indonesia dan riset lapangan adalah karya repo ini.
