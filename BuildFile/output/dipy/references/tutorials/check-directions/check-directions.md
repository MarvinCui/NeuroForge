# How To: Check Directions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check directions

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.sims.voxel`
- `dipy.testing.decorators`
- `dipy.reconst.dti`


## Step-by-Step Guide

### Step 1: Assign angles = value

```python
angles = [(0, 0)]
```

**Verification:**
```python
assert_array_almost_equal(sticks, [[0, 0, 1]])
```

### Step 2: Assign sticks = _check_directions(...)

```python
sticks = _check_directions(angles)
```

**Verification:**
```python
assert_array_almost_equal(sticks, [[0, 0, 1]])
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sticks, [[0, 0, 1]])
```

**Verification:**
```python
assert_array_almost_equal(sticks, [[1, 0, 0]])
```

### Step 4: Assign angles = value

```python
angles = [(0, 90)]
```

**Verification:**
```python
assert_array_almost_equal(sticks, [[0, 0, 1]])
```

### Step 5: Assign sticks = _check_directions(...)

```python
sticks = _check_directions(angles)
```

**Verification:**
```python
assert_array_almost_equal(sticks, [[1, 0, 0], ref_vec])
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sticks, [[0, 0, 1]])
```

**Verification:**
```python
assert_array_almost_equal(sticks, [ref_vec1, ref_vec2])
```

### Step 7: Assign angles = value

```python
angles = [(90, 0)]
```

### Step 8: Assign sticks = _check_directions(...)

```python
sticks = _check_directions(angles)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sticks, [[1, 0, 0]])
```

### Step 10: Assign angles = value

```python
angles = [(0, 0, 1)]
```

### Step 11: Assign sticks = _check_directions(...)

```python
sticks = _check_directions(angles)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sticks, [[0, 0, 1]])
```

### Step 13: Assign angles = np.array(...)

```python
angles = np.array([[90, 0], [30, 0]])
```

### Step 14: Assign sticks = _check_directions(...)

```python
sticks = _check_directions(angles)
```

### Step 15: Assign ref_vec = value

```python
ref_vec = [np.sin(np.pi * 30 / 180), 0, np.cos(np.pi * 30 / 180)]
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sticks, [[1, 0, 0], ref_vec])
```

### Step 17: Assign the1 = 0

```python
the1 = 0
```

### Step 18: Assign phi1 = 90

```python
phi1 = 90
```

### Step 19: Assign the2 = 30

```python
the2 = 30
```

### Step 20: Assign phi2 = 45

```python
phi2 = 45
```

### Step 21: Assign angles = np.array(...)

```python
angles = np.array([(the1, phi1), (the2, phi2)])
```

### Step 22: Assign sticks = _check_directions(...)

```python
sticks = _check_directions(angles)
```

### Step 23: Assign ref_vec1 = value

```python
ref_vec1 = (np.sin(np.pi * the1 / 180) * np.cos(np.pi * phi1 / 180), np.sin(np.pi * the1 / 180) * np.sin(np.pi * phi1 / 180), np.cos(np.pi * the1 / 180))
```

### Step 24: Assign ref_vec2 = value

```python
ref_vec2 = (np.sin(np.pi * the2 / 180) * np.cos(np.pi * phi2 / 180), np.sin(np.pi * the2 / 180) * np.sin(np.pi * phi2 / 180), np.cos(np.pi * the2 / 180))
```

### Step 25: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sticks, [ref_vec1, ref_vec2])
```


## Complete Example

```python
# Workflow
angles = [(0, 0)]
sticks = _check_directions(angles)
assert_array_almost_equal(sticks, [[0, 0, 1]])
angles = [(0, 90)]
sticks = _check_directions(angles)
assert_array_almost_equal(sticks, [[0, 0, 1]])
angles = [(90, 0)]
sticks = _check_directions(angles)
assert_array_almost_equal(sticks, [[1, 0, 0]])
angles = [(0, 0, 1)]
sticks = _check_directions(angles)
assert_array_almost_equal(sticks, [[0, 0, 1]])
angles = np.array([[90, 0], [30, 0]])
sticks = _check_directions(angles)
ref_vec = [np.sin(np.pi * 30 / 180), 0, np.cos(np.pi * 30 / 180)]
assert_array_almost_equal(sticks, [[1, 0, 0], ref_vec])
the1 = 0
phi1 = 90
the2 = 30
phi2 = 45
angles = np.array([(the1, phi1), (the2, phi2)])
sticks = _check_directions(angles)
ref_vec1 = (np.sin(np.pi * the1 / 180) * np.cos(np.pi * phi1 / 180), np.sin(np.pi * the1 / 180) * np.sin(np.pi * phi1 / 180), np.cos(np.pi * the1 / 180))
ref_vec2 = (np.sin(np.pi * the2 / 180) * np.cos(np.pi * phi2 / 180), np.sin(np.pi * the2 / 180) * np.sin(np.pi * phi2 / 180), np.cos(np.pi * the2 / 180))
assert_array_almost_equal(sticks, [ref_vec1, ref_vec2])
```

## Next Steps


---

*Source: test_voxel.py:59 | Complexity: Advanced | Last updated: 2026-05-18*