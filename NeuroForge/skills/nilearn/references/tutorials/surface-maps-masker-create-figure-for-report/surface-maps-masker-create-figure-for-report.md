# How To: Surface Maps Masker Create Figure For Report

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check figure generated in report of SurfaceMapsMasker.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.datasets`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: src_masker, mask_img, img, hemi
```

## Step-by-Step Guide

### Step 1: 'Check figure generated in report of SurfaceMapsMasker.'

```python
'Check figure generated in report of SurfaceMapsMasker.'
```

### Step 2: Assign tmp = _surface_mask_img(...)

```python
tmp = _surface_mask_img()
```

### Step 3: Assign data = value

```python
data = {'right': np.zeros(tmp.data.parts['right'].shape, dtype=np.float32), 'left': np.zeros(tmp.data.parts['left'].shape, dtype=np.float32)}
```

### Step 4: Assign unknown = unknown.astype(...)

```python
data[hemi] = tmp.data.parts[hemi].astype(np.float32)
```

### Step 5: Assign unknown = find_surface_clusters(...)

```python
clusters, labels = find_surface_clusters(tmp.mesh.parts[hemi], tmp.data.parts[hemi])
```

### Step 6: Assign max_size = unknown.max(...)

```python
max_size = clusters['size'].max()
```

### Step 7: Assign idx_biggest_cluster = unknown.to_numpy(...)

```python
idx_biggest_cluster = clusters['index'][clusters['size'] == max_size].to_numpy()
```

### Step 8: Assign unknown = 0

```python
data[hemi][labels != idx_biggest_cluster] = 0
```

### Step 9: Assign maps_imgs = at_least_2d(...)

```python
maps_imgs = at_least_2d(new_img_like(tmp, data))
```

### Step 10: Assign masker = src_masker(...)

```python
masker = src_masker(maps_imgs, mask_img=mask_img)
```

### Step 11: Call masker.fit()

```python
masker.fit(img)
```

### Step 12: Assign unknown = 'matplotlib'

```python
masker._report_content['engine'] = 'matplotlib'
```


## Complete Example

```python
# Setup
# Fixtures: src_masker, mask_img, img, hemi

# Workflow
'Check figure generated in report of SurfaceMapsMasker.'
tmp = _surface_mask_img()
data = {'right': np.zeros(tmp.data.parts['right'].shape, dtype=np.float32), 'left': np.zeros(tmp.data.parts['left'].shape, dtype=np.float32)}
data[hemi] = tmp.data.parts[hemi].astype(np.float32)
clusters, labels = find_surface_clusters(tmp.mesh.parts[hemi], tmp.data.parts[hemi])
max_size = clusters['size'].max()
idx_biggest_cluster = clusters['index'][clusters['size'] == max_size].to_numpy()
data[hemi][labels != idx_biggest_cluster] = 0
maps_imgs = at_least_2d(new_img_like(tmp, data))
masker = src_masker(maps_imgs, mask_img=mask_img)
masker.fit(img)
masker._report_content['engine'] = 'matplotlib'
return masker._create_figure_for_report(maps_imgs, bg_img=img)[0]
```

## Next Steps


---

*Source: test_baseline_comparisons.py:206 | Complexity: Advanced | Last updated: 2026-05-18*