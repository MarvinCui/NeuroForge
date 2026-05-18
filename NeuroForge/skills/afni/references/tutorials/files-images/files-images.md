# How To: Files Images

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test files images

## Prerequisites

**Required Modules:**
- `numpy`
- `py3k`
- `fileholders`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign arr = np.zeros(...)

```python
arr = np.zeros((2, 3, 4))
```

**Verification:**
```python
assert_equal(value.filename, None)
```

### Step 2: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

**Verification:**
```python
assert_equal(value.fileobj, None)
```

### Step 3: Assign klass = value

```python
klass = img_def['class']
```

**Verification:**
```python
assert_equal(value.pos, 0)
```

### Step 4: Assign file_map = klass.make_file_map(...)

```python
file_map = klass.make_file_map()
```

**Verification:**
```python
assert_equal(value.filename, None)
```

### Step 5: Call assert_equal()

```python
assert_equal(value.filename, None)
```

**Verification:**
```python
assert_equal(value.fileobj, None)
```

### Step 6: Call assert_equal()

```python
assert_equal(value.fileobj, None)
```

**Verification:**
```python
assert_equal(value.pos, 0)
```

### Step 7: Call assert_equal()

```python
assert_equal(value.pos, 0)
```

### Step 8: Assign img = klass(...)

```python
img = klass(arr.astype(np.float32), aff)
```

### Step 9: Assign img = klass(...)

```python
img = klass(arr, aff)
```

### Step 10: Call assert_equal()

```python
assert_equal(value.filename, None)
```

### Step 11: Call assert_equal()

```python
assert_equal(value.fileobj, None)
```

### Step 12: Call assert_equal()

```python
assert_equal(value.pos, 0)
```


## Complete Example

```python
# Workflow
arr = np.zeros((2, 3, 4))
aff = np.eye(4)
for img_def in class_map.values():
    klass = img_def['class']
    file_map = klass.make_file_map()
    for key, value in file_map.items():
        assert_equal(value.filename, None)
        assert_equal(value.fileobj, None)
        assert_equal(value.pos, 0)
    if klass == MGHImage:
        img = klass(arr.astype(np.float32), aff)
    else:
        img = klass(arr, aff)
    for key, value in img.file_map.items():
        assert_equal(value.filename, None)
        assert_equal(value.fileobj, None)
        assert_equal(value.pos, 0)
```

## Next Steps


---

*Source: test_files_interface.py:24 | Complexity: Advanced | Last updated: 2026-05-18*