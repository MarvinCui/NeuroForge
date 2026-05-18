# How To: Fit Matched Points

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test fit_matched_points: fitting two matching sets of points.

## Prerequisites

**Required Modules:**
- `os`
- `functools`
- `glob`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test fit_matched_points: fitting two matching sets of points.'

```python
'Test fit_matched_points: fitting two matching sets of points.'
```

**Verification:**
```python
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation')
```

### Step 2: Assign tgt_pts = np.random.RandomState.uniform(...)

```python
tgt_pts = np.random.RandomState(42).uniform(size=(6, 3))
```

**Verification:**
```python
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation and translation.')
```

### Step 3: Assign trans = rotation(...)

```python
trans = rotation(2, 6, 3)
```

**Verification:**
```python
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation, translation and scaling.')
```

### Step 4: Assign src_pts = apply_trans(...)

```python
src_pts = apply_trans(trans, tgt_pts)
```

### Step 5: Assign trans_est = fit_matched_points(...)

```python
trans_est = fit_matched_points(src_pts, tgt_pts, translate=False, out='trans')
```

### Step 6: Assign est_pts = apply_trans(...)

```python
est_pts = apply_trans(trans_est, src_pts)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation')
```

### Step 8: Assign trans = np.dot(...)

```python
trans = np.dot(translation(2, -6, 3), rotation(2, 6, 3))
```

### Step 9: Assign src_pts = apply_trans(...)

```python
src_pts = apply_trans(trans, tgt_pts)
```

### Step 10: Assign trans_est = fit_matched_points(...)

```python
trans_est = fit_matched_points(src_pts, tgt_pts, out='trans')
```

### Step 11: Assign est_pts = apply_trans(...)

```python
est_pts = apply_trans(trans_est, src_pts)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation and translation.')
```

### Step 13: Assign trans = reduce(...)

```python
trans = reduce(np.dot, (translation(2, -6, 3), rotation(1.5, 0.3, 1.4), scaling(0.5, 0.5, 0.5)))
```

### Step 14: Assign src_pts = apply_trans(...)

```python
src_pts = apply_trans(trans, tgt_pts)
```

### Step 15: Assign trans_est = fit_matched_points(...)

```python
trans_est = fit_matched_points(src_pts, tgt_pts, scale=1, out='trans')
```

### Step 16: Assign est_pts = apply_trans(...)

```python
est_pts = apply_trans(trans_est, src_pts)
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation, translation and scaling.')
```

### Step 18: Call pytest.raises()

```python
pytest.raises(RuntimeError, fit_matched_points, tgt_pts, src_pts, tol=10)
```


## Complete Example

```python
# Workflow
'Test fit_matched_points: fitting two matching sets of points.'
tgt_pts = np.random.RandomState(42).uniform(size=(6, 3))
trans = rotation(2, 6, 3)
src_pts = apply_trans(trans, tgt_pts)
trans_est = fit_matched_points(src_pts, tgt_pts, translate=False, out='trans')
est_pts = apply_trans(trans_est, src_pts)
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation')
trans = np.dot(translation(2, -6, 3), rotation(2, 6, 3))
src_pts = apply_trans(trans, tgt_pts)
trans_est = fit_matched_points(src_pts, tgt_pts, out='trans')
est_pts = apply_trans(trans_est, src_pts)
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation and translation.')
trans = reduce(np.dot, (translation(2, -6, 3), rotation(1.5, 0.3, 1.4), scaling(0.5, 0.5, 0.5)))
src_pts = apply_trans(trans, tgt_pts)
trans_est = fit_matched_points(src_pts, tgt_pts, scale=1, out='trans')
est_pts = apply_trans(trans_est, src_pts)
assert_array_almost_equal(tgt_pts, est_pts, 2, 'fit_matched_points with rotation, translation and scaling.')
tgt_pts[0, :] += 20
pytest.raises(RuntimeError, fit_matched_points, tgt_pts, src_pts, tol=10)
```

## Next Steps


---

*Source: test_coreg.py:344 | Complexity: Advanced | Last updated: 2026-05-18*