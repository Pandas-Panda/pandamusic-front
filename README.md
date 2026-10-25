# 🐼 PandaMusic — Full Project Summary
**Developer: Aayush Oza | October 2026**

---

## 📱 FLUTTER APP — Files Done

### Core Constants
| File | Purpose |
|------|---------|
| `lib/core/constants/app_colors.dart` | Color palette — #0A0A0A bg, #E24B4A accent, #1A1A1A surface |
| `lib/core/constants/app_text_styles.dart` | All text styles — heading, body, caption, song title, tab label |
| `lib/core/constants/app_spacing.dart` | Spacing/padding constants — xs, sm, md, lg, xl, xxl |
| `lib/core/constants/api_constants.dart` | Base URL + all API endpoints |
| `lib/core/constants/app_constants.dart` | DB name, prefs keys, notification IDs, player actions |

### Core Theme & Utils
| File | Purpose |
|------|---------|
| `lib/core/theme/app_theme.dart` | Full dark ThemeData — AppBar, BottomNav, Card, Input, Button, Slider, Switch |
| `lib/core/utils/responsive_helper.dart` | isMobile() / isWindows() — breakpoint 600px, sidebar width 220px |
| `lib/core/utils/duration_utils.dart` | Format mm:ss, listening time, parse string to seconds |

### App Entry
| File | Purpose |
|------|---------|
| `lib/main.dart` | Entry point — DB init, API init, orientation lock, status bar |
| `lib/app.dart` | MultiProvider root — AuthProvider, PlayerProvider, PlaylistProvider, DownloadProvider. Platform split → MobileRoot / WindowsRoot |

### Data Layer
| File | Purpose |
|------|---------|
| `lib/data/local/entities/song_model.dart` | Song model — id, playlistId, title, videoId, youtubeUrl, thumbnailUrl, thumbnailPath, localPath, durationMs, isCached, sortOrder, addedAt, cutRangesJson, pendingDownload |
| `lib/data/local/entities/playlist_model.dart` | Playlist model — id, name, createdAt, iconPath, songCount, totalDurationMs |
| `lib/data/local/dao/song_dao.dart` | All song DB queries — insert, update, delete, markCached, updateSortOrder, updateSongEdit, finalizeTrim, getPendingSongs, songExistsInPlaylist |
| `lib/data/local/dao/playlist_dao.dart` | All playlist DB queries — CRUD + getAllPlaylistsWithStats() JOIN query |
| `lib/data/local/app_database.dart` | SQLite setup — Android + Windows FFI, WAL mode, foreign keys, indexes |

### Services
| File | Purpose |
|------|---------|
| `lib/services/auth_service.dart` | OTP, JWT token, PIN, biometric, secure storage, first launch |
| `lib/services/api_service.dart` | Dio HTTP client — interceptors, token attach, download, error handling |

### Providers
| File | Purpose |
|------|---------|
| `lib/providers/auth_provider.dart` | Login state, OTP flow, biometric, PIN, security settings |
| `lib/providers/playlist_provider.dart` | CRUD playlists + songs, copy/move song, reorder, mark cached |
| `lib/providers/download_provider.dart` | Download tasks map, progress tracking, cancel, retry, clear completed |

---

## 📱 FLUTTER APP — Files Remaining

### Services (Next Up)
| File | Purpose |
|------|---------|
| `lib/services/download_service.dart` | Actual download — call backend /music/stream-url → Dio download with resume |
| `lib/services/player_service.dart` | just_audio wrapper — queue, shuffle, loop, cut ranges, session save/restore |
| `lib/services/notification_service.dart` | Firebase push + local notifications |
| `lib/services/subscription_service.dart` | Subscription status, Razorpay payment, trial check |
| `lib/services/sleep_schedule_service.dart` | Sleep timer — window check, session cap, cancel |
| `lib/services/cache_manager.dart` | Audio cache dir, storage management, clear old cache |

### Providers
| File | Purpose |
|------|---------|
| `lib/providers/player_provider.dart` | Player state — now playing, queue, shuffle, loop, position, cut ranges |

### UI — Auth Screens
| File | Purpose |
|------|---------|
| `lib/ui/shared/splash_screen.dart` | Panda logo + loading animation |
| `lib/ui/shared/auth/login_screen.dart` | Email input screen |
| `lib/ui/shared/auth/register_screen.dart` | Name, email, phone, password, confirm password + validation |
| `lib/ui/shared/auth/verify_email_screen.dart` | "Check your inbox" waiting screen |
| `lib/ui/shared/auth/forgot_password_screen.dart` | Enter email → receive reset link |
| `lib/ui/shared/auth/reset_password_screen.dart` | New password + confirm |
| `lib/ui/shared/auth/pin_entry_screen.dart` | PIN lock screen |

### UI — Mobile Shell
| File | Purpose |
|------|---------|
| `lib/ui/mobile/mobile_root.dart` | BottomNavigationBar — 3 tabs + mini player above nav |
| `lib/ui/mobile/tabs/playlists_tab.dart` | Playlist grid + create button |
| `lib/ui/mobile/tabs/games_tab.dart` | 5 games grid |
| `lib/ui/mobile/tabs/profile_tab.dart` | Subscription, referral, stats, security, settings |

### UI — Windows Shell
| File | Purpose |
|------|---------|
| `lib/ui/windows/windows_root.dart` | Left sidebar shell — 3 tabs |
| `lib/ui/windows/tabs/playlists_tab.dart` | Wider layout playlist grid |
| `lib/ui/windows/tabs/games_tab.dart` | Windows games layout |
| `lib/ui/windows/tabs/profile_tab.dart` | Windows profile layout |

### UI — Shared Screens
| File | Purpose |
|------|---------|
| `lib/ui/shared/mini_player.dart` | Red mini player bar above bottom nav |
| `lib/ui/shared/song_tile.dart` | Song list item — thumbnail, title, duration, options |
| `lib/ui/shared/playlist_card.dart` | Playlist grid/list card |
| `lib/ui/shared/playlist_screen.dart` | Open playlist, song list, play, reorder, long press |
| `lib/ui/shared/now_playing_screen.dart` | Full player — progress, controls, shuffle, loop, sleep, trim |
| `lib/ui/shared/search_screen.dart` | YouTube search + 30sec preview + download |
| `lib/ui/shared/edit_song_screen.dart` | Rename song, trim audio, change thumbnail |
| `lib/ui/shared/add_song_screen.dart` | Search + add to playlist |

### UI — Games (5 games)
| File | Purpose |
|------|---------|
| `lib/ui/shared/games/panda_2048.dart` | 2048 with panda tiles + leaderboard |
| `lib/ui/shared/games/block_puzzle.dart` | Block puzzle game |
| `lib/ui/shared/games/arrow_puzzle.dart` | Arrow puzzle game |
| `lib/ui/shared/games/bus_jam.dart` | Bus jam game |
| `lib/ui/shared/games/voice_panda.dart` | Microphone endless runner |

---

## 🖥️ BACKEND SERVER — Files Done

### Structure
```
D:\pandamusicserverv2\
├── .env                    → all secret keys
├── app.py                  → Flask entry, register blueprints
├── config.py               → env vars, password rules, search filters
├── database.py             → DB connection, init_db(), dict_cursor()
├── requirements.txt        → all Python packages
├── routes/
│   ├── auth.py             → register, login, verify, forgot, reset, refresh, profile
│   ├── music.py            → search, stream-url, preview, ping
│   ├── games.py            → submit score, leaderboard, my-scores
│   ├── subscription.py     → status, create-order, verify-payment, renew
│   ├── referral.py         → get code, apply, validate
│   └── stats.py            → global stats, app config
└── services/
    ├── auth_service.py     → hash password, JWT, validate email/phone/password, referral code
    ├── otp_service.py      → Brevo email — verification + reset templates
    ├── music_service.py    → yt-dlp search + stream URL + filter logic
    └── push_service.py     → Firebase FCM — device, topic, subscribe
```

---

## 🌐 ALL REST API ROUTES

### Auth
| Method | Route | Purpose |
|--------|-------|---------|
| POST | `/auth/register` | Register with name, email, phone, password → sends verify email |
| GET | `/auth/verify?token=` | Verify email via link → returns JWT |
| POST | `/auth/login` | Login with email + password → returns JWT |
| POST | `/auth/forgot-password` | Send reset link to email |
| POST | `/auth/reset-password` | Reset password with token |
| POST | `/auth/refresh` | Refresh JWT token |
| GET | `/auth/profile` | Get user profile + subscription + referral |

### Music
| Method | Route | Purpose |
|--------|-------|---------|
| GET | `/music/search?q=` | Search YouTube — filtered (no movies/TV shows) |
| GET | `/music/stream-url?video_id=` | Get audio URL for download |
| GET | `/music/preview?video_id=` | Get audio URL for 30sec preview |
| GET | `/ping` | Health check |

### Subscription
| Method | Route | Purpose |
|--------|-------|---------|
| GET | `/subscription/status` | Get trial/active/expired status + days left |
| POST | `/subscription/create-order` | Create Razorpay order |
| POST | `/subscription/verify-payment` | Verify payment + activate subscription |
| POST | `/subscription/renew` | Renew existing subscription |

### Referral
| Method | Route | Purpose |
|--------|-------|---------|
| GET | `/referral/code` | Get my referral code + referred users list |
| POST | `/referral/apply` | Apply someone's referral code → +3 days both |
| GET | `/referral/validate?code=` | Check if referral code is valid |

### Games
| Method | Route | Purpose |
|--------|-------|---------|
| POST | `/games/score` | Submit score for a game |
| GET | `/games/leaderboard?game=` | Monthly leaderboard per game |
| GET | `/games/my-scores` | My best scores for all games |

### Stats
| Method | Route | Purpose |
|--------|-------|---------|
| GET | `/stats/global` | Total users, new this month, active subscribers |
| GET | `/config` | App min version, force update, subscription amount |

---

## 🔑 CREDENTIALS & SERVICES

| Service | Purpose | Status |
|---------|---------|--------|
| Neon PostgreSQL | Server database | ✅ Connected |
| Brevo | Email verification + reset | ✅ API key ready |
| Razorpay Test Mode | Subscription payments | ✅ Keys ready |
| Netlify | Verification + reset links | ✅ Live at pandamusicforpandas.netlify.app |
| Firebase | Push notifications | ⏳ Credentials needed in .env |

### Netlify URLs
```
Verify email  → https://pandamusicforpandas.netlify.app/verify?token=xxx
Reset password → https://pandamusicforpandas.netlify.app/reset?token=xxx
```

---

## 🗄️ DATABASE TABLES (Neon PostgreSQL)

| Table | Columns |
|-------|---------|
| `users` | id, name, email, phone, password_hash, is_verified, verify_token, verify_token_expiry, reset_token, reset_token_expiry, created_at, last_login |
| `subscriptions` | id, user_id, status, trial_start, trial_end, sub_start, sub_end, razorpay_order_id, razorpay_payment_id, created_at |
| `referrals` | id, user_id, referral_code, referred_by, total_referrals, created_at |
| `game_scores` | id, user_id, user_name, game, score, submitted_at |

**Local device SQLite (Flutter):**

| Table | Columns |
|-------|---------|
| `playlists` | id, name, createdAt, iconPath |
| `songs` | id, playlistId, title, videoId, youtubeUrl, thumbnailUrl, thumbnailPath, localPath, durationMs, isCached, sortOrder, addedAt, cutRangesJson, pendingDownload |

---

## 📦 FLUTTER PACKAGES USED

| Package | Purpose |
|---------|---------|
| `just_audio` | Audio playback Android + Windows |
| `audio_service` | Background play + lock screen controls |
| `just_audio_background` | Background audio session |
| `dio` | HTTP client + download + interceptors |
| `connectivity_plus` | Internet check |
| `sqflite` | Android SQLite |
| `sqflite_common_ffi` | Windows SQLite |
| `shared_preferences` | Key-value storage |
| `cached_network_image` | Thumbnail caching |
| `shimmer` | Skeleton loading animation |
| `lottie` | Animations |
| `flutter_svg` | SVG icons |
| `local_auth` | Biometric fingerprint/face |
| `flutter_secure_storage` | JWT token secure storage |
| `firebase_core` | Firebase base |
| `firebase_messaging` | Push notifications |
| `flutter_local_notifications` | Local notifications |
| `workmanager` | Background download worker |
| `provider` | State management |
| `noise_meter` | Microphone for Voice Panda game |
| `flutter_launcher_icons` | Auto generate all icon sizes |

---

## 📦 BACKEND PACKAGES USED

| Package | Purpose |
|---------|---------|
| `flask` | Web framework |
| `psycopg2-binary` | PostgreSQL connection |
| `python-dotenv` | Load .env file |
| `PyJWT` | JWT token generation + verification |
| `bcrypt` | Password hashing |
| `sib-api-v3-sdk` | Brevo email sending |
| `yt-dlp` | YouTube audio URL extraction + search |
| `razorpay` | Payment processing |
| `firebase-admin` | Push notifications |
| `gunicorn` | Production WSGI server for Render |

---

## 🚀 NEXT STEPS — RECOMMENDED ORDER

### Backend (Remaining)
```
1. Deploy to Render → set all env vars
2. Add Firebase credentials to .env
3. Update Netlify verify.html + reset.html pages properly
4. Test all API routes with Postman
```

### Flutter (Remaining — in order)
```
1.  download_service.dart        → Dio download + resume
2.  player_service.dart          → just_audio + queue + cut ranges
3.  player_provider.dart         → player state management
4.  notification_service.dart    → Firebase + local notifications
5.  cache_manager.dart           → audio cache management
6.  sleep_schedule_service.dart  → sleep timer logic
7.  subscription_service.dart    → Razorpay + status check
8.  splash_screen.dart           → panda logo + loading
9.  login_screen.dart            → email + password
10. register_screen.dart         → full registration form
11. verify_email_screen.dart     → check inbox screen
12. forgot/reset password screens
13. pin_entry_screen.dart        → PIN lock
14. mobile_root.dart             → bottom nav shell
15. playlists_tab.dart           → main screen
16. playlist_screen.dart         → songs list
17. search_screen.dart           → search + preview + download
18. now_playing_screen.dart      → full player UI
19. mini_player.dart             → mini player bar
20. profile_tab.dart             → subscription + referral + stats
21. edit_song_screen.dart        → rename + trim + thumbnail
22. games_tab.dart               → 5 games grid
23. 5 game files                 → 2048, block, arrow, bus, voice
24. windows_root.dart            → sidebar shell
25. windows tabs (3 files)       → wider layouts
26. App icon setup               → flutter_launcher_icons
27. Deep link setup              → pandamusic:// scheme
28. AndroidManifest.xml          → permissions + deep link
```

---

## 📊 OVERALL PROGRESS

| Area | Done | % |
|------|------|---|
| Flutter Core/Constants/Theme | ✅ | 100% |
| Flutter Database Layer | ✅ | 100% |
| Flutter Auth Service + Provider | ✅ | 100% |
| Flutter API Service | ✅ | 100% |
| Flutter Download + Playlist Provider | ✅ | 100% |
| Flutter Player Service + Provider | ❌ | 0% |
| Flutter Other Services | ❌ | 0% |
| Flutter UI — Auth | ❌ | 0% |
| Flutter UI — Mobile Shell | ❌ | 0% |
| Flutter UI — Windows Shell | ❌ | 0% |
| Flutter UI — Screens | ❌ | 0% |
| Flutter Games | ❌ | 0% |
| Backend — All Files | ✅ | 100% |
| Backend — Deploy to Render | ❌ | 0% |
| Backend — Firebase Setup | ❌ | 0% |
| **TOTAL** | | **~40%** |

---
*Next session: Deploy backend to Render → then start Flutter download_service.dart*
