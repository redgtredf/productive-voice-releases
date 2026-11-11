# Changelog

All notable changes to Productive Voice. Newest first. Dates are the day the work was finished.

## 0.5.1 (in preparation, 2026-11-11)

### Fixed: long recordings
- AssemblyAI recordings failed on upload because of a header Electron rejects. The header is removed.
- A server error page (for example a Deepgram 504) now shows "returned HTTP 504", not a technical code message.
- Long recordings upload as a small compressed copy (Ogg/Opus, 32 kbps, about 10 MB per hour instead of about 116 MB). Your original audio is not changed. Before, a long recording could time out on an ordinary connection. Groq accepts files up to 25 MB: a longer recording asks you to use Deepgram or AssemblyAI.
- Transcribing a recording again no longer deletes the old transcript if the new attempt fails. The error shows on the card, and you can try again.
- A summary or timeline that was still being written when you transcribed again is dropped, not saved against the wrong text. Transcribing again clears the summary and timeline that were made from the old text.
- A recording with no speech says "No speech was found" and offers no summary.
- A recording left "Transcribing..." by a crash or a quit is reset when the app starts.
- Speaker labels or chapters that a provider refuses (HTTP 400) no longer stop the transcript: the app tries again without them.
- A recording with one speaker now gets a timeline (AssemblyAI; built from the word times in the provider's reply, not yet checked against a live reply).
- AI errors now show the provider's own message. Rate limits (HTTP 429) wait and try again. Models that think at length and run out of output space get one retry with more room.

### Fixed: first-run setup
- The first-run screen recommends one provider (OpenRouter) and stores a model that matches the provider you choose. Before, choosing "Anthropic (Recommended)" or OpenAI direct could leave a model that made the first dictation fail.
- Key checks use the provider you saved, not the model name. A provider and model that do not match give a plain message, with no request sent.
- Removed the claims that audio is processed locally and that the app can run in an "Offline Mode". The app has no offline speech-to-text.

### Privacy and security
- HIPAA-safe routing (renamed from "HIPAA Compliant Mode") now applies to recordings as well as live dictation. Before, a recording could still go to Groq with the mode on. It does not make the app HIPAA compliant: you need your own agreements with the providers.
- Logs no longer contain HTTP headers or cookies from a failed update check, or text you dictated.
- The support report is redacted for keys, tokens, cookies and e-mail addresses, and is shown to you before anything is copied.
- Development switches (`NODE_ENV`, `PV_DEV_*`, DevTools) have no effect in the installed app. The installed app can only show its own pages. `LICENSE_SERVER_URL` is ignored in the installed app.
- Stricter page security policy: no inline scripts. The Inter font is part of the app, so no font server is contacted.
- The speech-language setting, imported file paths, audio chunks and the "paste from history" request are checked. Files outside the app's own folders cannot be read or deleted through the archive code.
- Removed two unused native packages.

### Changed
- New option "Never press Enter in terminals" (on by default). "Press Enter After Paste" no longer sends Enter into Windows Terminal, Command Prompt, PowerShell, WSL and similar. A terminal inside an editor (for example the VS Code terminal) cannot be detected.
- Model list and prices refreshed (GPT-6.1 Terra, GPT-6 Luna and Luna Pro, Gemini 3.8 Flash, DeepSeek V4.1 Flash added). `npm run models:check` and `models:sync` compare the list with OpenRouter. The "Custom..." model choice in Settings works.
- Updates now come from a public releases page: https://github.com/redgtredf/productive-voice-releases. If the update server cannot be reached, Settings says so calmly, and the app checks once a day instead of every six hours. This version must be installed by hand once, because earlier versions look for updates in a repository that is not public.
- The installer is smaller: koffi's binaries for other systems are left out.
- Includes the licence clock-policy fix from the main branch: a clock set back never locks the app and never starts a fresh trial.

### Known gaps
- The installer is not code-signed. Windows SmartScreen may warn.
- AssemblyAI and Groq were not tested against live accounts in this release (no keys). Deepgram was. OpenAI-direct requests were checked in unit tests, not live.
- API keys are still readable by the settings screen's code. A safer arrangement is planned.

## 0.5.0 (2026-11-10)
- AI summaries of long recordings, with five templates (meeting, client call, lecture, interview, brain dump).
- Speaker labels ("who said what"), with renaming; summaries use the names you choose.
- A chapter timeline for each recording; click a chapter to play the audio from there.
- In-app update flow (ready dialog, manual check, re-check every six hours).
- Licence: clock policy and signed-error handling; crash dumps; a single support address; Electron 42.11.18.
- AssemblyAI language setting and more patient polling.
- HIPAA mode forces the OpenAI provider and its safe model together.

## 0.4.0 (2026-09-10)
- Uniform licence gate: development builds no longer bypass it.
- The 30-day trial is anchored to the licence server, so reinstalling or wiping settings does not restart it. Offline grace of 7 days is kept.
- Dependency audit cleared (0 known problems).
- Pill fixes: "Hide this for 1 hour", growth away from screen edges, a visible tooltip.
- Recording guards: a recording is not lost when another dictation starts.
- Presenter remote: a key hook that does not consume the keys.
