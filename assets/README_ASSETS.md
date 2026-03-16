# Assets — Image Checklist

Replace these placeholders with actual images from your experiments.

## Required images:

### teaser.png
- Side-by-side: Baseline | Ours (+OC+CS) on 2 scenes
- Recommended: room0 and office0 (best visual difference)
- Layout: 2 rows × 2 columns, labeled "Baseline" and "Ours"
- Resolution: at least 1920×960
- Generate from Photo-SLAM-eval full-trajectory renders

### method_overview.png
- Diagram showing OC + CS modifications
- Can export from paper LaTeX figure, or redraw as clean SVG → PNG
- Should clearly show: (1) opacity correction formula on cloned Gaussians,
  (2) pixel cone geometry for scale initialization

### qual_room0.png, qual_office0.png, qual_tum_desk.png
- Close-up crops showing quality difference
- 3 columns: Input RGB | Baseline | Ours
- Pick regions where improvement is most visible (textures, edges, distant walls)
- Inset zoom boxes for fine detail

### video_thumbnail.png
- Screenshot from the supplementary video
- Shows the 3-row layout: Input | Baseline | Ours
- Add play button overlay

## How to generate:

```bash
# From Photo-SLAM-eval output:
cd ~/Congthai-5/output

# Side-by-side comparison:
python make_comparison.py \
    --baseline room0/baseline/renders/ \
    --ours room0/oc_cs/renders/ \
    --output ../paper-repo/assets/qual_room0.png \
    --frame 150 \    # Pick a good frame
    --crop 200,100,600,400  # Interesting region
```
