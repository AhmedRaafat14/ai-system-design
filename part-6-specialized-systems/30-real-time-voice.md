# 30. Real-Time Voice AI

*Part VI. Specialized Systems · [Reading list](../README.md)*

Voice agents are a systems-latency problem first and a model-quality
problem second.

- **Pipeline**: VAD (voice activity detection) → streaming STT → LLM →
  streaming TTS, or an end-to-end speech-to-speech model. Pipelines give
  control, [observability](../part-4-production-engineering/22-observability.md), and component-level swaps; speech-to-speech cuts
  latency and preserves prosody but reduces control. Most production
  systems still run pipelines.
- **Latency budget**: target well under a second voice-to-voice; humans
  read silence beyond that as failure. Stream every stage: partial STT into
  the LLM, first LLM sentence into TTS while the rest generates. Measure
  p95 voice-to-voice, not averages.
- **Turn-taking**: endpointing (when has the caller finished?) and barge-in
  (caller interrupts playback: stop TTS, cancel generation, keep state)
  make or break the experience. Test with real interruption patterns.
- **Reality of audio**: telephony codecs, background noise, code-switching,
  and dialects destroy lab WER numbers. Evaluate STT per dialect and per
  channel (phone vs web) on your own recordings.
- Everything from Parts III-IV still applies: budgets per call, tool
  confirmation for consequential actions, fallback to a human as a
  first-class flow (and legally required disclosure that the caller is
  talking to an AI in a growing number of jurisdictions, see §34).
- Voice-specific [evals](../part-4-production-engineering/21-evaluation-strategy.md): WER/CER per dialect, endpointing errors,
  interruption handling, task completion, latency percentiles, and TTS
  quality (MOS-style human scoring plus pronunciation checks on domain
  vocabulary and names).

---

**Prev:** [29. Document Processing and OCR](../part-5-data-engineering/29-document-processing-and-ocr.md) · [Reading list](../README.md) · **Next:** [31. Multilingual and Arabic-Specific Notes](31-multilingual-and-arabic.md)
