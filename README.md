<p align="center">
  <img src="logo.png" width="350" alt="tinylens logo" /><br>
  <strong>Tidy image analysis for digital humanities and film studies</strong>
</p>

<p align="center">
<a href="https://github.com/nabsiddiqui/tinylens"><img src="https://img.shields.io/badge/R--CMD--check-passing-brightgreen" alt="R-CMD-check"></a>
<a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
</p>

---

**tinylens** is an R package for analyzing images and videos in a way that fits naturally into tidyverse workflows. Every function takes a tibble and returns a tibble with added columns—no list-columns, no nested structures, just tidy data.

## What It Does

- 📹 **Video Processing**: Detect shots, extract frames, compute pacing metrics
- 🎨 **Color Analysis**: Brightness, saturation, warmth, dominant colors (11 functions)
- 📐 **Composition**: Rule of thirds, visual complexity, center bias
- 🎬 **Film Metrics**: Shot scale (9 types), camera angles (6 types), ASL
- 🤖 **Local LLM**: Image descriptions via Ollama (no cloud APIs)
- 🔊 **Audio**: Loudness and spectral features per shot

## Installation

```r
devtools::install_github("nabsiddiqui/tinylens")
```

## Quick Example

```r
library(tinylens)

# Analyze a video
shots <- video_extract_shots("my_film.mp4") |>
  extract_brightness() |>
  extract_colourfulness() |>
  film_classify_angle()

# Get summary stats
film_compute_asl(shots)          # Average shot length
film_summarize_scales(shots)     # Shot scale distribution
```

Output is a tibble with one row per shot and 60+ feature columns:

```r
# A tibble: 15 × 62
   id         shot_id duration shot_scale brightness colourfulness warmth ...
   <chr>        <int>    <dbl> <chr>           <dbl>         <dbl>  <dbl> ...
 1 frame_001        1     12.5 MS              0.456          34.2  0.123 ...
 2 frame_026        2      8.0 CU              0.512          28.9  0.089 ...
```

## Function Overview

| Category | Functions | What They Add |
|----------|-----------|---------------|
| **Video** | `video_extract_shots()`, `video_sample_frames()` | shot_id, duration, start_time, end_time |
| **Color** | `extract_brightness()`, `extract_colourfulness()`, `extract_warmth()`, ... | brightness, colourfulness, warmth, tint, dominant_hex |
| **Film** | `film_classify_scale()`, `film_classify_angle()` | shot_scale, camera_angle |
| **Composition** | `extract_rule_of_thirds()`, `extract_center_bias()` | thirds_score, center_bias |
| **LLM** | `llm_describe()`, `llm_classify()` | description, category |

## Required Packages

magick, tibble, dplyr, purrr, cli

**Optional**: av (video), tuneR (audio), torch (embeddings), httr2 (LLM)

## License

MIT © Nabeel Siddiqui

---

*If you use tinylens in research, please cite: Siddiqui, N. (2026). tinylens: Tidy Image Analysis for Digital Humanities. https://github.com/nabsiddiqui/tinylens*
