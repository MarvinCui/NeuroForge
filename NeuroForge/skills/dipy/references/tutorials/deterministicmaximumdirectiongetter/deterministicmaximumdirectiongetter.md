# How To: Deterministicmaximumdirectiongetter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test DeterministicMaximumDirectionGetter

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.direction`
- `dipy.reconst.shm`


## Step-by-Step Guide

### Step 1: Assign direction = unknown.copy(...)

```python
direction = unit_octahedron.vertices[-1].copy()
```

### Step 2: Assign point = np.zeros(...)

```python
point = np.zeros(3)
```

### Step 3: Assign N = value

```python
N = unit_octahedron.theta.shape[0]
```

### Step 4: Assign pmf = np.zeros(...)

```python
pmf = np.zeros((3, 3, 3, N))
```

### Step 5: Assign dg = DeterministicMaximumDirectionGetter.from_pmf(...)

```python
dg = DeterministicMaximumDirectionGetter.from_pmf(pmf, 90, unit_octahedron)
```

### Step 6: Assign state = dg.get_direction(...)

```python
state = dg.get_direction(point, direction)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(state, 1)
```

### Step 8: Assign pmf = np.zeros(...)

```python
pmf = np.zeros((3, 3, 3, N))
```

### Step 9: Assign unknown = 1

```python
pmf[0, 0, 0, 0] = 1
```

### Step 10: Assign dg = DeterministicMaximumDirectionGetter.from_pmf(...)

```python
dg = DeterministicMaximumDirectionGetter.from_pmf(pmf, 0, unit_octahedron)
```

### Step 11: Assign state = dg.get_direction(...)

```python
state = dg.get_direction(point, direction)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(state, 1)
```


## Complete Example

```python
# Workflow
direction = unit_octahedron.vertices[-1].copy()
point = np.zeros(3)
N = unit_octahedron.theta.shape[0]
pmf = np.zeros((3, 3, 3, N))
dg = DeterministicMaximumDirectionGetter.from_pmf(pmf, 90, unit_octahedron)
state = dg.get_direction(point, direction)
npt.assert_equal(state, 1)
pmf = np.zeros((3, 3, 3, N))
pmf[0, 0, 0, 0] = 1
dg = DeterministicMaximumDirectionGetter.from_pmf(pmf, 0, unit_octahedron)
state = dg.get_direction(point, direction)
npt.assert_equal(state, 1)
```

## Next Steps


---

*Source: test_prob_direction_getter.py:117 | Complexity: Advanced | Last updated: 2026-05-18*