# How To: Read Write Annot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: Test generating .annot file and reading it back.

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

### Step 1: 'Test generating .annot file and reading it back.'

```python
'Test generating .annot file and reading it back.'
```

**Verification:**
```python
assert np.all(np.isclose(rgbal2, rgbal))
```

### Step 2: Assign nvertices = 10

```python
nvertices = 10
```

**Verification:**
```python
assert np.all(np.isclose(labels2, labels))
```

### Step 3: Assign nlabels = 3

```python
nlabels = 3
```

**Verification:**
```python
assert names2 == names
```

### Step 4: Assign names = value

```python
names = [f'label {l}' for l in range(1, nlabels + 1)]
```

### Step 5: Assign labels = value

```python
labels = list(range(nlabels)) + list(np.random.randint(0, nlabels, nvertices - nlabels))
```

### Step 6: Assign labels = np.array(...)

```python
labels = np.array(labels, dtype=np.int32)
```

### Step 7: Call np.random.shuffle()

```python
np.random.shuffle(labels)
```

### Step 8: Assign rgbal = np.zeros(...)

```python
rgbal = np.zeros((nlabels, 5), dtype=np.int32)
```

### Step 9: Assign unknown = np.random.randint(...)

```python
rgbal[:, :4] = np.random.randint(0, 255, (nlabels, 4))
```

### Step 10: Assign unknown = 255

```python
rgbal[0, 3] = 255
```

### Step 11: Assign unknown = value

```python
rgbal[:, 4] = rgbal[:, 0] + rgbal[:, 1] * 2 ** 8 + rgbal[:, 2] * 2 ** 16
```

### Step 12: Assign annot_path = 'c.annot'

```python
annot_path = 'c.annot'
```

### Step 13: Call write_annot()

```python
write_annot(annot_path, labels, rgbal, names, fill_ctab=False)
```

### Step 14: Assign unknown = read_annot(...)

```python
labels2, rgbal2, names2 = read_annot(annot_path)
```

### Step 15: Assign names2 = value

```python
names2 = [n.decode('ascii') for n in names2]
```

**Verification:**
```python
assert np.all(np.isclose(rgbal2, rgbal))
```


## Complete Example

```python
# Workflow
'Test generating .annot file and reading it back.'
nvertices = 10
nlabels = 3
names = [f'label {l}' for l in range(1, nlabels + 1)]
labels = list(range(nlabels)) + list(np.random.randint(0, nlabels, nvertices - nlabels))
labels = np.array(labels, dtype=np.int32)
np.random.shuffle(labels)
rgbal = np.zeros((nlabels, 5), dtype=np.int32)
rgbal[:, :4] = np.random.randint(0, 255, (nlabels, 4))
rgbal[0, 3] = 255
rgbal[:, 4] = rgbal[:, 0] + rgbal[:, 1] * 2 ** 8 + rgbal[:, 2] * 2 ** 16
annot_path = 'c.annot'
with InTemporaryDirectory():
    write_annot(annot_path, labels, rgbal, names, fill_ctab=False)
    labels2, rgbal2, names2 = read_annot(annot_path)
    names2 = [n.decode('ascii') for n in names2]
    assert np.all(np.isclose(rgbal2, rgbal))
    assert np.all(np.isclose(labels2, labels))
    assert names2 == names
```

## Next Steps


---

*Source: test_io.py:220 | Complexity: Advanced | Last updated: 2026-05-18*