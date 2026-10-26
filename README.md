## Few-Shot CLIP Adaptation on Oxford Flowers102

Project for the **Deep Learning** course at the University of Trento.

This project studies few-shot adaptation of CLIP on Oxford Flowers102 with 10 shots per base class. I evaluate base and novel accuracy and the harmonic mean, and compare multiple prompt-based adaptation strategies.

## Methods Tried (Brief)

- Zero-shot CLIP baseline.
- CoOp (class-agnostic): a single learned prompt shared across classes.
- CoOp (class-specific): one learned prompt per base class.
- CoOp (hybrid): class-specific prompts for base classes and a shared prompt for novel classes.
- CoOp (dynamic-weighted): per-image weighted mix of base prompts for novel classes.
- Naive hybrid: CoOp for base classes, zero-shot CLIP for novel classes.
- Unified 102-class evaluation to test real-world performance.

## Highlight: Dynamic Thresholding (Final Method)

The final method uses class-specific CoOp prompts to compute a confidence gap between the top-1 and top-2 prompt scores. If the gap exceeds a threshold, the image is treated as a base-class example and evaluated with CoOp prompts; otherwise it falls back to zero-shot CLIP. This adaptive routing preserves novel-class accuracy while improving base-class accuracy, and it yields the best overall trade-off under unified evaluation. A cross-validation procedure on base classes is used to set the threshold without leaking novel data.

## Results

| Method | Base Acc | Novel Acc | Harmonic Mean |
|---|---:|---:|---:|
| Zero-shot | 66.92% | 74.24% | 70.39% |
| CoOp (Agnostic) | 77.68% | 71.93% | 74.69% |
| CoOp (Specific) | 72.91% | 71.82% | 72.36% |
| CoOp (Hybrid) | 61.18% | 74.10% | 67.02% |
| CoOp (Dynamic) | 72.75% | 71.82% | 72.28% |
| Naive (Hybrid) | 46.74% | 78.18% | 58.51% |
| CoOp (CV Threshold 0.135 - Conservative) | 71.17% | 74.24% | 72.67% |
| CoOp (CV Threshold 0.043 - Opt) | **78.41%** | 73.99% | **76.14%** |

### Takeaway

The best trade-off under unified evaluation is achieved by **threshold-based routing** (including the CV-estimated optimal threshold), which improves harmonic mean from **70.39%** (zero-shot unified) to **76.14%** while keeping novel performance close to the zero-shot baseline.
