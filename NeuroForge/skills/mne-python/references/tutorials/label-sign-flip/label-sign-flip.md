# How To: Label Sign Flip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test label sign flip computation.

## Prerequisites

**Required Modules:**
- `glob`
- `os`
- `pickle`
- `shutil`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.label`
- `mne.source_estimate`
- `mne.source_space`
- `mne.surface`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test label sign flip computation.'

```python
'Test label sign flip computation.'
```

**Verification:**
```python
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), len(idx))
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), 0.0)
```

### Step 3: Assign label = Label(...)

```python
label = Label(vertices=src[0]['vertno'][:5], hemi='lh')
```

**Verification:**
```python
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), len(idx))
```

### Step 4: Assign unknown = np.array(...)

```python
src[0]['nn'][label.vertices] = np.array([[1.0, 0.0, 0.0], [0.0, 1.0, 0.0], [0, 0, 1.0], [1.0 / np.sqrt(2), 1.0 / np.sqrt(2), 0.0], [1.0 / np.sqrt(2), 1.0 / np.sqrt(2), 0.0]])
```

### Step 5: Assign known_flips = np.array(...)

```python
known_flips = np.array([1, 1, np.nan, 1, 1])
```

### Step 6: Assign idx = value

```python
idx = [0, 1, 3, 4]
```

### Step 7: Assign flip = label_sign_flip(...)

```python
flip = label_sign_flip(label, src)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), len(idx))
```

### Step 9: Assign bi_label = value

```python
bi_label = label + Label(vertices=src[1]['vertno'][:5], hemi='rh')
```

### Step 10: Assign unknown = value

```python
src[1]['nn'][src[1]['vertno'][:5]] = -src[0]['nn'][label.vertices]
```

### Step 11: Assign flip = label_sign_flip(...)

```python
flip = label_sign_flip(bi_label, src)
```

### Step 12: Assign known_flips = np.array(...)

```python
known_flips = np.array([1, 1, np.nan, 1, 1, 1, 1, np.nan, 1, 1])
```

### Step 13: Assign idx = value

```python
idx = [0, 1, 3, 4, 5, 6, 8, 9]
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), 0.0)
```

### Step 15: Assign flip = label_sign_flip(...)

```python
flip = label_sign_flip(bi_label, src)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), len(idx))
```


## Complete Example

```python
# Workflow
'Test label sign flip computation.'
src = read_source_spaces(src_fname)
label = Label(vertices=src[0]['vertno'][:5], hemi='lh')
src[0]['nn'][label.vertices] = np.array([[1.0, 0.0, 0.0], [0.0, 1.0, 0.0], [0, 0, 1.0], [1.0 / np.sqrt(2), 1.0 / np.sqrt(2), 0.0], [1.0 / np.sqrt(2), 1.0 / np.sqrt(2), 0.0]])
known_flips = np.array([1, 1, np.nan, 1, 1])
idx = [0, 1, 3, 4]
flip = label_sign_flip(label, src)
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), len(idx))
bi_label = label + Label(vertices=src[1]['vertno'][:5], hemi='rh')
src[1]['nn'][src[1]['vertno'][:5]] = -src[0]['nn'][label.vertices]
flip = label_sign_flip(bi_label, src)
known_flips = np.array([1, 1, np.nan, 1, 1, 1, 1, np.nan, 1, 1])
idx = [0, 1, 3, 4, 5, 6, 8, 9]
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), 0.0)
src[1]['nn'][src[1]['vertno'][:5]] *= -1
flip = label_sign_flip(bi_label, src)
assert_array_almost_equal(np.dot(flip[idx], known_flips[idx]), len(idx))
```

## Next Steps


---

*Source: test_label.py:1064 | Complexity: Advanced | Last updated: 2026-05-18*