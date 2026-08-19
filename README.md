# Audio Processor

GitHub Actions workflow untuk download & proses audio (YouTube, TikTok, SoundCloud, upload file).

## Bypass Copyright Roblox

1. **Download** audio dari sumber
2. **Speed up** dengan faktor T (mis. 2.3x) — tempo **dan** nada naik bersamaan (`ffmpeg asetrate`, seperti mempercepat kaset)
3. **Upload** ke Roblox sebagai audio asset
4. **Di game**: set `PlaybackSpeed = 1/T` (mis. 0.43) → suara kembali normal

> Jangan pakai time-stretch yang mempertahankan nada (`atempo`, `rubberband -t` saja). Itu merusak hasil inverse di Roblox.

`applied_speed` dikirim ke callback web → disimpan sebagai `roblox_playback_speed = 1 / applied_speed`.
