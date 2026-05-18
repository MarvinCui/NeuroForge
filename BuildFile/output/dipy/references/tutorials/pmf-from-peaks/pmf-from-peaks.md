# How To: Pmf From Peaks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test pmf from peaks

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

### Step 2: Assign n_vertices = len(...)

```python
n_vertices = len(sphere.vertices)
```

### Step 3: Assign peak_indices = np.full(...)

```python
peak_indices = np.full((2, 2, 2, 2), -1.0, dtype=float)
```

### Step 4: Assign peak_values = np.zeros(...)

```python
peak_values = np.zeros((2, 2, 2, 2), dtype=float)
```

### Step 5: Assign pmfgen = SimplePeakGen(...)

```python
pmfgen = SimplePeakGen(peak_indices, peak_values, sphere.vertices, sphere)
```

### Step 6: Assign point = np.array(...)

```python
point = np.array([0.5, 0.5, 0.5], dtype=float)
```

### Step 7: Assign pmf = pmfgen.get_pmf(...)

```python
pmf = pmfgen.get_pmf(point)
```

### Step 8: Call npt.assert_allclose()

```python
npt.assert_allclose(pmf[0], 2.5)
```

### Step 9: Call npt.assert_allclose()

```python
npt.assert_allclose(pmf[1], 2.0)
```

### Step 10: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pmf[2:], np.zeros(n_vertices - 2))
```

### Step 11: Assign pmf_value_0 = pmfgen.get_pmf_value(...)

```python
pmf_value_0 = pmfgen.get_pmf_value(point, sphere.vertices[0])
```

### Step 12: Assign pmf_value_1 = pmfgen.get_pmf_value(...)

```python
pmf_value_1 = pmfgen.get_pmf_value(point, sphere.vertices[1])
```

### Step 13: Assign pmf_value_2 = pmfgen.get_pmf_value(...)

```python
pmf_value_2 = pmfgen.get_pmf_value(point, sphere.vertices[2])
```

### Step 14: Call npt.assert_allclose()

```python
npt.assert_allclose(pmf_value_0, 2.5)
```

### Step 15: Call npt.assert_allclose()

```python
npt.assert_allclose(pmf_value_1, 2.0)
```

### Step 16: Call npt.assert_allclose()

```python
npt.assert_allclose(pmf_value_2, 0.0)
```

### Step 17: Assign unknown = 0

```python
peak_indices[x, y, z, 0] = 0
```

### Step 18: Assign unknown = value

```python
peak_values[x, y, z, 0] = x + y + z + 1
```

### Step 19: Assign unknown = 1

```python
peak_indices[x, y, z, 1] = 1
```

### Step 20: Assign unknown = 2.0

```python
peak_values[x, y, z, 1] = 2.0
```


## Complete Example

```python
# Workflow
sphere = HemiSphere.from_sphere(unit_octahedron)
n_vertices = len(sphere.vertices)
peak_indices = np.full((2, 2, 2, 2), -1.0, dtype=float)
peak_values = np.zeros((2, 2, 2, 2), dtype=float)
for x in range(2):
    for y in range(2):
        for z in range(2):
            peak_indices[x, y, z, 0] = 0
            peak_values[x, y, z, 0] = x + y + z + 1
            peak_indices[x, y, z, 1] = 1
            peak_values[x, y, z, 1] = 2.0
pmfgen = SimplePeakGen(peak_indices, peak_values, sphere.vertices, sphere)
point = np.array([0.5, 0.5, 0.5], dtype=float)
pmf = pmfgen.get_pmf(point)
npt.assert_allclose(pmf[0], 2.5)
npt.assert_allclose(pmf[1], 2.0)
npt.assert_array_equal(pmf[2:], np.zeros(n_vertices - 2))
pmf_value_0 = pmfgen.get_pmf_value(point, sphere.vertices[0])
pmf_value_1 = pmfgen.get_pmf_value(point, sphere.vertices[1])
pmf_value_2 = pmfgen.get_pmf_value(point, sphere.vertices[2])
npt.assert_allclose(pmf_value_0, 2.5)
npt.assert_allclose(pmf_value_1, 2.0)
npt.assert_allclose(pmf_value_2, 0.0)
```

## Next Steps


---

*Source: test_pmf.py:97 | Complexity: Advanced | Last updated: 2026-05-18*