# Chords & Emotions

A jsPsych 8 online experiment investigating the emotional connotations of musical chord pairs. Designed to run on [Pavlovia](https://pavlovia.org/).

## Live demo

Hosted via GitHub Pages: `https://<your-username>.github.io/<repo-name>/`

## Task

Participants hear 48 chord pairs presented in random order. For each pair they:

1. Listen to **Chord 1** (~1.5 s)
2. Listen to **Chord 2** (~1.5 s)
3. Type a brief free-text description of the emotional quality
4. Rate **Valence** (1 = very unpleasant → 5 = very pleasant) via SAM scale
5. Rate **Arousal** (1 = very calm → 5 = very excited) via SAM scale

Ratings can be made by clicking the SAM images or pressing **1–5** on the keyboard.

## Project structure

```
index.html          Main experiment file (single-page, no build step)
img/
  sam_valence_1-5.png   SAM manikin images for valence (add before running)
  sam_arousal_1-5.png   SAM manikin images for arousal (add before running)
.github/workflows/
  deploy.yml        GitHub Actions workflow — auto-deploys to GitHub Pages on push to main
```

## Setup

### Dependencies (loaded via CDN — no install required)

- [jsPsych 8.2.3](https://www.jspsych.org/)
- `@jspsych/plugin-html-keyboard-response`
- `@jspsych/plugin-html-button-response`
- `@jspsych/plugin-survey-text`

### SAM images

The Self-Assessment Manikin images are **not** included. Add your own files to `img/`:

| File | Scale point |
|------|-------------|
| `sam_valence_1.png` | Very unpleasant |
| `sam_valence_2.png` | Unpleasant |
| `sam_valence_3.png` | Neutral |
| `sam_valence_4.png` | Pleasant |
| `sam_valence_5.png` | Very pleasant |
| `sam_arousal_1.png` | Very calm |
| `sam_arousal_2.png` | Calm |
| `sam_arousal_3.png` | Moderate |
| `sam_arousal_4.png` | Excited |
| `sam_arousal_5.png` | Very excited |

### Chord pairs

The 48 placeholder chord pairs in `index.html` (the `CHORD_PAIRS` array near the top of the script) should be replaced with the actual stimulus list. Each entry has the form:

```js
{ id: 1, chord1: "C major", chord2: "C minor" }
```

Audio files are not yet wired up. The chord display phase currently shows a text placeholder; replace the `html-keyboard-response` chord trials with an audio-response plugin when MP3s are available.

## Data

At the end of each session jsPsych outputs a CSV with one row per sub-trial. Key columns:

| Column | Description |
|--------|-------------|
| `pair_id` | Chord pair number (1–48) |
| `chord1` / `chord2` | Chord names |
| `phase` | `chord1`, `chord2`, `free_text`, `valence`, or `arousal` |
| `response` | Raw jsPsych response |
| `valence` | Numeric rating 1–5 (valence rows only) |
| `arousal` | Numeric rating 1–5 (arousal rows only) |
| `rt` | Reaction time in ms |

## Deploying to Pavlovia

1. Replace the `on_finish` handler in `initJsPsych` with the Pavlovia data-save call.
2. Add the Pavlovia plugin and initialisation/finish trials to the timeline.
3. Upload the repository to Pavlovia via GitLab sync.
