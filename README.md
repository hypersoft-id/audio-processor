# Audio Processor — Roblox Bypass

## Cara kerja bypass (sama konsep layanan seperti Audio Velocity)

1. **Download** audio dari YouTube / TikTok / SoundCloud
2. **Modifikasi speed + pitch bersamaan** (tape mode — seperti mempercepat/memperlambat kaset)
3. **Upload** ke Roblox (fingerprint berubah → lolos deteksi copyright)
4. **Di game**: set `Sound.PlaybackSpeed` ke nilai inverse → suara kembali normal

> `PlaybackSpeed` di Roblox mengubah **tempo DAN pitch** bersamaan — ini kunci agar inverse bekerja.

## Dua mode proses

| Mode | Kapan dipakai | Proses file | PlaybackSpeed di Roblox |
|------|---------------|-------------|-------------------------|
| **SLOW** | Track ≤ ~174 detik (dengan speed 2.3) | Perlambat ÷2.3 | **×2.3** (lebih bersih) |
| **FAST** | Track panjang | Percepat ×2.3 | **×0.43** (bisa terjepit jika <0.5) |

**Tips kualitas:** Gunakan speed **2.0x** → PlaybackSpeed **0.5x** di Roblox (batas aman).

## Teknis FFmpeg

```bash
# FAST mode (speed up)
ffmpeg -af "asetrate=101430,aresample=44100:resampler=soxr:precision=28" ...

# SLOW mode (slow down) — kualitas lebih baik
ffmpeg -af "asetrate=19174,aresample=44100:resampler=soxr:precision=28" ...
```

**Jangan pakai:** `atempo`, `rubberband -t` saja, atau `loudnorm` agresif — merusak hasil inverse.

## Output ke website

- `applied_speed` — faktor bypass yang dipakai
- `roblox_playback` — nilai exact untuk PlaybackSpeed di Studio
- `bypass_mode` — `slow` atau `fast`
