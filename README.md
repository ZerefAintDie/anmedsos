# Polarisasi Komunitas Autonomous Coding Agent di YouTube

Final Project Analisis Media Sosial. Analisis jaringan balasan komentar YouTube (SNA), sentimen, dan topik seputar autonomous coding agent.

## Struktur

```
anmedsos/
├── 01_data_preprocessing_sentimen_topik.ipynb   # crawling, preprocessing, sentimen, topik, ekspor CSV
├── requirements.txt
├── .env.example                                 # template API key
└── data/
    ├── raw/         # data mentah per video (tidak di-upload)
    ├── cache/       # cache sentimen dan embedding (tidak di-upload)
    └── processed/   # dataset final yang sudah dianonimkan (di-upload)
```

## Cara menjalankan

1. Pakai Python 3.12 atau 3.13, lalu install library:
   ```bash
   pip install -r requirements.txt
   ```
2. Salin `.env.example` menjadi `.env`, lalu isi `YOUTUBE_API_KEY` (YouTube Data API v3).
3. Buka notebook dari folder `anmedsos/`, lalu jalankan semua sel (*Run All*).

Data di `data/processed/` adalah snapshot pada tanggal yang tercatat di `data/processed/metadata.json`. Mengambil ulang data (`FORCE_RECRAWL = True`) bisa memberi hasil sedikit berbeda karena komentar YouTube terus bertambah atau dihapus.

## Dataset (`data/processed/`)

| File | Isi |
|---|---|
| `comments_clean.csv` | Satu baris per komentar: teks, sentimen, topik, tema |
| `videos.csv` | Metadata video |
| `edges_reply.csv` | Satu baris per balasan (Source membalas Target) |
| `edges_reply_gephi.csv` | Edge berarah berbobot untuk Gephi (Source, Target, Type, Weight) |
| `nodes_users.csv` | Atribut tiap akun untuk Gephi |
| `edges_user_video.csv` | Edge graf bipartit pengguna–video |
| `nodes_bipartite.csv` | Node graf bipartit (user/video) |
| `topic_info.csv` | Daftar topik BERTopic |
| `metadata.json` | Tanggal crawling, parameter, versi library |

Semua akun sudah dianonimkan (`user_00001`, dst.) dan `@handle` di teks diganti `@user`.
