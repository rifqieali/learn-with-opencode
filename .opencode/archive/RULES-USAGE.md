# Panduan Penggunaan: Technology Learning & Work Mentor

Aturan lengkap ada di `./rules.md` (yang dibaca AI). File ini cuma panduan pakai.

## File-file

| File | Isi |
|---|---|
| `rules.md` | Aturan lengkap (v3 merged: toolkit video + kelebihan v2) |
| `AGENTS.md` | Ringkasan + pointer ke `rules.md` |
| `rules.v1-mentor-legacy.md` | Arsip rules lama (learning-first yang ketat). Jangan dihapus. |
| `rules.v2-work-while-learning.md` | Backup rules kerja sebelum merge video (2026-09-27). Jangan dihapus. |
| `opencode.json` | Mendaftarkan `rules.md` + `AGENTS.md` sebagai instructions |

## Cara buka opencode

Buka dari root workspace ini:

```bash
opencode
# dari /LaravelEra
```

Buka dari sub-project juga bisa (misal `EMS-Laravel/`) — config root tetap
kebaca karena opencode mencari config dari direktori aktif ke atas.

- **Dari root** → AI lihat semua sub-project. Enak buat grinding/pindah app,
  tapi konteks lebih besar.
- **Dari sub-project** → fokus satu app, path relatif lebih pendek.

## Default behavior: WORK MODE

Kerja seperti biasa, tanpa keyword → AI jadi pair programmer: boleh kasih
code, fix bug, refactor, bikin migration/test, plus penjelasan kenapa +
trade-off.

## Pindah mode

| Mode | Keyword | Efek |
|---|---|---|
| MENTOR | `mentor`, `jangan kasih code`, `bantu gue mikir`, `gue mau coba sendiri`, `/hint`, `/debug` | Dibimbing bertahap (L0-L6 adaptive), tanpa solusi langsung |
| EXAMINER | `/R`, `/review-design`, `examiner`, `challenge desain ini` | Tantang rancangan sebelum code |
| TEACH | `ajari`, `teach`, `belajar`, `jelasin dari dasar`, `buat lesson`, `/teach`, `/read` | Belajar fundamental, satu konsep per sesi |
| REVIEW | `review`, `review code`, `cek code`, `audit`, `code review`, `/review-code` | Temuan: `CRITICAL / IMPORTANT / IMPROVEMENT / OPTIONAL` |
| DEADLINE | `deadline`, `langsung fix`, `kasih code`, `mode copas`, `urgent`, `ship it` | Solusi langsung, mengalahkan mode lain |

Contoh:

```text
mentor, bantu gue mikir soal query N+1 ini
/teach Eloquent relationship
review code ini
deadline, langsung fix aja
```

## Mematikan rules

- **Satu sesi:** `abaikan rules.md untuk sesi ini`
- **Satu project:** hapus `rules.md` dari `instructions` di `opencode.json`
- **Repo GitHub tim:** jangan taruh file personal di repo. Pakai global config:
  copy `rules.md` ke misal `~/.config/opencode/rules-mentor.md`, lalu daftarkan
  path absolutnya di `~/.config/opencode/opencode.json`:

  ```json
  {"$schema": "https://opencode.ai/config.json", "instructions": ["/home/YOU/.config/opencode/rules-mentor.md"]}
  ```

  Verifikasi dengan `opencode debug config`.

## Pasang ke project lain

1. Copy `rules.md` (atau pakai global config di atas).
2. Sesuaikan `AGENTS.md` dengan project tujuan — jangan copy mentah karena
   file di sini nyebut sub-project workspace ini.
3. Pastikan `opencode.json` mendaftarkan keduanya di `instructions`.
4. Jangan commit file personal (`rules.md`, `rules.v1-mentor-legacy.md`,
   learning records) ke repo tim. Yang boleh di-commit kalau tim setuju:
   `AGENTS.md` berisi convention project.
