# How To: Object Size

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test object size estimation.

## Prerequisites

**Required Modules:**
- `copy`
- `datetime`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.time_frequency`
- `mne.utils`
- `mne.utils.numerics`
- `sklearn.decomposition`


## Step-by-Step Guide

### Step 1: 'Test object size estimation.'

```python
'Test object size estimation.'
```

**Verification:**
```python
assert object_size(np.ones(10, np.float32)) < object_size(np.ones(10, np.float64))
```

### Step 2: Assign x = dict(...)

```python
x = dict(a=1)
```

**Verification:**
```python
assert lower < size < upper, f'{lower} < {size} < {upper}:\n{obj}'
```

### Step 3: Assign unknown = np.ones(...)

```python
x['a'] = np.ones(100000, float)
```

**Verification:**
```python
assert object_size(x) < 1000
```

### Step 4: Assign nb = value

```python
nb = x['a'].nbytes
```

**Verification:**
```python
assert nb < sz < nb * 1.01
```

### Step 5: Assign sz = object_size(...)

```python
sz = object_size(x)
```

**Verification:**
```python
assert nb < sz < nb * 1.01
```

### Step 6: Assign unknown = value

```python
x['b'] = x['a']
```

**Verification:**
```python
assert x['a'].flags.writeable
```

### Step 7: Assign sz = object_size(...)

```python
sz = object_size(x)
```

**Verification:**
```python
assert nb < sz < nb * 1.01
```

### Step 8: Assign unknown = unknown.view(...)

```python
x['b'] = x['a'].view()
```

### Step 9: Assign unknown.flags.writeable = False

```python
x['b'].flags.writeable = False
```

**Verification:**
```python
assert x['a'].flags.writeable
```

### Step 10: Assign sz = object_size(...)

```python
sz = object_size(x)
```

**Verification:**
```python
assert nb < sz < nb * 1.01
```

### Step 11: Assign size = object_size(...)

```python
size = object_size(obj)
```

**Verification:**
```python
assert lower < size < upper, f'{lower} < {size} < {upper}:\n{obj}'
```


## Complete Example

```python
# Workflow
'Test object size estimation.'
assert object_size(np.ones(10, np.float32)) < object_size(np.ones(10, np.float64))
for lower, upper, obj in ((0, 60, ''), (0, 30, 1), (0, 30, 1.0), (0, 70, 'foo'), (0, 150, np.ones(0)), (0, 150, np.int32(1)), (150, 500, np.ones(20)), (30, 400, dict()), (400, 1000, dict(a=np.ones(50))), (200, 900, _eye_array(20, format='csc')), (200, 900, _eye_array(20, format='csr'))):
    size = object_size(obj)
    assert lower < size < upper, f'{lower} < {size} < {upper}:\n{obj}'
x = dict(a=1)
assert object_size(x) < 1000
x['a'] = np.ones(100000, float)
nb = x['a'].nbytes
sz = object_size(x)
assert nb < sz < nb * 1.01
x['b'] = x['a']
sz = object_size(x)
assert nb < sz < nb * 1.01
x['b'] = x['a'].view()
x['b'].flags.writeable = False
assert x['a'].flags.writeable
sz = object_size(x)
assert nb < sz < nb * 1.01
```

## Next Steps


---

*Source: test_numerics.py:305 | Complexity: Advanced | Last updated: 2026-05-18*