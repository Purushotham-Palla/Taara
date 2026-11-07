# Tara • Daily Voice Standup (Native Android App)

Turnkey, production-grade native Android Studio project for **Tara**, your personal AI daily voice standup and accountability partner powered by the **Gemini 2.0 Flash Live Multimodal API**.

---

## 🌟 Why Native Android Solves Every Web Limitation

1. **True Background Lock-Screen Ringing**:
   - Web apps in mobile browsers cannot wake up your phone or trigger real incoming call ringing when locked.
   - This native Android app uses `AlarmManager.setExactAndAllowWhileIdle()` + high-priority `NotificationCompat.Builder` with `fullScreenIntent` to ring your phone and turn on the screen at your exact scheduled standup time, even in Android Doze mode.

2. **Native Low-Latency Audio Streaming**:
   - `AudioRecord` at 16,000 Hz, 16-bit PCM Mono.
   - Built-in hardware **Acoustic Echo Canceler (`AcousticEchoCanceler`)** and **Noise Suppressor (`NoiseSuppressor`)** so Tara's voice coming out of the loudspeaker never bleeds back into the microphone.
   - `AudioTrack` at 24,000 Hz streaming playback with instant barge-in buffer flush when speaking.

3. **Gemini 2.0 Flash Live API**:
   - Connects directly to Google's official bidirectional WebSocket:
     `wss://generativelanguage.googleapis.com/ws/google.ai.generativelanguage.v1beta.GenerativeService.BidiGenerateContent?key=YOUR_API_KEY`
   - Configured with `models/gemini-2.0-flash-exp` (resolving the `Code 1008` model error).

---

## 🚀 How to Run in Android Studio (1 Click)

1. **Extract the ZIP file**:
   Extract `TaraVoiceStandup_Android.zip` on your computer.

2. **Open in Android Studio**:
   - Open Android Studio (Hedgehog, Iguana, Jellyfish, Koala or newer).
   - Select **Open** and choose the `TaraVoiceStandup` folder.
   - Android Studio will automatically sync the Gradle files.

3. **Run on Device or Emulator**:
   - Connect your Android phone via USB (with USB Debugging enabled) or start an Android Emulator.
   - Click the green **Run (▶)** button in Android Studio.

4. **Setup inside the App**:
   - Paste your **Gemini API Key** from [Google AI Studio](https://aistudio.google.com/apikey).
   - Tap **Save Key**.
   - Tap **Run 1-Click Diagnostics** to confirm all 3 steps show green checkmarks.
   - Tap **Call Me Now (Test Tara's Call)** to test the full-screen ringing and live voice standup immediately!
   - Pick your desired daily standup time (e.g., `09:00 AM`). Tara will wake your phone and call you automatically every day.

---

## 📱 App Structure

- `com.tara.standup.MainActivity`: Dashboard, Time Picker, API key management, Diagnostics.
- `com.tara.standup.IncomingCallActivity`: Real full-screen incoming call UI with ringtone and vibration.
- `com.tara.standup.LiveCallActivity`: Live audio call screen, waveform visualizer, transcript stream, in-call controls.
- `com.tara.standup.gemini.GeminiLiveClient`: OkHttp WebSocket implementation of Gemini Multimodal Live API.
- `com.tara.standup.audio.AudioRecorderManager`: 16kHz PCM audio record with hardware echo cancellation.
- `com.tara.standup.audio.AudioTrackPlayer`: 24kHz PCM audio playback with instant interruption handling.
- `com.tara.standup.alarm.AlarmScheduler` & `AlarmReceiver`: Scheduled background alarm service.
