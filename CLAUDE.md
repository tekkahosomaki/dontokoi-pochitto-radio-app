# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

「ポチッとラジオ」(`dontokoi-pochitto-radio-app`, credited to 「どんと来い！ガジェットラボ」) — an internet radio player that runs in the browser from a single HTML file, `apps/pochitto-radio.html`. The on-screen title is 「どんと来い！ポチッとラジオ」. Version 1 plays 27 hard-coded stations (SomaFM, Radio Paradise, KEXP, FIP, Radio Swiss, NTS, Rinse FM, Intergalactic FM; `STATIONS` in the HTML) with play/stop, volume, now-playing and error display. It is published on GitHub Pages at https://tekkahosomaki.github.io/dontokoi-pochitto-radio-app/apps/pochitto-radio.html (the repo is public; a Claude artifact was tried first but its CSP `media-src 'self' data: blob:` blocks external audio — `docs/adr` 0005). The full spec is `docs/design/02-画面と操作.md`; the station list with stream URLs is `docs/design/03-局の一覧.md`.

Playback is a single `<audio>` element: set `src` to the stream URL and `play()` (`docs/adr` 0004). Stop = `pause()` and clear `src` so the stream stops downloading; resuming re-sets the URL and plays live. Don't route audio through Web Audio API (CORS varies by station).

## Constraints

- The whole app is **one HTML file** with CSS and JavaScript inline — no external scripts, stylesheets, fonts, or build step (see `docs/adr` 0001). It must work both on GitHub Pages and opened by double-click (`file://`).
- Only https direct streams (`docs/adr` 0003). When a station URL changes, update both the HTML and `docs/design/03-局の一覧.md`.
- SomaFM returns 403 to curl's default User-Agent, to the Claude desktop app's built-in browser (its UA contains "Claude"), and to some referers (`http://localhost`, `github.io`); `127.0.0.1` and the artifact domains are fine. So SomaFM can't be tested in the built-in browser — verify behaviour with Radio Paradise there, and pass a browser UA when checking streams from the shell.
- The repo is public: commits must use the anonymous identity (どんと来い！ガジェットラボ / GitHub noreply address, set in the global git config) and docs must not contain the local Windows user name — write paths as `C:\Users\<ユーザー名>\...`.
- No test suite, linter, or build. Verify by opening the HTML in a browser and playing stations. Browser automation tools can't drive `file://` pages; serve `apps/` over a local HTTP server instead. Node and Python are not available on the dev PC; a PowerShell `HttpListener` script works.

## Repository layout

```
apps/pochitto-radio.html  The whole app (HTML + inline CSS + inline JS)
docs/adr/                 Architecture decisions, one file per decision, numbered (0001-…)
docs/design/              Design/spec doc, one file per chapter, numbered (01-…)
```

Each `docs/adr` and `docs/design` folder has its own `README.md` acting as an index — read that first when looking for a specific decision or spec chapter.

## Docs conventions

- A new non-trivial technical decision gets a new numbered file in `docs/adr/` (Japanese filename, no spaces, format: ステータス / 背景 / 決定 / 検討した代替案 / 結果・影響) — follow the existing files' structure, and add it to `docs/adr/README.md`'s list.
- A spec/behavior change gets reflected in the relevant chapter file under `docs/design/` (also add new chapters to `docs/design/README.md`'s table of contents if you add one).

## Git workflow

Before running `git commit`, propose the commit message to the user and wait for approval — do not commit immediately even if they've already said "commit this" in general terms.
