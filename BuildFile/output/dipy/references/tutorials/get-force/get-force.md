# How To: Get Force

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get force

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign charges = np.array(...)

```python
charges = np.array([[1.0, 0, 0], [0, 1.0, 0], [0, 0, 1.0]])
```

### Step 2: Assign unknown = _get_forces(...)

```python
force, pot = _get_forces(charges)
```

### Step 3: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(force, 0)
```

### Step 4: Assign charges = np.array(...)

```python
charges = np.array([[1, -0.1, 0], [1, 0, 0]])
```

### Step 5: Assign unknown = _get_forces(...)

```python
force, pot = _get_forces(charges)
```

### Step 6: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(force[1, [0, 2]], 0)
```

### Step 7: Call nt.assert_()

```python
nt.assert_(force[1, 1] > 0)
```


## Complete Example

```python
# Workflow
charges = np.array([[1.0, 0, 0], [0, 1.0, 0], [0, 0, 1.0]])
force, pot = _get_forces(charges)
nt.assert_array_almost_equal(force, 0)
charges = np.array([[1, -0.1, 0], [1, 0, 0]])
force, pot = _get_forces(charges)
nt.assert_array_almost_equal(force[1, [0, 2]], 0)
nt.assert_(force[1, 1] > 0)
```

## Next Steps


---

*Source: test_sphere.py:294 | Complexity: Intermediate | Last updated: 2026-05-18*