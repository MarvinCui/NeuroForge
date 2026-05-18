# How To: Array Proxy

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test array proxy

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `ecat`
- `openers`
- `testing`
- `tmpdirs`
- `test_fileslice`


## Step-by-Step Guide

### Step 1: Assign dat = self.img.get_fdata(...)

```python
dat = self.img.get_fdata()
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

### Step 3: Assign data_prox = value

```python
data_prox = img.dataobj
```

### Step 4: Assign data2 = np.array(...)

```python
data2 = np.array(data_prox)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(data2, dat)
```

### Step 6: Assign data3 = np.array(...)

```python
data3 = np.array(data_prox)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(data3, dat)
```


## Complete Example

```python
# Workflow
dat = self.img.get_fdata()
img = self.image_class.load(self.example_file)
data_prox = img.dataobj
data2 = np.array(data_prox)
assert_array_equal(data2, dat)
data3 = np.array(data_prox)
assert_array_equal(data3, dat)
```

## Next Steps


---

*Source: test_ecat.py:207 | Complexity: Intermediate | Last updated: 2026-05-18*