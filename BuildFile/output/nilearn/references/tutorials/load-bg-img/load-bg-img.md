# How To: Load Bg Img

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test load bg img

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `base64`
- `io`
- `numpy`
- `pytest`
- `matplotlib`
- `nibabel`
- `nilearn`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.plotting._engine_utils`
- `nilearn.plotting.html_stat_map`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: Assign affine = affine_eye

```python
affine = affine_eye
```

### Step 2: Assign unknown = value

```python
affine[0, 0] = -1
```

### Step 3: Assign unknown = 0.1

```python
affine[0, 1] = 0.1
```

### Step 4: Assign unknown = _simulate_img(...)

```python
img, _ = _simulate_img(affine)
```

### Step 5: Assign unknown = load_bg_img(...)

```python
bg_img, _, _, _ = load_bg_img(img, bg_img=None)
```

### Step 6: Call _check_affine()

```python
_check_affine(bg_img.affine)
```

### Step 7: Assign unknown = load_bg_img(...)

```python
bg_img, _, _, _ = load_bg_img(img)
```

### Step 8: Call _check_affine()

```python
_check_affine(bg_img.affine)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
affine = affine_eye
affine[0, 0] = -1
affine[0, 1] = 0.1
img, _ = _simulate_img(affine)
bg_img, _, _, _ = load_bg_img(img, bg_img=None)
_check_affine(bg_img.affine)
bg_img, _, _, _ = load_bg_img(img)
_check_affine(bg_img.affine)
```

## Next Steps


---

*Source: test_html_stat_map.py:189 | Complexity: Advanced | Last updated: 2026-05-18*