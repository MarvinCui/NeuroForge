# How To: Flip Axis

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test flip axis

## Prerequisites

**Required Modules:**
- `numpy`
- `nose.tools`
- `numpy.testing`
- `orientations`
- `affines`


## Step-by-Step Guide

### Step 1: Assign a = np.arange.reshape(...)

```python
a = np.arange(24).reshape((2, 3, 4))
```

**Verification:**
```python
assert_array_equal(flip_axis(a), np.flipud(a))
```

### Step 2: Call assert_array_equal()

```python
assert_array_equal(flip_axis(a), np.flipud(a))
```

**Verification:**
```python
assert_array_equal(flip_axis(a, axis=0), np.flipud(a))
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(flip_axis(a, axis=0), np.flipud(a))
```

**Verification:**
```python
assert_array_equal(flip_axis(a, axis=1), np.fliplr(a))
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(flip_axis(a, axis=1), np.fliplr(a))
```

**Verification:**
```python
assert_array_equal(flip_axis(a.tolist(), axis=0), np.flipud(a))
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(flip_axis(a.tolist(), axis=0), np.flipud(a))
```

**Verification:**
```python
assert_array_equal(flip_axis(a, axis=2), b)
```

### Step 6: Assign b = a.transpose(...)

```python
b = a.transpose()
```

### Step 7: Assign b = np.flipud(...)

```python
b = np.flipud(b)
```

### Step 8: Assign b = b.transpose(...)

```python
b = b.transpose()
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(flip_axis(a, axis=2), b)
```


## Complete Example

```python
# Workflow
a = np.arange(24).reshape((2, 3, 4))
assert_array_equal(flip_axis(a), np.flipud(a))
assert_array_equal(flip_axis(a, axis=0), np.flipud(a))
assert_array_equal(flip_axis(a, axis=1), np.fliplr(a))
assert_array_equal(flip_axis(a.tolist(), axis=0), np.flipud(a))
b = a.transpose()
b = np.flipud(b)
b = b.transpose()
assert_array_equal(flip_axis(a, axis=2), b)
```

## Next Steps


---

*Source: test_orientations.py:128 | Complexity: Advanced | Last updated: 2026-05-18*