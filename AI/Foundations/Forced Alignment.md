---
type: atomic
tags: [ai/ml, ai]
date: 2026-10-04
---

# Forced Alignment

## Idea
Forced alignment takes audio and a transcript you already have and works out exactly when each word (or sound) was spoken.

## Definition
Speech recognition answers "what was said"; **forced alignment** answers "when", given the text. An acoustic model scores how well each short audio frame matches each phoneme, and a dynamic-programming search (Viterbi or CTC alignment) finds the best path that walks through the transcript in order. The output is start and end times per word or phoneme, which powers karaoke-style captions, subtitle timing, cutting video at word boundaries and phonetics research. A **voice activity detection** (VAD) step usually splits long audio into speech segments first. A practical gotcha for captions: the last word before a pause tends to be stretched into the following silence, so a word that took 300 ms is reported as lasting two seconds and the caption lingers. Capping word durations (around 700 ms) and trimming against VAD boundaries fixes most of it.

## Tools
- **Montreal Forced Aligner** — Kaldi-based, GMM-HMM aligner widely used in research.
- **WhisperX** — Whisper transcription plus a wav2vec2 phoneme model for word-level timestamps, with VAD-based segmentation.
- **Gentle / aeneas** — older open-source aligners for English and for text-to-audio sync.

## Source
Forced alignment came out of HMM speech recognition; the Penn Phonetics Lab Forced Aligner (Yuan and Liberman, 2008) brought it to linguists. Michael McAuliffe et al. introduced the Montreal Forced Aligner (Interspeech 2017), and Max Bain et al. published WhisperX (Interspeech 2023).

---

## Compass

**Roots** — *where this comes from*
It is a classic [[Supervised Learning]] application: acoustic models are trained on audio already labelled with phonemes, then reused to label new audio.

**Paths** — *where this leads*
Word timings make transcripts editable like text, and they are the timing layer under any caption pipeline that later splits or styles words.

**Neighbors** — *what lives nearby*
Speech models chop audio into frames much as text models chop text into [[Tokens]], and the timestamps are only as good as the frame size.

**Clash** — *what pushes against this*
It assumes the transcript is correct: a missing or wrong word forces the aligner to bend the timeline around it, a quiet [[Silent Failure]] that looks fine until captions drift out of sync.
