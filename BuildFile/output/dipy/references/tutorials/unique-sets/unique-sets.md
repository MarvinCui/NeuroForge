# How To: Unique Sets

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test unique sets

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

### Step 1: Assign sets = np.array(...)

```python
sets = np.array([[0, 1, 2], [1, 2, 0], [0, 2, 1], [1, 2, 3]])
```

### Step 2: Assign e = array_to_set(...)

```python
e = array_to_set([[0, 1, 2], [1, 2, 3]])
```

### Step 3: Assign u = unique_sets(...)

```python
u = unique_sets(sets)
```

### Step 4: Call nt.assert_equal()

```python
nt.assert_equal(len(u), len(e))
```

### Step 5: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(u), e)
```

### Step 6: Assign unknown = unique_sets(...)

```python
u, m = unique_sets(sets, return_inverse=True)
```

### Step 7: Call nt.assert_equal()

```python
nt.assert_equal(len(u), len(e))
```

### Step 8: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(u), e)
```

### Step 9: Call nt.assert_equal()

```python
nt.assert_equal(np.sort(u[m], -1), np.sort(sets, -1))
```


## Complete Example

```python
# Workflow
sets = np.array([[0, 1, 2], [1, 2, 0], [0, 2, 1], [1, 2, 3]])
e = array_to_set([[0, 1, 2], [1, 2, 3]])
u = unique_sets(sets)
nt.assert_equal(len(u), len(e))
nt.assert_equal(array_to_set(u), e)
u, m = unique_sets(sets, return_inverse=True)
nt.assert_equal(len(u), len(e))
nt.assert_equal(array_to_set(u), e)
nt.assert_equal(np.sort(u[m], -1), np.sort(sets, -1))
```

## Next Steps


---

*Source: test_sphere.py:91 | Complexity: Advanced | Last updated: 2026-05-18*