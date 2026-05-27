# meditation-timer

A minimal meditation timer for mobile. Set a duration, press start, and it plays an audio cue at the beginning and end of your session.

## How it works

Press start and the intro tone plays. A countdown runs for your chosen duration, then the outro tone plays to signal the end of the session. Press stop at any time to cancel.

Durations: 10, 20, 30, 40, 50, or 60 minutes.

## Staying awake on iPhone

The main challenge for a browser-based timer on iOS is that Safari suspends JavaScript when the screen locks, which means a `setTimeout` scheduled for 30 minutes from now simply won't fire.

This app uses two strategies to work around it:

**Screen Wake Lock** — on start, the app requests the [Screen Wake Lock API](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Wake_Lock_API), which prevents the screen from auto-locking. As long as the screen is on, JavaScript keeps running normally and the outro fires on time. iOS Safari 16.4+ supports this. A status line below the button confirms whether the lock was acquired.

**On-wake recovery** — if the wake lock is released (e.g. the user manually locks the phone and unlocks it), the app recalculates elapsed time when the screen comes back on. If the outro was due while the screen was dark it plays immediately on resume.

The timer uses `Date.now()` rather than a decrementing counter, so gaps from any suspension don't cause drift.

## Usage

Open in Safari on iPhone and add to your home screen for the best experience (Settings → Add to Home Screen). No install, no account, no network required after the first load.

## Audio files

- `med-intro.mp3` — played when the session starts
- `med-outro.mp3` — played 23 seconds before the end (timed to finish at zero)
