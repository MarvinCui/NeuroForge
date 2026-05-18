# How To: Obliquity

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check the calculation of inclination of an affine axes.

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `pytest`
- `numpy.testing`
- `affines`
- `eulerangles`
- `orientations`
- `math`


## Step-by-Step Guide

### Step 1: 'Check the calculation of inclination of an affine axes.'

```python
'Check the calculation of inclination of an affine axes.'
```

**Verification:**
```python
assert_almost_equal(obliquity(aligned), [0.0, 0.0, 0.0])
```

### Step 2: Assign aligned = np.diag(...)

```python
aligned = np.diag([2.0, 2.0, 2.3, 1.0])
```

**Verification:**
```python
assert_almost_equal(obliquity(oblique) * 180 / pi, [0.0810285, 5.1569949, 5.1569376])
```

### Step 3: Assign unknown = value

```python
aligned[:-1, -1] = [-10, -10, -7]
```

### Step 4: Assign R = from_matvec(...)

```python
R = from_matvec(euler2mat(x=0.09, y=0.001, z=0.001), [0.0, 0.0, 0.0])
```

### Step 5: Assign oblique = R.dot(...)

```python
oblique = R.dot(aligned)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(obliquity(aligned), [0.0, 0.0, 0.0])
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(obliquity(oblique) * 180 / pi, [0.0810285, 5.1569949, 5.1569376])
```


## Complete Example

```python
# Workflow
'Check the calculation of inclination of an affine axes.'
from math import pi
aligned = np.diag([2.0, 2.0, 2.3, 1.0])
aligned[:-1, -1] = [-10, -10, -7]
R = from_matvec(euler2mat(x=0.09, y=0.001, z=0.001), [0.0, 0.0, 0.0])
oblique = R.dot(aligned)
assert_almost_equal(obliquity(aligned), [0.0, 0.0, 0.0])
assert_almost_equal(obliquity(oblique) * 180 / pi, [0.0810285, 5.1569949, 5.1569376])
```

## Next Steps


---

*Source: test_affines.py:211 | Complexity: Intermediate | Last updated: 2026-05-18*