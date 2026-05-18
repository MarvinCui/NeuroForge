# How To: Pmf From Peaks Invalid Point

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test pmf from peaks invalid point

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

### Step 2: Assign peak_indices = np.zeros(...)

```python
peak_indices = np.zeros((2, 2, 2, 1), dtype=float)
```

### Step 3: Assign peak_values = np.ones(...)

```python
peak_values = np.ones((2, 2, 2, 1), dtype=float)
```

### Step 4: Assign pmfgen = SimplePeakGen(...)

```python
pmfgen = SimplePeakGen(peak_indices, peak_values, sphere.vertices, sphere)
```

### Step 5: Assign invalid_point = np.array(...)

```python
invalid_point = np.array([-0.1, 0.5, 0.5], dtype=float)
```

### Step 6: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pmfgen.get_pmf(invalid_point), np.zeros(len(sphere.vertices)))
```

### Step 7: Call npt.assert_allclose()

```python
npt.assert_allclose(pmfgen.get_pmf_value(invalid_point, sphere.vertices[0]), 0.0)
```


## Complete Example

```python
# Workflow
sphere = HemiSphere.from_sphere(unit_octahedron)
peak_indices = np.zeros((2, 2, 2, 1), dtype=float)
peak_values = np.ones((2, 2, 2, 1), dtype=float)
pmfgen = SimplePeakGen(peak_indices, peak_values, sphere.vertices, sphere)
invalid_point = np.array([-0.1, 0.5, 0.5], dtype=float)
npt.assert_array_equal(pmfgen.get_pmf(invalid_point), np.zeros(len(sphere.vertices)))
npt.assert_allclose(pmfgen.get_pmf_value(invalid_point, sphere.vertices[0]), 0.0)
```

## Next Steps


---

*Source: test_pmf.py:128 | Complexity: Intermediate | Last updated: 2026-05-18*