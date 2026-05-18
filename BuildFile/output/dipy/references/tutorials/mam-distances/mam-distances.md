# How To: Mam Distances

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mam distances

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking.streamline`
- `time`


## Step-by-Step Guide

### Step 1: Assign xyz1 = np.array(...)

```python
xyz1 = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]])
```

**Verification:**
```python
assert_almost_equal(zd2[0], 1.76135602742)
```

### Step 2: Assign xyz2 = np.array(...)

```python
xyz2 = np.array([[0, 1, 1], [1, 0, 1], [2, 3, -2]])
```

### Step 3: Assign xyz1 = xyz1.astype(...)

```python
xyz1 = xyz1.astype('float32')
```

### Step 4: Assign xyz2 = xyz2.astype(...)

```python
xyz2 = xyz2.astype('float32')
```

### Step 5: Assign zd2 = pf.mam_distances(...)

```python
zd2 = pf.mam_distances(xyz1, xyz2)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(zd2[0], 1.76135602742)
```


## Complete Example

```python
# Workflow
xyz1 = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]])
xyz2 = np.array([[0, 1, 1], [1, 0, 1], [2, 3, -2]])
xyz1 = xyz1.astype('float32')
xyz2 = xyz2.astype('float32')
zd2 = pf.mam_distances(xyz1, xyz2)
assert_almost_equal(zd2[0], 1.76135602742)
```

## Next Steps


---

*Source: test_distances.py:199 | Complexity: Intermediate | Last updated: 2026-05-18*