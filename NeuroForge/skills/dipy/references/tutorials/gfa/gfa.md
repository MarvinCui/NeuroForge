# How To: Gfa

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gfa

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.reconst.odf`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign g = gfa(...)

```python
g = gfa(np.ones(100))
```

**Verification:**
```python
assert_equal(g, 0)
```

### Step 2: Call assert_equal()

```python
assert_equal(g, 0)
```

**Verification:**
```python
assert_equal(g, np.array([0, 0]))
```

### Step 3: Assign g = gfa(...)

```python
g = gfa(np.ones((2, 100)))
```

**Verification:**
```python
assert_almost_equal(g, np.sqrt(9.0 / 81))
```

### Step 4: Call assert_equal()

```python
assert_equal(g, np.array([0, 0]))
```

**Verification:**
```python
assert_almost_equal(g, np.sqrt(99.0 / 99.0 ** 2))
```

### Step 5: Assign g = gfa(...)

```python
g = gfa(np.hstack([np.ones(9), [0]]))
```

**Verification:**
```python
assert_(np.isnan(g))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(g, np.sqrt(9.0 / 81))
```

### Step 7: Assign g = gfa(...)

```python
g = gfa(np.hstack([np.ones(99), [0]]))
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(g, np.sqrt(99.0 / 99.0 ** 2))
```

### Step 9: Assign g = gfa(...)

```python
g = gfa(np.zeros(10))
```

### Step 10: Call assert_()

```python
assert_(np.isnan(g))
```


## Complete Example

```python
# Workflow
g = gfa(np.ones(100))
assert_equal(g, 0)
g = gfa(np.ones((2, 100)))
assert_equal(g, np.array([0, 0]))
g = gfa(np.hstack([np.ones(9), [0]]))
assert_almost_equal(g, np.sqrt(9.0 / 81))
g = gfa(np.hstack([np.ones(99), [0]]))
assert_almost_equal(g, np.sqrt(99.0 / 99.0 ** 2))
g = gfa(np.zeros(10))
assert_(np.isnan(g))
```

## Next Steps


---

*Source: test_odf.py:69 | Complexity: Advanced | Last updated: 2026-05-18*