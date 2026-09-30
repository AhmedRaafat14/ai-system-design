# 28. Synthetic Data

*Part V. Data Engineering · [Reading list](../README.md)*

- Best uses: augmenting rare classes and edge cases, generating format
  examples for SFT, building [eval](../part-4-production-engineering/21-evaluation-strategy.md) variants, and distillation traces from a
  strong teacher (check the teacher's terms of use).
- **Never ship unverified synthetic data.** Filter with deterministic
  checks plus an LLM judge, then human-sample. Generation is cheap;
  verification is the actual work.
- Keep real data in the mix and track the synthetic ratio. Training
  recursively on model output degrades quality and diversity (the "model
  collapse" failure mode documented in the literature).
- Label provenance: every synthetic example tagged as such, with generator
  model and prompt version, so it can be excluded or reweighted later.

---

**Prev:** [27. Annotation Operations](27-annotation-operations.md) · [Reading list](../README.md) · **Next:** [29. Document Processing and OCR](29-document-processing-and-ocr.md)
