# How To: Bundles Distances Mam

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bundles distances mam

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

### Step 1: Assign xyz1A = np.array(...)

```python
xyz1A = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]], dtype='float32')
```

**Verification:**
```python
assert_true(len(w) == 1)
```

### Step 2: Assign xyz2A = np.array(...)

```python
xyz2A = np.array([[0, 1, 1], [1, 0, 1], [2, 3, -2]], dtype='float32')
```

**Verification:**
```python
assert_true(issubclass(w[0].category, UserWarning))
```

### Step 3: Assign xyz1B = np.array(...)

```python
xyz1B = np.array([[-1, 0, 0], [2, 0, 0], [2, 3, 0], [3, 0, 0]], dtype='float32')
```

**Verification:**
```python
assert_true('not have the same number of points' in str(w[0].message))
```

### Step 4: Assign tracksA = value

```python
tracksA = [xyz1A, xyz2A]
```

### Step 5: Assign tracksB = value

```python
tracksB = [xyz1B, xyz1A, xyz2A]
```

### Step 6: Call pf.bundles_distances_mam()

```python
pf.bundles_distances_mam(tracksA, tracksB, metric=metric)
```

### Step 7: Call warnings.simplefilter()

```python
warnings.simplefilter('always', category=UserWarning)
```

### Step 8: Assign tracksC = value

```python
tracksC = [xyz2A, xyz1A]
```

### Step 9: Assign _ = pf.bundles_distances_mam(...)

```python
_ = pf.bundles_distances_mam(tracksA, tracksC)
```

### Step 10: Call print()

```python
print(w)
```

### Step 11: Call assert_true()

```python
assert_true(len(w) == 1)
```

### Step 12: Call assert_true()

```python
assert_true(issubclass(w[0].category, UserWarning))
```

### Step 13: Call assert_true()

```python
assert_true('not have the same number of points' in str(w[0].message))
```


## Complete Example

```python
# Workflow
xyz1A = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]], dtype='float32')
xyz2A = np.array([[0, 1, 1], [1, 0, 1], [2, 3, -2]], dtype='float32')
xyz1B = np.array([[-1, 0, 0], [2, 0, 0], [2, 3, 0], [3, 0, 0]], dtype='float32')
tracksA = [xyz1A, xyz2A]
tracksB = [xyz1B, xyz1A, xyz2A]
for metric in ('avg', 'min', 'max'):
    pf.bundles_distances_mam(tracksA, tracksB, metric=metric)
with warnings.catch_warnings(record=True) as w:
    warnings.simplefilter('always', category=UserWarning)
    tracksC = [xyz2A, xyz1A]
    _ = pf.bundles_distances_mam(tracksA, tracksC)
    print(w)
    assert_true(len(w) == 1)
    assert_true(issubclass(w[0].category, UserWarning))
    assert_true('not have the same number of points' in str(w[0].message))
```

## Next Steps


---

*Source: test_distances.py:119 | Complexity: Advanced | Last updated: 2026-05-18*