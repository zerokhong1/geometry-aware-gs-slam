# Statistical Analysis of Experiment Results

## SLAM Non-Determinism

ORB-SLAM3 exhibits non-deterministic behavior due to multi-threading in feature extraction and tracking. We measured this variance by running the **same config** 10 times on Replica room0:

| Metric | Mean | Std | Min | Max | Range |
|--------|------|-----|-----|-----|-------|
| PSNR | 30.12 | 0.28 | 29.61 | 30.84 | 1.23 |
| SSIM | 0.910 | 0.004 | 0.903 | 0.917 | 0.014 |
| ATE (cm) | 0.65 | 0.12 | 0.45 | 0.89 | 0.44 |

**Conclusion**: Single-run comparisons in GS-SLAM papers can show differences up to ±0.84 dB that are purely from SLAM randomness, not from method changes. Our 3×3 protocol (3 runs per config, report mean) mitigates this.

## Significance of +OC+CS Improvement

Paired t-test comparing Baseline vs +OC+CS across all 8 scenes (using per-scene means of 3 runs):

- **PSNR**: t(7) = 8.42, p < 0.001 (significant)
- **SSIM**: t(7) = 6.91, p < 0.001 (significant)
- **LPIPS**: t(7) = -7.15, p < 0.001 (significant)

The +0.42 dB average improvement is statistically significant and exceeds the measured SLAM variance.

## ED Component Analysis

Enhanced Densification shows improvement over baseline but degrades from +OC+CS:

| Comparison | Δ PSNR | p-value | Significant? |
|------------|--------|---------|--------------|
| Full vs Baseline | +0.25 | 0.003 | Yes |
| Full vs +OC+CS | -0.17 | 0.021 | Yes (negative) |

ED adds noise from unconverged Gaussians in the online setting. This is consistent with our hypothesis that offline densification assumptions break under SLAM's streaming constraint.
