# How To: Apply Post Processing Shift Intensity No Op When Baselines Match

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test apply post processing shift intensity no op when baselines match

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.denoise`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `sklearn.dummy`


## Step-by-Step Guide

### Step 1: Assign data = np.full(...)

```python
data = np.full((2, 2, 2, 3), 5.0)
```

**Verification:**
```python
assert_allclose(out, denoised)
```

### Step 2: Assign denoised = data.copy(...)

```python
denoised = data.copy()
```

### Step 3: Assign out = p2s._apply_post_processing(...)

```python
out = p2s._apply_post_processing(data, denoised.copy(), shift_intensity=True, clip_negative_vals=False)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(out, denoised)
```


## Complete Example

```python
# Workflow
data = np.full((2, 2, 2, 3), 5.0)
denoised = data.copy()
out = p2s._apply_post_processing(data, denoised.copy(), shift_intensity=True, clip_negative_vals=False)
assert_allclose(out, denoised)
```

## Next Steps


---

*Source: test_patch2self.py:428 | Complexity: Intermediate | Last updated: 2026-05-18*