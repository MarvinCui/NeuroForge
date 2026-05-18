# How To: Dkl2Rgb

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the conversion (forward) for DKL to RGB (signed).

    

## Prerequisites

**Required Modules:**
- `psychopy.tools.colorspacetools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test the conversion (forward) for DKL to RGB (signed).\n\n    '

```python
'Test the conversion (forward) for DKL to RGB (signed).\n\n    '
```

**Verification:**
```python
assert np.allclose(np.asarray((1, 1, 1)), dkl2rgb(dklWhite))
```

### Step 2: Assign N = 1024

```python
N = 1024
```

### Step 3: Call np.random.seed()

```python
np.random.seed(123456)
```

### Step 4: Assign dklColors = np.zeros(...)

```python
dklColors = np.zeros((N, 3))
```

### Step 5: Assign unknown = np.random.uniform(...)

```python
dklColors[:, 0] = np.random.uniform(0, 90, (N,))
```

### Step 6: Assign unknown = np.random.uniform(...)

```python
dklColors[:, 1] = np.random.uniform(0, 360, (N,))
```

### Step 7: Assign unknown = np.random.uniform(...)

```python
dklColors[:, 2] = np.random.uniform(0, 1, (N,))
```

### Step 8: Assign _ = dkl2rgb(...)

```python
_ = dkl2rgb(dklColors)
```

### Step 9: Assign dklWhite = value

```python
dklWhite = [90, 0, 1]
```

**Verification:**
```python
assert np.allclose(np.asarray((1, 1, 1)), dkl2rgb(dklWhite))
```


## Complete Example

```python
# Workflow
'Test the conversion (forward) for DKL to RGB (signed).\n\n    '
N = 1024
np.random.seed(123456)
dklColors = np.zeros((N, 3))
dklColors[:, 0] = np.random.uniform(0, 90, (N,))
dklColors[:, 1] = np.random.uniform(0, 360, (N,))
dklColors[:, 2] = np.random.uniform(0, 1, (N,))
_ = dkl2rgb(dklColors)
dklWhite = [90, 0, 1]
assert np.allclose(np.asarray((1, 1, 1)), dkl2rgb(dklWhite))
```

## Next Steps


---

*Source: test_colorspacetools.py:77 | Complexity: Advanced | Last updated: 2026-05-18*