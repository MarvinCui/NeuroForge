# How To: Check Peak Size

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check peak size

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.direction.peaks`
- `dipy.testing.decorators`
- `dipy.viz.horizon.util`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign peak_dirs = rng.random(...)

```python
peak_dirs = rng.random((100, 100, 100, 10, 6))
```

### Step 2: Assign pam = PeaksAndMetrics(...)

```python
pam = PeaksAndMetrics()
```

### Step 3: Assign pam.peak_dirs = peak_dirs

```python
pam.peak_dirs = peak_dirs
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(True, check_peak_size([(pam, None)]))
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(True, check_peak_size([(pam, None), (pam, None)]))
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(False, check_peak_size([(pam, None)], ref_img_shape=(100, 100, 1), sync_imgs=True))
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(False, check_peak_size([(pam, None)], ref_img_shape=(100, 100, 100), sync_imgs=False))
```

### Step 8: Assign pam1 = PeaksAndMetrics(...)

```python
pam1 = PeaksAndMetrics()
```

### Step 9: Assign peak_dirs_1 = rng.random(...)

```python
peak_dirs_1 = rng.random((100, 100, 50, 10, 6))
```

### Step 10: Assign pam1.peak_dirs = peak_dirs_1

```python
pam1.peak_dirs = peak_dirs_1
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal(False, check_peak_size([(pam, None), (pam1, None)]))
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(False, check_peak_size([(pam, None), (pam1, None)], ref_img_shape=(100, 100, 100), sync_imgs=True))
```

### Step 13: Call npt.assert_equal()

```python
npt.assert_equal(False, check_peak_size([(pam, None), (pam1, None)], ref_img_shape=(100, 100, 100), sync_imgs=False))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
peak_dirs = rng.random((100, 100, 100, 10, 6))
pam = PeaksAndMetrics()
pam.peak_dirs = peak_dirs
npt.assert_equal(True, check_peak_size([(pam, None)]))
npt.assert_equal(True, check_peak_size([(pam, None), (pam, None)]))
npt.assert_equal(False, check_peak_size([(pam, None)], ref_img_shape=(100, 100, 1), sync_imgs=True))
npt.assert_equal(False, check_peak_size([(pam, None)], ref_img_shape=(100, 100, 100), sync_imgs=False))
pam1 = PeaksAndMetrics()
peak_dirs_1 = rng.random((100, 100, 50, 10, 6))
pam1.peak_dirs = peak_dirs_1
npt.assert_equal(False, check_peak_size([(pam, None), (pam1, None)]))
npt.assert_equal(False, check_peak_size([(pam, None), (pam1, None)], ref_img_shape=(100, 100, 100), sync_imgs=True))
npt.assert_equal(False, check_peak_size([(pam, None), (pam1, None)], ref_img_shape=(100, 100, 100), sync_imgs=False))
```

## Next Steps


---

*Source: test_util.py:141 | Complexity: Advanced | Last updated: 2026-05-18*