# How To: Label Io

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test IO of label files.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test IO of label files.'

```python
'Test IO of label files.'
```

**Verification:**
```python
assert_equal(label.name, 'test-lh')
```

### Step 2: Assign label = read_label(...)

```python
label = read_label(label_fname)
```

**Verification:**
```python
assert label.subject is None
```

### Step 3: Call assert_equal()

```python
assert_equal(label.name, 'test-lh')
```

**Verification:**
```python
assert label.color is None
```

### Step 4: Call label.save()

```python
label.save(tmp_path / 'foo')
```

**Verification:**
```python
assert_labels_equal(label, label2)
```

### Step 5: Assign label2 = read_label(...)

```python
label2 = read_label(tmp_path / 'foo-lh.label')
```

**Verification:**
```python
assert_labels_equal(label, label2)
```

### Step 6: Call assert_labels_equal()

```python
assert_labels_equal(label, label2)
```

### Step 7: Assign dest = value

```python
dest = tmp_path / 'foo.pickled'
```

### Step 8: Call assert_labels_equal()

```python
assert_labels_equal(label, label2)
```

### Step 9: Call pickle.dump()

```python
pickle.dump(label, fid, pickle.HIGHEST_PROTOCOL)
```

### Step 10: Assign label2 = pickle.load(...)

```python
label2 = pickle.load(fid)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test IO of label files.'
label = read_label(label_fname)
assert_equal(label.name, 'test-lh')
assert label.subject is None
assert label.color is None
label.save(tmp_path / 'foo')
label2 = read_label(tmp_path / 'foo-lh.label')
assert_labels_equal(label, label2)
dest = tmp_path / 'foo.pickled'
with open(dest, 'wb') as fid:
    pickle.dump(label, fid, pickle.HIGHEST_PROTOCOL)
with open(dest, 'rb') as fid:
    label2 = pickle.load(fid)
assert_labels_equal(label, label2)
```

## Next Steps


---

*Source: test_label.py:332 | Complexity: Advanced | Last updated: 2026-05-18*