# How To: Pmf From Sh

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test pmf from sh

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.pmf`
- `dipy.reconst`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign sphere = HemiSphere.from_sphere(...)

```python
sphere = HemiSphere.from_sphere(unit_octahedron)
```

### Step 2: Assign out = np.zeros(...)

```python
out = np.zeros(len(sphere.vertices))
```

### Step 3: Assign pmf = pmfgen.get_pmf(...)

```python
pmf = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'))
```

### Step 4: Assign out = pmfgen.get_pmf(...)

```python
out = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'), out)
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(np.sum(pmf) > 0, True)
```

### Step 6: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(pmf, out)
```

### Step 7: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pmfgen.get_pmf(np.array([-1, 0, 0], dtype='float')), np.zeros(len(sphere.vertices)))
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pmfgen.get_pmf(np.array([0, 0, 10], dtype='float')), np.zeros(len(sphere.vertices)))
```

### Step 9: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 10: Assign pmfgen = SHCoeffPmfGen(...)

```python
pmfgen = SHCoeffPmfGen(np.ones([2, 2, 2, 28]), sphere, None)
```


## Complete Example

```python
# Workflow
sphere = HemiSphere.from_sphere(unit_octahedron)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    pmfgen = SHCoeffPmfGen(np.ones([2, 2, 2, 28]), sphere, None)
out = np.zeros(len(sphere.vertices))
pmf = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'))
out = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'), out)
npt.assert_equal(np.sum(pmf) > 0, True)
npt.assert_array_almost_equal(pmf, out)
npt.assert_array_equal(pmfgen.get_pmf(np.array([-1, 0, 0], dtype='float')), np.zeros(len(sphere.vertices)))
npt.assert_array_equal(pmfgen.get_pmf(np.array([0, 0, 10], dtype='float')), np.zeros(len(sphere.vertices)))
```

## Next Steps


---

*Source: test_pmf.py:41 | Complexity: Advanced | Last updated: 2026-05-18*