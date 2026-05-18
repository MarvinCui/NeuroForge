# How To: Multiload

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multiload

## Prerequisites

**Required Modules:**
- `__future__`
- `os.path`
- `shutil`
- `tempfile`
- `warnings`
- `numpy`
- `loadsave`
- `nifti1`
- `numpy.testing`
- `nose.tools`
- `resource`


## Step-by-Step Guide

### Step 1: Assign N = value

```python
N = SOFT_LIMIT + 100
```

### Step 2: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24).reshape((2, 3, 4))
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, np.eye(4))
```

### Step 4: Assign imgs = value

```python
imgs = []
```

### Step 5: Call warn()

```python
warn('It would take too long to test file handles, aborting')
```

### Step 6: Assign tmpdir = mkdtemp(...)

```python
tmpdir = mkdtemp()
```

### Step 7: Assign fname = pjoin(...)

```python
fname = pjoin(tmpdir, 'test.img')
```

### Step 8: Call save()

```python
save(img, fname)
```

### Step 9: Call shutil.rmtree()

```python
shutil.rmtree(tmpdir)
```

### Step 10: Call imgs.append()

```python
imgs.append(load(fname))
```


## Complete Example

```python
# Workflow
N = SOFT_LIMIT + 100
if N > 5000:
    warn('It would take too long to test file handles, aborting')
    return
arr = np.arange(24).reshape((2, 3, 4))
img = Nifti1Image(arr, np.eye(4))
imgs = []
try:
    tmpdir = mkdtemp()
    fname = pjoin(tmpdir, 'test.img')
    save(img, fname)
    for i in range(N):
        imgs.append(load(fname))
finally:
    del img, imgs
    shutil.rmtree(tmpdir)
```

## Next Steps


---

*Source: test_filehandles.py:30 | Complexity: Advanced | Last updated: 2026-05-18*