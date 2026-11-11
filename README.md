# Productive Voice: downloads

Productive Voice is a dictation app for Windows. You press a hotkey, speak, and the text appears in the app you are using.

This repository holds the installers only. It has no source code. The app checks this page for updates.

## Get the app

Download the latest installer from the [Releases](../../releases/latest) page. Run `Productive Voice Setup <version>.exe`.

Requirements: Windows 10 or 11, 64-bit. You bring your own API keys for speech-to-text (Deepgram, AssemblyAI or Groq) and, if you want AI tidy-up, for an AI provider.

## The installer is not signed

The installer has no code-signing certificate yet. Windows SmartScreen may show "Windows protected your PC". This is expected for an unsigned installer.

Before you run it, check the file against the SHA-256 value in the release notes:

```powershell
Get-FileHash -Algorithm SHA256 "C:\Users\<you>\Downloads\Productive Voice Setup <version>.exe"
```

If the two values differ, do not run the file.

## Updates

The app can check this repository for a newer version. It never sends your audio, text or keys here. The only request is for the public update file.

## Licence

Productive Voice needs a licence key. A 30-day trial starts when you first open the app.
