# How To: Rgb2Hsv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the conversion (forward and inverse) for HSV to RGB (signed). This
does not test for "correctness", but rather if the functions provided for
the conversion are the inverse of each other.

## Prerequisites

**Required Modules:**
- `psychopy.tools.colorspacetools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test the conversion (forward and inverse) for HSV to RGB (signed). This\n    does not test for "correctness", but rather if the functions provided for\n    the conversion are the inverse of each other.\n\n    '

```python
'Test the conversion (forward and inverse) for HSV to RGB (signed). This\n    does not test for "correctness", but rather if the functions provided for\n    the conversion are the inverse of each other.\n\n    '
```

**Verification:**
```python
assert np.allclose(hsvOut, hsvColors)
```

### Step 2: Assign N = 1024

```python
N = 1024
```

**Verification:**
```python
assert np.allclose(hsvOut, hsvColors)
```

### Step 3: Call np.random.seed()

```python
np.random.seed(123456)
```

### Step 4: Assign hsvColors = np.zeros(...)

```python
hsvColors = np.zeros((N, 3))
```

### Step 5: Assign unknown = np.random.randint(...)

```python
hsvColors[:, 0] = np.random.randint(0, 360, (N,))
```

### Step 6: Assign unknown = np.random.uniform(...)

```python
hsvColors[:, 1:] = np.random.uniform(0, 1, (N, 2))
```

### Step 7: Assign hsvOut = rgb2hsv(...)

```python
hsvOut = rgb2hsv(hsv2rgb(hsvColors))
```

**Verification:**
```python
assert np.allclose(hsvOut, hsvColors)
```

### Step 8: Assign hsvColors = np.zeros(...)

```python
hsvColors = np.zeros((N, N, 3))
```

### Step 9: Assign unknown = np.random.randint(...)

```python
hsvColors[:, :, 0] = np.random.randint(0, 360, (N, N))
```

### Step 10: Assign unknown = np.random.uniform(...)

```python
hsvColors[:, :, 1:] = np.random.uniform(0, 1, (N, N, 2))
```

### Step 11: Assign hsvOut = rgb2hsv(...)

```python
hsvOut = rgb2hsv(hsv2rgb(hsvColors))
```

**Verification:**
```python
assert np.allclose(hsvOut, hsvColors)
```


## Complete Example

```python
# Workflow
'Test the conversion (forward and inverse) for HSV to RGB (signed). This\n    does not test for "correctness", but rather if the functions provided for\n    the conversion are the inverse of each other.\n\n    '
N = 1024
np.random.seed(123456)
hsvColors = np.zeros((N, 3))
hsvColors[:, 0] = np.random.randint(0, 360, (N,))
hsvColors[:, 1:] = np.random.uniform(0, 1, (N, 2))
hsvOut = rgb2hsv(hsv2rgb(hsvColors))
assert np.allclose(hsvOut, hsvColors)
hsvColors = np.zeros((N, N, 3))
hsvColors[:, :, 0] = np.random.randint(0, 360, (N, N))
hsvColors[:, :, 1:] = np.random.uniform(0, 1, (N, N, 2))
hsvOut = rgb2hsv(hsv2rgb(hsvColors))
assert np.allclose(hsvOut, hsvColors)
```

## Next Steps


---

*Source: test_colorspacetools.py:11 | Complexity: Advanced | Last updated: 2026-05-18*