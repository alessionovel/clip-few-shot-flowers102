## Few-Shot CLIP Adaptation on Oxford Flowers102

This project studies few-shot adaptation of CLIP on Oxford Flowers102 with 10 shots per base class. We evaluate base and novel accuracy and the harmonic mean, and compare multiple prompt-based adaptation strategies.

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
