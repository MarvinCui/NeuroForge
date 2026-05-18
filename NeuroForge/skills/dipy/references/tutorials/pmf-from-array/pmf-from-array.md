# How To: Pmf From Array

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test pmf from array

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

### Step 2: Assign pmfgen = SimplePmfGen(...)

```python
pmfgen = SimplePmfGen(np.ones([2, 2, 2, len(sphere.vertices)]), sphere)
```

### Step 3: Assign out = np.zeros(...)

```python
out = np.zeros(len(sphere.vertices))
```

### Step 4: Assign pmf = pmfgen.get_pmf(...)

```python
pmf = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'))
```

### Step 5: Assign out = pmfgen.get_pmf(...)

```python
out = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'), out)
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(np.sum(pmf) > 0, True)
```

### Step 7: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(pmf, out)
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pmfgen.get_pmf(np.array([-1, 0, 0], dtype=float)), np.zeros(len(sphere.vertices)))
```

### Step 9: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pmfgen.get_pmf(np.array([0, 0, 10], dtype=float)), np.zeros(len(sphere.vertices)))
```

### Step 10: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, lambda: SimplePmfGen(np.ones([2, 2, 2, len(sphere.vertices)]), default_sphere))
```


## Complete Example

```python
# Workflow
sphere = HemiSphere.from_sphere(unit_octahedron)
pmfgen = SimplePmfGen(np.ones([2, 2, 2, len(sphere.vertices)]), sphere)
out = np.zeros(len(sphere.vertices))
pmf = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'))
out = pmfgen.get_pmf(np.array([0, 0, 0], dtype='float'), out)
npt.assert_equal(np.sum(pmf) > 0, True)
npt.assert_array_almost_equal(pmf, out)
npt.assert_array_equal(pmfgen.get_pmf(np.array([-1, 0, 0], dtype=float)), np.zeros(len(sphere.vertices)))
npt.assert_array_equal(pmfgen.get_pmf(np.array([0, 0, 10], dtype=float)), np.zeros(len(sphere.vertices)))
npt.assert_raises(ValueError, lambda: SimplePmfGen(np.ones([2, 2, 2, len(sphere.vertices)]), default_sphere))
```

## Next Steps


---

*Source: test_pmf.py:69 | Complexity: Advanced | Last updated: 2026-05-18*