# TXT (txt.73.nu)

A tiny in-browser text and code viewer/editor that keeps everything in the URL.

**Live:** https://txt.73.nu

## What it does
- Edit text directly in the browser
- Syntax highlight the content (auto-detect or choose a language)
- Toggle line wrapping
- Share the content by sharing the URL
- Download the current text using the detected or selected file type

## How it works
- The editor state is stored in the URL **hash** (`#...`), not on a server.
- When you type, the text is encoded and written to `location.hash` using `history.replaceState`, so the page does not reload.
- On load (or when the hash changes), the page decodes the hash back into text and restores:
  - wrapping on/off
  - language selection (Auto or locked)
  - the text itself
- To keep URLs shorter, it picks the smallest encoding among a few options (for example URL-encoding, LZ-based compression, and optionally browser compression streams when available).
- Highlighting is done client-side (Highlight.js). In Auto mode it tries to detect a language; in locked mode it uses the selected language.
- The download button exports the current text as a file with an extension and MIME type that match:
  - the detected language (Auto mode), or
  - the selected language (locked mode)

## Limits
- Because everything is in the URL hash, very large content can hit browser and platform URL limits.
- Auto language detection can be imperfect for short snippets.
