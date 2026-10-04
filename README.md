# Termux Projects Index

Every program on this device that's come up while working with Claude —
one list, so it's clear which were built together, and which existed
before Claude looked at them. Requested directly, to settle "was this
built with Claude / leaning on Claude, or did I write actual Python on
my own." Kept as one file, on request, rather than split up.

**Honest limit on this list**: it's built from Claude's own session
memory plus what's actually on disk right now — not from any git
history on the files that predate this record (most of them aren't in
a git repo at all, so there's no commit log to check authorship or
dates against). Everything below in the first table has direct
evidence (Claude wrote it, in a recorded session). Everything in the
second table was *found already on this device*, with no record of who
wrote it or when — the description says what evidence exists either
way. There is no entry anywhere in Claude's memory of Gabe having
written Python independently; if that happened, it isn't reflected
here because no record of it exists to draw from.

## Built with Claude — direct record

| Project | Where it lives | What it is |
|---|---|---|
| **Spark** | `~/spark` — [DarkPhilosopher/spark](https://github.com/DarkPhilosopher/spark) | The main WHEN/DO game-creation engine — two engines kept in parity (Python terminal + JS/WebGL browser), `chatshell.py`'s chat-command interface, the tile library, the Outpost RTS game, terrain painting, `look`/`place_it`, `spark browser`. The largest, longest-running project; most of its own history predates what's summarized in current memory — CHANGELOG.md in that repo is the fuller record. |
| **spark2** | `~/spark2` (own git repo, no GitHub remote) | A from-scratch, standalone WHEN/DO-shaped 2D engine — deliberately *not* Spark, built to explore "what's fundamentally required" for a game like it, independent of Spark's own code. |
| **termux-chat** | `~/termux-chat` (own git repo, no remote) | Split-screen ASCII animation + typewriter-effect, paginated chat log toy. |
| **gridplace** | `/sdcard/Download/gridplace` (Downloads, not Termux home; no git) | ASCII cursor/place/color/submit grid toy — pieces flash until submitted. |
| **ASC** | `~/github/termux/android/ASC` — [DarkPhilosopher/ASC](https://github.com/DarkPhilosopher/ASC) | Cursor + fixed 16x16 ASCII grid, type any letter to spawn it; grew a chat/terminal log and a small variable/target/`/when`-`/calc` system. |
| **termux-link** | `~/termux-link` (own git repo, no remote) | Bidirectional FIFO channel (`Link` class) between two independent Termux sessions, plus a `RUN_COMMAND`-based session-opener — confirmed working on-device. |
| **overseer** | `~/bin/overseer` — [DarkPhilosopher/termux-bin](https://github.com/DarkPhilosopher/termux-bin) | One dashboard: a numbered menu (`babymenu.py`, max 8 slots, 7 always back/exit, `a` shows everything at once) plus `/help`/`/list`/`/open`/`/newsession`/`/sessions` for muscle memory, reachable from a pinned Termux:API notification too. |
| **programs** + **catalog_lib.py** | `~/bin/programs`, `~/bin/catalog_lib.py` — same repo | Auto-detecting command lister — scans `$PREFIX/bin` for any shim tagged `# CATALOG: ...` and lists/starts it; numbered, `/open <number>` works. |
| **babymenu.py** | `~/bin/babymenu.py` — same repo | The shared numbered-menu pattern behind `overseer`: up to 8 options, slot 7 always back (or exit at the top level), slot 8 becomes "more..." only once options overflow past 7. |
| **opensession** | `~/bin/opensession` — same repo | Plain-shell wrapper opening a brand-new, independent Termux session via the `RUN_COMMAND` intent — confirmed working on-device. |
| **note3** | `~/bin/note3` — same repo | Generic 3-button Termux notification poster — you supply the labels and the shell command each button runs. |
| **termux-sessions** | `~/bin/termux-sessions` — same repo | Lists/closes real Termux session TABS (not just `claude` processes) — by raw pid, list position number, or tty name (`pts/1`); `kill all` excludes the one you ran it from by default, `--include-self` overrides. |
| **memguard.sh** | `~/bin/memguard.sh` — same repo | Boot-started, runs forever: warns via notification if free RAM drops under 300MB — root-caused after 3 concurrent `claude` sessions forced this phone into heavy swap. |
| **web1** / **web2** | `$PREFIX/bin/web1`, `web2` (one-liners, not in a repo) | Quick top-level shortcuts: `web1` = `spark browser` (Spark's browser/web view), `web2` = plain `spark2`. |
| **PROJECTS-INDEX** | `~/github/termux/android/PROJECTS-INDEX` — [DarkPhilosopher/PROJECTS-INDEX](https://github.com/DarkPhilosopher/PROJECTS-INDEX) | This file. |
| **termux-bin** | `~/bin` — [DarkPhilosopher/termux-bin](https://github.com/DarkPhilosopher/termux-bin) | The repo several rows above actually live in, as of 2026-10-04 — previously had no git history at all. Built specifically so the same programs can be kept current across Gabe's two personal phones (an A17 and an A33): clone it, run its own `install.sh` once to wire up the bare commands, `git pull` + `install.sh` again later to catch up. |

## Found already on this device — no creation record either way

These existed before any Claude session has a memory of building them.
Every one of them is written in the same distinctive style Claude's own
files use elsewhere on this device (a long header docstring/comment
explaining *why*, not just what) — real evidence, but circumstantial,
not a confirmed record the way the table above is. None of them are in
a git repo, so there's no commit history to check dates or authorship
against either.

| File | What it is | Evidence of origin |
|---|---|---|
| `~/bin/termux-panel` | Adds/removes a swipeable panel of extra keys on Termux's own keyboard row, by editing `termux.properties`. | Same long-docstring style as everything above; discussed *as already existing* when Gabe asked about Termux's extra-keys bar. |
| `~/bin/ti.sh` | Notification-based text input with channel switching over tmux, using the same "$REPLY in a button action" trick `overseer notify` was later built to match. | Same style; its own working Reply-button trick is literally what `overseer notify` was modeled on once found. |
| `~/bin/collect-screenshots.py` | Moves screenshot-like files into `/sdcard/ClaudeInbox/screenshots` — a destination named for feeding them to Claude. | The destination path being literally `ClaudeInbox` is fairly strong evidence this was built to work with Claude, even with no session record of building it. |
| `~/.termux-voice/loop.sh`, `toggle.sh`, `notify.sh` | The "Claude Control" voice system — a toggleable background loop using `termux-speech-to-text`, forwarding heard speech into a `claude` tmux session. | `loop.sh` was directly edited this session (added a "claude" wake-word gate + logging) — that edit is a confirmed record, but the *original* three-file system predates it with no creation record. |
| `~/.termux/boot/start-claude.sh` | Termux:Boot entry point — starts the boot-time `claude` tmux session and the voice-control notification. | Edited twice this session (added `memguard.sh`, removed `termux-wake-lock`) — same as above, edits are confirmed, original isn't. |
| `/root/bin/claude-session.sh` (inside the Ubuntu proot container) | Idempotently ensures a tmux session named `claude` is running `claude` inside the container. | Read this session, not written; same style. |

## How to keep this current

Nothing updates this file automatically — it's a snapshot, written by
hand, the same way the table above was compiled from memory. If a new
project gets built, it belongs in the first table; if something new
turns up that already existed with no record, it belongs in the
second, with whatever evidence actually exists for it, not a guess.
