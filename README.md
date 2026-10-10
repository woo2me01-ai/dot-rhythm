# 🎯 Rhythm Dot Tap

**How fast are your reflexes?** Tap the dots to the beat for 2 minutes, see your reaction time measured to **0.01 seconds**, and share your result as a one-line emoji score card.

```
🎯 Rhythm Dot Tap 10/9
🟩🟩🟩🟥🟨🟨🟥🟩
⏱ Lasted 1m 52s (LEVEL 12)
🏆 #57 today of 1,234 players
⚡ Avg reaction 0.48s 🐆 Cheetah · 3,240 pts
```

No sign-up, no install. Open the link and play.

## ✨ Features

- **Reaction-time tracking (0.01s precision):** every dot is timed from the moment it appears to the moment you tap it. The results screen shows your average, fastest, and slowest reaction.
- **Rhythm-based gameplay:** dots pulse to a beat. Tap right on the beat for a PERFECT bonus.
- **12 levels in 2 minutes:** every 10 seconds the dots get smaller and faster and the tempo rises (100 → 160 BPM).
- **Emoji score card:** your run becomes a single line of emoji (1 square = 15 seconds), ready to paste into a group chat or onto X.
- **One-tap sharing:** opens the native share sheet on mobile (KakaoTalk, Messages, X…). Where sharing isn't supported, the result is copied to the clipboard instead.
- **English / Korean:** switch with the EN | KR toggle. The game follows the browser language by default and remembers your choice. Add `?lang=en` or `?lang=ko` to the URL to force a language.
- **Music as you play:** every hit plays the next note of a public-domain medley (Ode to Joy → Twinkle Twinkle → Für Elise → Canon in D).
- **🏆 Today's ranking:** a daily leaderboard that resets at midnight (KST). Just pick a nickname, no account needed. After that, runs are submitted automatically.
- **⚔️ Friend challenge rooms:** create a room and share its link (`?room=abc123`) in a group chat. Everyone who joins through the link gets their own room leaderboard.
- **Local best scores:** your top 10 runs are saved in your own browser (localStorage).
- **Single HTML file:** no frameworks, no build step, no external assets. Sound is generated with the Web Audio API.

## 🕹️ How to Play

| | Rule | Points |
|---|---|---|
| ● | Tap a dot | +10 |
| ★ | Every 5th dot is a **golden dot** | +50 |
| ◆ | Every 30 combo, a **blue dot** appears | +100 |
| ♪ | Tap right on the beat (PERFECT) | +5 bonus |
| 🔥 | Every 10 combo raises the multiplier (×2, ×3, ×4) | |
| ✕ | Missing a dot or tapping empty space counts as a miss and resets your combo | |
| ❤ | 3 lives. The 3rd miss ends the game | |

### Emoji score card legend

| Emoji | Meaning |
|---|---|
| 🟩 | Fast (avg under 0.50s) |
| 🟨 | OK (0.50–0.70s) |
| 🟧 | Slow (over 0.70s) |
| 🟥 | A miss happened in this section |
| ⬛ | Section not reached |

### Reaction-time ranks

⚡ Lightning (< 0.40s) · 🐆 Cheetah (< 0.50s) · 🐇 Rabbit (< 0.65s) · 🐢 Turtle

## 🚀 Run It

Download `index.html` and open it in any modern browser. That's it.

To host it, upload `index.html` to any static host (GitHub Pages, Netlify, Vercel…). The native share sheet only works over `https://`. When opened as a local file, the Share button copies the result instead.

### Deploying on GitHub Pages

1. Push this folder to a GitHub repository.
2. Go to **Settings → Pages**, choose the branch, and save.
3. Set your game URL in `SHARE_URL` inside `index.html` so shared results link back to your game.

## 🏆 Online Ranking Setup (optional)

The ranking uses a free [Supabase](https://supabase.com) database. Without it, the game works exactly as before, with ranking buttons hidden.

1. Create a Supabase project (the Seoul region is a good fit for Korean players).
2. Open **SQL Editor → New query**, paste the whole `ranking-setup.sql`, and click **Run**.
3. Copy the **Project URL** and the **Publishable key** (or legacy `anon` key) from **Connect** or **Settings → API Keys**.
4. Put them in `SUPABASE_URL` and `SUPABASE_KEY` at the top of the script in `index.html`.

Never put the **secret** / `service_role` key in `index.html`.

**How scores are protected:** the browser can't read or write the scores table directly. It can only call database functions that reject impossible runs: scores above the maximum possible, superhuman reaction times, hit rates and levels that don't match the time played, and fake clears. They also rate-limit submissions and filter nicknames. Only the nickname, run stats, a random browser ID, and a hashed (not raw) IP for spam control are stored.

## ⚙️ Customization

All settings are at the top of the `<script>` in `index.html`. On-screen text updates automatically when you change them.

| Setting | Default | What it does |
|---|---|---|
| `ROUND_SECONDS` | `120` | Length of one game (seconds) |
| `LEVEL_SECONDS` | `10` | Seconds per level |
| `LEVELS` | 12 levels | Dot size, speed, lifetime, and BPM per level |
| `SPECIAL_EVERY` | `5` | Golden dot frequency |
| `BLUE_EVERY_COMBO` / `POINTS_BLUE` | `30` / `100` | Blue dot combo interval and points |
| `MAX_MISSES` | `3` | Misses allowed before game over |
| `PERFECT_WINDOW` | `0.09` | Seconds before/after the beat that count as PERFECT |
| `BLOCK_SECONDS` | `15` | Seconds per emoji square on the score card |
| `RT_FAST` / `RT_OK` | `0.50` / `0.70` | Reaction-time thresholds for 🟩 / 🟨 / 🟧 |
| `SHARE_URL` | `""` | Game URL included in shared results |
| `SUPABASE_URL` / `SUPABASE_KEY` | `""` | Turn on the online ranking (see above) |
| `SONGS` | 4 songs | Melody played note-by-note on each hit |
| `I18N` | `ko`, `en` | All on-screen text, per language |

## 🛠️ Built With

- HTML5 Canvas
- Vanilla JavaScript
- Web Audio API
- Web Share API (with Clipboard fallback)
- Supabase (Postgres) for the optional online ranking

## 📄 License

MIT
