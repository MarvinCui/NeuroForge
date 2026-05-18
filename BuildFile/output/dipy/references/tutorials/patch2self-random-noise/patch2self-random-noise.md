# How To: Patch2Self Random Noise

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test patch2self random noise

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign S0 = value

```python
S0 = 30 + 2 * rng.standard_normal((20, 20, 20, 50))
```

**Verification:**
```python
assert_greater_equal(S0den_shift.min(), S0.min())
```

### Step 2: Assign bvals = np.repeat(...)

```python
bvals = np.repeat(30, 50)
```

**Verification:**
```python
assert_less_equal(np.round(S0den_shift.mean()), 30)
```

### Step 3: Assign extra_args = value

```python
extra_args = {'patch_radius': (0, 0, 0)} if version == 1 else {}
```

**Verification:**
```python
assert_greater(S0den_clip.min(), S0.min())
```

### Step 4: Assign S0den_shift = p2s.patch2self(...)

```python
S0den_shift = p2s.patch2self(S0, bvals, model='ols', shift_intensity=True, version=version, **extra_args)
```

**Verification:**
```python
assert_equal(np.round(S0den_clip.mean()), 30)
```

### Step 5: Call assert_greater_equal()

```python
assert_greater_equal(S0den_shift.min(), S0.min())
```

**Verification:**
```python
assert_greater(S0den_clip.min(), S0.min())
```

### Step 6: Call assert_less_equal()

```python
assert_less_equal(np.round(S0den_shift.mean()), 30)
```

**Verification:**
```python
assert_equal(np.round(S0den_clip.mean()), 30)
```

### Step 7: Assign msg = 'Both `clip_negative_vals` and `shift_intensity` .*'

```python
msg = 'Both `clip_negative_vals` and `shift_intensity` .*'
```

**Verification:**
```python
assert_greater(S0den_clip.min(), S0.min())
```

### Step 8: Call assert_greater()

```python
assert_greater(S0den_clip.min(), S0.min())
```

**Verification:**
```python
assert_equal(np.round(S0den_clip.mean()), 30)
```

### Step 9: Call assert_equal()

```python
assert_equal(np.round(S0den_clip.mean()), 30)
```

### Step 10: Call assert_greater()

```python
assert_greater(S0den_clip.min(), S0.min())
```

### Step 11: Call assert_equal()

```python
assert_equal(np.round(S0den_clip.mean()), 30)
```

### Step 12: Assign S0den_clip = p2s.patch2self(...)

```python
S0den_clip = p2s.patch2self(S0, bvals, model='ols', clip_negative_vals=False, shift_intensity=False, version=version, **extra_args)
```

### Step 13: Call assert_greater()

```python
assert_greater(S0den_clip.min(), S0.min())
```

### Step 14: Call assert_equal()

```python
assert_equal(np.round(S0den_clip.mean()), 30)
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=UserWarning)
```

### Step 16: Assign S0den_clip = p2s.patch2self(...)

```python
S0den_clip = p2s.patch2self(S0, bvals, model='ols', clip_negative_vals=True, version=version, **extra_args)
```

### Step 17: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=UserWarning)
```

### Step 18: Assign S0den_clip = p2s.patch2self(...)

```python
S0den_clip = p2s.patch2self(S0, bvals, model='ols', clip_negative_vals=True, shift_intensity=True, version=version, **extra_args)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = 30 + 2 * rng.standard_normal((20, 20, 20, 50))
bvals = np.repeat(30, 50)
for version in [1, 3]:
    extra_args = {'patch_radius': (0, 0, 0)} if version == 1 else {}
    S0den_shift = p2s.patch2self(S0, bvals, model='ols', shift_intensity=True, version=version, **extra_args)
    assert_greater_equal(S0den_shift.min(), S0.min())
    assert_less_equal(np.round(S0den_shift.mean()), 30)
    msg = 'Both `clip_negative_vals` and `shift_intensity` .*'
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', message=msg, category=UserWarning)
        S0den_clip = p2s.patch2self(S0, bvals, model='ols', clip_negative_vals=True, version=version, **extra_args)
    assert_greater(S0den_clip.min(), S0.min())
    assert_equal(np.round(S0den_clip.mean()), 30)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', message=msg, category=UserWarning)
        S0den_clip = p2s.patch2self(S0, bvals, model='ols', clip_negative_vals=True, shift_intensity=True, version=version, **extra_args)
    assert_greater(S0den_clip.min(), S0.min())
    assert_equal(np.round(S0den_clip.mean()), 30)
    S0den_clip = p2s.patch2self(S0, bvals, model='ols', clip_negative_vals=False, shift_intensity=False, version=version, **extra_args)
    assert_greater(S0den_clip.min(), S0.min())
    assert_equal(np.round(S0den_clip.mean()), 30)
```

## Next Steps


---

*Source: test_patch2self.py:30 | Complexity: Advanced | Last updated: 2026-05-18*