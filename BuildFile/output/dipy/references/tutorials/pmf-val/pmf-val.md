# How To: Pmf Val

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test pmf val

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.pmf`
- `dipy.reconst`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign sphere = get_sphere(...)

```python
sphere = get_sphere(name='symmetric724')
```

### Step 2: Assign point = np.array(...)

```python
point = np.array([1, 1, 1], dtype='float')
```

### Step 3: Assign out = np.ones(...)

```python
out = np.ones(len(sphere.vertices))
```

### Step 4: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 5: Assign pmfgen = SHCoeffPmfGen(...)

```python
pmfgen = SHCoeffPmfGen(rng.random([2, 2, 2, 28]), sphere, None)
```

### Step 6: Assign pmf = pmfgen.get_pmf(...)

```python
pmf = pmfgen.get_pmf(point)
```

### Step 7: Assign pmf_2 = pmfgen.get_pmf(...)

```python
pmf_2 = pmfgen.get_pmf(point, out)
```

### Step 8: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(pmf, out)
```

### Step 9: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(pmf, pmf_2)
```

### Step 10: Assign xyz = value

```python
xyz = sphere.vertices[idx] + rng.random([3]) / 100
```

### Step 11: Assign pmf_idx = pmfgen.get_pmf_value(...)

```python
pmf_idx = pmfgen.get_pmf_value(point, xyz)
```

### Step 12: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(pmf[idx], pmf_idx)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
sphere = get_sphere(name='symmetric724')
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    pmfgen = SHCoeffPmfGen(rng.random([2, 2, 2, 28]), sphere, None)
point = np.array([1, 1, 1], dtype='float')
out = np.ones(len(sphere.vertices))
for idx in [0, 5, 15, -1]:
    pmf = pmfgen.get_pmf(point)
    pmf_2 = pmfgen.get_pmf(point, out)
    npt.assert_array_almost_equal(pmf, out)
    npt.assert_array_almost_equal(pmf, pmf_2)
    xyz = sphere.vertices[idx] + rng.random([3]) / 100
    pmf_idx = pmfgen.get_pmf_value(point, xyz)
    npt.assert_array_almost_equal(pmf[idx], pmf_idx)
```

## Next Steps


---

*Source: test_pmf.py:16 | Complexity: Advanced | Last updated: 2026-05-18*