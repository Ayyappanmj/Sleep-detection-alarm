# 😴 Sleep Alarm Detector

Detects when you fall asleep at your desk using your webcam. Shows a **green** face box when you're awake and a **red** pulsing alert when your eyes are closed too long — and plays an alarm sound to wake you up.

---

## Requirements

- Python 3.8+
- Webcam

Install dependencies:

```bash
pip install -r requirements.txt
```

*(or install manually: `pip install mediapipe opencv-python numpy pygame`)*

---

## Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Ayyappanmj/Sleep-detection-alarm.git
   cd Sleep-detection-alarm
   ```

2. **Alarm Sound:**
   A default alarm beep sound (`dragon-studio-censor-beep-3-372460.mp3`) is already included and configured out of the box.
   To use your own sound, place your `.mp3` or `.wav` file in the project folder and update `ALARM_SOUND_FILE` in `sleep_alarm.py`:

   ```python
   ALARM_SOUND_FILE = "your-custom-alarm.mp3"
   ```

3. **(Optional) Tune Settings** at the top of `sleep_alarm.py`:

| Variable | Default | Description |
|---|---|---|
| `EAR_THRESHOLD` | `0.22` | Eye openness threshold — lower = less sensitive |
| `EYE_CLOSED_SECONDS` | `2.5` | Seconds eyes must stay closed to trigger alarm |

---

## Run

```bash
python sleep_alarm.py
```

Press **Q** to quit.

---

## How It Works

| Status | Signal | What's shown |
|---|---|---|
| 👁️ Eyes open | 🟢 Green | Green face box + "AWAKE" pill |
| 😴 Eyes closing | 🟠 Orange bar | Progress bar filling up |
| 🚨 Eyes closed ≥ 2.5s | 🔴 Red | Pulsing red overlay + alarm sound |

- Uses **MediaPipe Face Mesh** to track 468 facial landmarks in real time.
- Computes the **Eye Aspect Ratio (EAR)** for both eyes — when EAR drops below the threshold, the countdown starts.
- Alarm loops until you open your eyes.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Black screen / no camera | Check camera permissions or specify `cv2.VideoCapture(0)` / `cv2.VideoCapture(1)` |
| Alarm not playing | Check that `pygame` is installed and the sound file exists |
| Too many false triggers | Increase `EAR_THRESHOLD` to `0.25` |
| Alarm fires too quickly | Increase `EYE_CLOSED_SECONDS` to `3.0` or higher |
