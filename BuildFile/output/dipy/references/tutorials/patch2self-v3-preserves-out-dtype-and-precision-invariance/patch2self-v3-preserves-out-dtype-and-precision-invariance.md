# How To: Patch2Self V3 Preserves Out Dtype And Precision Invariance

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test patch2self v3 preserves out dtype and precision invariance

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

### Step 1: Assign shape = value

```python
shape = (10, 10, 6, 13)
```

**Verification:**
```python
assert_equal(den32.dtype, np.float32)
```

### Step 2: Assign base = value

```python
base = 30.0 + 2.0 * rng.standard_normal(shape)
```

**Verification:**
```python
assert_equal(den64.dtype, np.float64)
```

### Step 3: Assign bvals = np.repeat(...)

```python
bvals = np.repeat(1000.0, shape[-1])
```

**Verification:**
```python
assert_allclose(m32, m64, rtol=0.02, atol=1.25)
```

### Step 4: Assign data32 = base.astype(...)

```python
data32 = base.astype(np.float32)
```

**Verification:**
```python
assert_allclose(s32, s64, rtol=0.1, atol=1.0)
```

### Step 5: Assign data64 = base.astype(...)

```python
data64 = base.astype(np.float64)
```

### Step 6: Assign den32 = p2s.patch2self(...)

```python
den32 = p2s.patch2self(data32, bvals, model='ridge', alpha=1.0, version=3)
```

### Step 7: Assign den64 = p2s.patch2self(...)

```python
den64 = p2s.patch2self(data64, bvals, model='ridge', alpha=1.0, version=3)
```

### Step 8: Call assert_equal()

```python
assert_equal(den32.dtype, np.float32)
```

### Step 9: Call assert_equal()

```python
assert_equal(den64.dtype, np.float64)
```

### Step 10: Assign m32 = den32.reshape.mean(...)

```python
m32 = den32.reshape(-1, shape[-1]).mean(axis=0)
```

### Step 11: Assign m64 = den64.reshape.mean(...)

```python
m64 = den64.reshape(-1, shape[-1]).mean(axis=0)
```

### Step 12: Assign s32 = den32.reshape.std(...)

```python
s32 = den32.reshape(-1, shape[-1]).std(axis=0)
```

### Step 13: Assign s64 = den64.reshape.std(...)

```python
s64 = den64.reshape(-1, shape[-1]).std(axis=0)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(m32, m64, rtol=0.02, atol=1.25)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(s32, s64, rtol=0.1, atol=1.0)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
shape = (10, 10, 6, 13)
base = 30.0 + 2.0 * rng.standard_normal(shape)
bvals = np.repeat(1000.0, shape[-1])
data32 = base.astype(np.float32)
data64 = base.astype(np.float64)
den32 = p2s.patch2self(data32, bvals, model='ridge', alpha=1.0, version=3)
den64 = p2s.patch2self(data64, bvals, model='ridge', alpha=1.0, version=3)
assert_equal(den32.dtype, np.float32)
assert_equal(den64.dtype, np.float64)
m32 = den32.reshape(-1, shape[-1]).mean(axis=0)
m64 = den64.reshape(-1, shape[-1]).mean(axis=0)
s32 = den32.reshape(-1, shape[-1]).std(axis=0)
s64 = den64.reshape(-1, shape[-1]).std(axis=0)
assert_allclose(m32, m64, rtol=0.02, atol=1.25)
assert_allclose(s32, s64, rtol=0.1, atol=1.0)
```

## Next Steps


---

*Source: test_patch2self.py:335 | Complexity: Advanced | Last updated: 2026-05-18*