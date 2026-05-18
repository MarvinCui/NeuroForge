# How To: Annot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: Test IO of .annot against freesurfer example data.

## Prerequisites

**Required Modules:**
- `getpass`
- `hashlib`
- `os`
- `struct`
- `time`
- `unittest`
- `os.path`
- `os.path`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileslice`
- `testing`
- `tests.nibabel_data`
- `tmpdirs`
- `io`


## Step-by-Step Guide

### Step 1: 'Test IO of .annot against freesurfer example data.'

```python
'Test IO of .annot against freesurfer example data.'
```

**Verification:**
```python
assert labels.shape == (163842,)
```

### Step 2: Assign annots = value

```python
annots = ['aparc', 'aparc.a2005s']
```

**Verification:**
```python
assert ctab.shape == (len(names), 5)
```

### Step 3: Assign annot_path = pjoin(...)

```python
annot_path = pjoin(data_path, 'label', f'lh.{a}.annot')
```

**Verification:**
```python
assert np.sum(labels_orig == 0) == 13887
```

### Step 4: Assign unknown = read_annot(...)

```python
labels, ctab, names = read_annot(annot_path)
```

**Verification:**
```python
assert np.sum(labels_orig == 1639705) == 13327
```

### Step 5: Assign labels_orig = None

```python
labels_orig = None
```

**Verification:**
```python
assert np.array_equal(labels, labels2)
```

### Step 6: Assign unknown = read_annot(...)

```python
labels_orig, _, _ = read_annot(annot_path, orig_ids=True)
```

**Verification:**
```python
assert np.array_equal(labels_orig, labels_orig_2)
```

### Step 7: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(labels == -1, labels_orig == 0)
```

**Verification:**
```python
assert np.array_equal(ctab, ctab2)
```

### Step 8: Assign content_hash = hashlib.md5.hexdigest(...)

```python
content_hash = hashlib.md5(Path(annot_path).read_bytes()).hexdigest()
```

**Verification:**
```python
assert names == names2
```

### Step 9: Assign annot_path = 'test'

```python
annot_path = 'test'
```

### Step 10: Call write_annot()

```python
write_annot(annot_path, labels, ctab, names)
```

### Step 11: Assign unknown = read_annot(...)

```python
labels2, ctab2, names2 = read_annot(annot_path)
```

**Verification:**
```python
assert np.array_equal(labels_orig, labels_orig_2)
```

### Step 12: Assign unknown = read_annot(...)

```python
labels_orig_2, _, _ = read_annot(annot_path, orig_ids=True)
```

**Verification:**
```python
assert np.sum(labels_orig == 1639705) == 13327
```


## Complete Example

```python
# Workflow
'Test IO of .annot against freesurfer example data.'
annots = ['aparc', 'aparc.a2005s']
for a in annots:
    annot_path = pjoin(data_path, 'label', f'lh.{a}.annot')
    labels, ctab, names = read_annot(annot_path)
    assert labels.shape == (163842,)
    assert ctab.shape == (len(names), 5)
    labels_orig = None
    if a == 'aparc':
        labels_orig, _, _ = read_annot(annot_path, orig_ids=True)
        np.testing.assert_array_equal(labels == -1, labels_orig == 0)
        content_hash = hashlib.md5(Path(annot_path).read_bytes()).hexdigest()
        if content_hash == 'bf0b488994657435cdddac5f107d21e8':
            assert np.sum(labels_orig == 0) == 13887
        elif content_hash == 'd4f5b7cbc2ed363ac6fcf89e19353504':
            assert np.sum(labels_orig == 1639705) == 13327
        else:
            raise RuntimeError('Unknown freesurfer file. Please report the problem to the maintainer of nibabel.')
    with InTemporaryDirectory():
        annot_path = 'test'
        write_annot(annot_path, labels, ctab, names)
        labels2, ctab2, names2 = read_annot(annot_path)
        if labels_orig is not None:
            labels_orig_2, _, _ = read_annot(annot_path, orig_ids=True)
    assert np.array_equal(labels, labels2)
    if labels_orig is not None:
        assert np.array_equal(labels_orig, labels_orig_2)
    assert np.array_equal(ctab, ctab2)
    assert names == names2
```

## Next Steps


---

*Source: test_io.py:176 | Complexity: Advanced | Last updated: 2026-05-18*