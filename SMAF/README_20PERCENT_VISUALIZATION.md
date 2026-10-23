# ACDC 20% qualitative and feature visualization

In PyCharm, right-click and run:

```text
RUN_RCFM_20PERCENT_VISUALIZE.py
```

The first run trains one full RCFM configuration with 14 labeled cases (20%)
and seed 2023. It keeps all previous 5% runs unchanged, uses an independent
subprocess, and resumes from a compatible `last.pt` after a process crash.
After training, it creates the same fixed Q25/Q50/Q75 qualitative slices used
by the comparison methods and a 600-DPI pixel-feature t-SNE figure.

The t-SNE points are clean EMA-teacher decoder features immediately before the
segmentation head. BG, RV, Myo, and LV are sampled with equal counts from the
same 40 test cases and fixed slices, and colors always come from ground truth.
Sampling coordinates and t-SNE parameters are saved with the figure so later
baselines can be compared on exactly the same pixels.
