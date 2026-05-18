# How To: Array Proxy

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test array proxy

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `numpy`
- `py3k`
- `volumeutils`
- `ecat`
- `unittest`
- `nose.tools`
- `numpy.testing`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign dat = self.img.get_data(...)

```python
dat = self.img.get_data()
```

**Verification:**
```python
assert_array_equal(data2, dat)
```

### Step 2: Assign img = self.image_class.load(...)

```python
img = self.image_class.load(self.example_file)
```

**Verification:**
```python
assert_array_equal(data3, dat)
```

### Step 3: Assign secret_data = value

```python
secret_data = img._data
```

### Step 4: Assign data2 = np.array(...)

```python
data2 = np.array(secret_data)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(data2, dat)
```

### Step 6: Assign data3 = np.array(...)

```python
data3 = np.array(secret_data)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(data3, dat)
```


## Complete Example

```python
# Workflow
dat = self.img.get_data()
img = self.image_class.load(self.example_file)
secret_data = img._data
data2 = np.array(secret_data)
assert_array_equal(data2, dat)
data3 = np.array(secret_data)
assert_array_equal(data3, dat)
```

## Next Steps


---

*Source: test_ecat.py:218 | Complexity: Intermediate | Last updated: 2026-05-18*