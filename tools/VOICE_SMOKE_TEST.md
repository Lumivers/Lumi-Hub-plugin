# Lumi-Hub Voice WS Smoke Test

## 1) Prerequisites

- Host WS server is running on `ws://127.0.0.1:8765`
- TTS credentials can be provided by either:
  - Environment variable `DASHSCOPE_API_KEY`
  - Runtime config argument `--api-key` (sent via `VOICE_CONFIG_SET`)
- Voice ID can be provided by either:
  - Environment variable `LUMI_DASHSCOPE_VOICE_ID`
  - Runtime config argument `--voice-id`

## 2) Run

From repository root:

```powershell
python host/tools/ws_voice_smoke_test.py --auto-register --voice-id "your-voice-id"
```

Or provide API key directly without setting env vars:

```powershell
python host/tools/ws_voice_smoke_test.py --auto-register --api-key "your-dashscope-key" --voice-id "your-voice-id"
```

Optional interrupt test:

```powershell
python host/tools/ws_voice_smoke_test.py --auto-register --voice-id "your-voice-id" --interrupt-after-ms 800
```

## 3) Expected Output

- `CONNECT` acknowledged
- `AUTH_RESPONSE` success
- `TTS_STREAM_START`
- multiple `TTS_STREAM_CHUNK`
- `TTS_STREAM_END`

For interrupt case:

- `VOICE_INTERRUPT_ACK`
- `TTS_STREAM_END` status should be `interrupted`

## 4) Common Failures

- `[WinError 1225] ... refused`:
  - Host is not running or port mismatch.
- `No TTS provider registered`:
  - voice extension setup not loaded.
- `Missing API key env: DASHSCOPE_API_KEY`:
  - API key is missing from both environment variable and runtime config.
- `voice_id is required`:
  - set `LUMI_DASHSCOPE_VOICE_ID` or pass `--voice-id`.
