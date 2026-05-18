# How To: Patch2Self Boundary

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test patch2self boundary

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
S0 = 100 + np.zeros((20, 20, 20, 20))
```

**Verification:**
```python
assert_greater(S0[9, 9, 9, 9], 290)
```

### Step 2: Assign noise = value

```python
noise = 2 * rng.standard_normal((20, 20, 20, 20))
```

**Verification:**
```python
assert_less(S0[10, 10, 10, 10], 110)
```

### Step 3: Assign unknown = value

```python
S0[:10, :10, :10, :10] = 300 + noise[:10, :10, :10, :10]
```

### Step 4: Assign bvals = np.repeat(...)

```python
bvals = np.repeat(100, 20)
```

### Step 5: Assign extra_args = value

```python
extra_args = {'patch_radius': (0, 0, 0)} if version == 1 else {}
```

### Step 6: Call p2s.patch2self()

```python
p2s.patch2self(S0, bvals, **extra_args)
```

### Step 7: Call assert_greater()

```python
assert_greater(S0[9, 9, 9, 9], 290)
```

### Step 8: Call assert_less()

```python
assert_less(S0[10, 10, 10, 10], 110)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = 100 + np.zeros((20, 20, 20, 20))
noise = 2 * rng.standard_normal((20, 20, 20, 20))
S0 += noise
S0[:10, :10, :10, :10] = 300 + noise[:10, :10, :10, :10]
bvals = np.repeat(100, 20)
for version in [1, 3]:
    extra_args = {'patch_radius': (0, 0, 0)} if version == 1 else {}
    p2s.patch2self(S0, bvals, **extra_args)
    assert_greater(S0[9, 9, 9, 9], 290)
    assert_less(S0[10, 10, 10, 10], 110)
```

## Next Steps


---

*Source: test_patch2self.py:99 | Complexity: Advanced | Last updated: 2026-05-18*