# How To: Multiload

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test multiload

## Prerequisites

**Required Modules:**
- `shutil`
- `unittest`
- `os.path`
- `tempfile`
- `numpy`
- `loadsave`
- `nifti1`
- `resource`


## Step-by-Step Guide

### Step 1: Assign N = value

```python
N = SOFT_LIMIT + 100
```

### Step 2: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24, dtype='int32').reshape((2, 3, 4))
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, np.eye(4))
```

### Step 4: Assign imgs = value

```python
imgs = []
```

### Step 5: Assign tmpdir = mkdtemp(...)

```python
tmpdir = mkdtemp()
```

### Step 6: Assign fname = pjoin(...)

```python
fname = pjoin(tmpdir, 'test.img')
```

### Step 7: Call save()

```python
save(img, fname)
```

### Step 8: Call imgs.extend()

```python
imgs.extend((load(fname) for _ in range(N)))
```

### Step 9: Call shutil.rmtree()

```python
shutil.rmtree(tmpdir)
```


## Complete Example

```python
# Workflow
N = SOFT_LIMIT + 100
arr = np.arange(24, dtype='int32').reshape((2, 3, 4))
img = Nifti1Image(arr, np.eye(4))
imgs = []
try:
    tmpdir = mkdtemp()
    fname = pjoin(tmpdir, 'test.img')
    save(img, fname)
    imgs.extend((load(fname) for _ in range(N)))
finally:
    del img, imgs
    shutil.rmtree(tmpdir)
```

## Next Steps


---

*Source: test_filehandles.py:25 | Complexity: Advanced | Last updated: 2026-05-18*