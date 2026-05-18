# How To: Viewer Nonras

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test viewer nonRAS

## Prerequisites

**Required Modules:**
- `unittest`
- `collections`
- `numpy`
- `pytest`
- `numpy.testing`
- `optpkg`
- `viewers`


## Step-by-Step Guide

### Step 1: Assign data1 = np.random.rand(...)

```python
data1 = np.random.rand(10, 20, 40)
```

**Verification:**
```python
assert_array_equal(sag, data1[5, :, :])
```

### Step 2: Assign unknown = 0

```python
data1[5, 10, :] = 0
```

**Verification:**
```python
assert_array_equal(cor, data1[:, :, 30].T)
```

### Step 3: Assign unknown = 0

```python
data1[5, :, 30] = 0
```

**Verification:**
```python
assert_array_equal(axi, data1[:, 10, :].T)
```

### Step 4: Assign unknown = 0

```python
data1[:, 10, 30] = 0
```

**Verification:**
```python
assert_array_equal(sag, data1[6, :, :])
```

### Step 5: Assign aff1 = np.array(...)

```python
aff1 = np.array([[1, 0, 0, -5], [0, 0, 1, -30], [0, 1, 0, -10], [0, 0, 0, 1]])
```

**Verification:**
```python
assert_array_equal(cor, data1[:, :, 32].T)
```

### Step 6: Assign o1 = OrthoSlicer3D(...)

```python
o1 = OrthoSlicer3D(data1, aff1)
```

**Verification:**
```python
assert_array_equal(axi, data1[:, 13, :].T)
```

### Step 7: Assign sag = unknown.get_array(...)

```python
sag = o1._ims[0].get_array()
```

### Step 8: Assign cor = unknown.get_array(...)

```python
cor = o1._ims[1].get_array()
```

### Step 9: Assign axi = unknown.get_array(...)

```python
axi = o1._ims[2].get_array()
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(sag, data1[5, :, :])
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(cor, data1[:, :, 30].T)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(axi, data1[:, 10, :].T)
```

### Step 13: Call o1.set_position()

```python
o1.set_position(1, 2, 3)
```

### Step 14: Assign sag = unknown.get_array(...)

```python
sag = o1._ims[0].get_array()
```

### Step 15: Assign cor = unknown.get_array(...)

```python
cor = o1._ims[1].get_array()
```

### Step 16: Assign axi = unknown.get_array(...)

```python
axi = o1._ims[2].get_array()
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(sag, data1[6, :, :])
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(cor, data1[:, :, 32].T)
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(axi, data1[:, 13, :].T)
```


## Complete Example

```python
# Workflow
data1 = np.random.rand(10, 20, 40)
data1[5, 10, :] = 0
data1[5, :, 30] = 0
data1[:, 10, 30] = 0
aff1 = np.array([[1, 0, 0, -5], [0, 0, 1, -30], [0, 1, 0, -10], [0, 0, 0, 1]])
o1 = OrthoSlicer3D(data1, aff1)
sag = o1._ims[0].get_array()
cor = o1._ims[1].get_array()
axi = o1._ims[2].get_array()
assert_array_equal(sag, data1[5, :, :])
assert_array_equal(cor, data1[:, :, 30].T)
assert_array_equal(axi, data1[:, 10, :].T)
o1.set_position(1, 2, 3)
sag = o1._ims[0].get_array()
cor = o1._ims[1].get_array()
axi = o1._ims[2].get_array()
assert_array_equal(sag, data1[6, :, :])
assert_array_equal(cor, data1[:, :, 32].T)
assert_array_equal(axi, data1[:, 13, :].T)
```

## Next Steps


---

*Source: test_viewers.py:110 | Complexity: Advanced | Last updated: 2026-05-18*