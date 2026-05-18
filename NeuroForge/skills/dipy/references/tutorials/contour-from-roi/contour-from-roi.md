# How To: Contour From Roi

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test contour from roi

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.align.reslice`
- `dipy.align.tests.test_streamlinear`
- `dipy.data`
- `dipy.direction`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking.stopping_criterion`
- `dipy.tracking.streamline`
- `dipy.tracking.tracker`
- `dipy.utils.optpkg`
- `dipy.viz`


## Step-by-Step Guide

### Step 1: Assign unknown = read_stanford_labels(...)

```python
hardi_img, gtab, labels_img = read_stanford_labels()
```

### Step 2: Assign data = np.asanyarray(...)

```python
data = np.asanyarray(hardi_img.dataobj)
```

### Step 3: Assign labels = np.asanyarray(...)

```python
labels = np.asanyarray(labels_img.dataobj)
```

### Step 4: Assign affine = value

```python
affine = hardi_img.affine
```

### Step 5: Assign white_matter = value

```python
white_matter = (labels == 1) | (labels == 2)
```

### Step 6: Assign classifier = ThresholdStoppingCriterion(...)

```python
classifier = ThresholdStoppingCriterion(csa_peaks.gfa, 0.25)
```

### Step 7: Assign seed_mask = value

```python
seed_mask = labels == 2
```

### Step 8: Assign seeds = utils.seeds_from_mask(...)

```python
seeds = utils.seeds_from_mask(seed_mask, density=[1, 1, 1], affine=affine)
```

### Step 9: Assign streamlines_generator = eudx_tracking(...)

```python
streamlines_generator = eudx_tracking(seeds, classifier, affine, pam=csa_peaks, random_seed=1, sphere=default_sphere, step_size=2, max_angle=45)
```

### Step 10: Assign streamlines = list(...)

```python
streamlines = list(streamlines_generator)
```

### Step 11: Assign streamlines_actor = actor.line(...)

```python
streamlines_actor = actor.line(streamlines, colors=colormap.line_colors(streamlines))
```

### Step 12: Assign seedroi_actor = actor.contour_from_roi(...)

```python
seedroi_actor = actor.contour_from_roi(seed_mask, affine=affine, color=[0, 1, 1], opacity=0.5)
```

### Step 13: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 14: Assign csa_model = CsaOdfModel(...)

```python
csa_model = CsaOdfModel(gtab, sh_order_max=6)
```

### Step 15: Assign csa_peaks = peaks_from_model(...)

```python
csa_peaks = peaks_from_model(csa_model, data, default_sphere, relative_peak_threshold=0.8, min_separation_angle=45, mask=white_matter)
```

### Step 16: Assign sc = window.Scene(...)

```python
sc = window.Scene()
```

### Step 17: Assign sc2 = window.Scene(...)

```python
sc2 = window.Scene()
```

### Step 18: Call sc.add()

```python
sc.add(streamlines_actor)
```

### Step 19: Assign arr3 = window.snapshot(...)

```python
arr3 = window.snapshot(sc, fname=Path(out_dir) / 'test_surface3.png', offscreen=True)
```

### Step 20: Assign report3 = window.analyze_snapshot(...)

```python
report3 = window.analyze_snapshot(arr3, find_objects=True)
```

### Step 21: Call sc2.add()

```python
sc2.add(streamlines_actor)
```

### Step 22: Call sc2.add()

```python
sc2.add(seedroi_actor)
```

### Step 23: Assign arr4 = window.snapshot(...)

```python
arr4 = window.snapshot(sc2, fname=Path(out_dir) / 'test_surface4.png', offscreen=True)
```

### Step 24: Assign report4 = window.analyze_snapshot(...)

```python
report4 = window.analyze_snapshot(arr4, find_objects=True)
```

### Step 25: Call npt.assert_array_less()

```python
npt.assert_array_less(report4.objects, report3.objects + 1)
```


## Complete Example

```python
# Workflow
hardi_img, gtab, labels_img = read_stanford_labels()
data = np.asanyarray(hardi_img.dataobj)
labels = np.asanyarray(labels_img.dataobj)
affine = hardi_img.affine
white_matter = (labels == 1) | (labels == 2)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    csa_model = CsaOdfModel(gtab, sh_order_max=6)
    csa_peaks = peaks_from_model(csa_model, data, default_sphere, relative_peak_threshold=0.8, min_separation_angle=45, mask=white_matter)
classifier = ThresholdStoppingCriterion(csa_peaks.gfa, 0.25)
seed_mask = labels == 2
seeds = utils.seeds_from_mask(seed_mask, density=[1, 1, 1], affine=affine)
streamlines_generator = eudx_tracking(seeds, classifier, affine, pam=csa_peaks, random_seed=1, sphere=default_sphere, step_size=2, max_angle=45)
streamlines = list(streamlines_generator)
streamlines_actor = actor.line(streamlines, colors=colormap.line_colors(streamlines))
seedroi_actor = actor.contour_from_roi(seed_mask, affine=affine, color=[0, 1, 1], opacity=0.5)
with TemporaryDirectory() as out_dir:
    sc = window.Scene()
    sc2 = window.Scene()
    sc.add(streamlines_actor)
    arr3 = window.snapshot(sc, fname=Path(out_dir) / 'test_surface3.png', offscreen=True)
    report3 = window.analyze_snapshot(arr3, find_objects=True)
    sc2.add(streamlines_actor)
    sc2.add(seedroi_actor)
    arr4 = window.snapshot(sc2, fname=Path(out_dir) / 'test_surface4.png', offscreen=True)
    report4 = window.analyze_snapshot(arr4, find_objects=True)
    npt.assert_array_less(report4.objects, report3.objects + 1)
```

## Next Steps


---

*Source: test_fury.py:55 | Complexity: Advanced | Last updated: 2026-05-18*