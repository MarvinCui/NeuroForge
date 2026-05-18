# How To: Read Ctf Annotations Smoke Test

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading CTF marker file.

`testdata_ctf_mc.ds` has no trials or offsets therefore its a plain reading
of whatever is in the MarkerFile.mrk.

## Prerequisites

**Required Modules:**
- `copy`
- `os`
- `shutil`
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `mne`
- `mne.io.ctf.info`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.io`
- `mne.io.ctf.constants`
- `mne.io.ctf.info`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test reading CTF marker file.\n\n    `testdata_ctf_mc.ds` has no trials or offsets therefore its a plain reading\n    of whatever is in the MarkerFile.mrk.\n    '

```python
'Test reading CTF marker file.\n\n    `testdata_ctf_mc.ds` has no trials or offsets therefore its a plain reading\n    of whatever is in the MarkerFile.mrk.\n    '
```

**Verification:**
```python
assert_allclose(annot.onset, EXPECTED_ONSET)
```

### Step 2: Assign EXPECTED_ONSET = value

```python
EXPECTED_ONSET = [0.0, 0.1425, 0.285, 0.42833333, 0.57083333, 0.71416667, 0.85666667, 0.99916667, 1.1425, 1.285, 1.4275, 1.57083333, 1.71333333, 1.85666667, 1.99916667, 2.14166667, 2.285, 2.4275, 2.57083333, 2.71333333, 2.85583333, 2.99916667, 3.14166667, 3.28416667, 3.4275, 3.57, 3.71333333, 3.85583333, 3.99833333, 4.14166667, 4.28416667, 4.42666667, 4.57, 4.7125, 4.85583333, 4.99833333]
```

### Step 3: Assign fname = op.join(...)

```python
fname = op.join(ctf_dir, 'testdata_ctf_mc.ds')
```

### Step 4: Assign annot = read_annotations(...)

```python
annot = read_annotations(fname)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(annot.onset, EXPECTED_ONSET)
```

### Step 6: Assign raw = read_raw_ctf(...)

```python
raw = read_raw_ctf(fname)
```

### Step 7: Call _assert_annotations_equal()

```python
_assert_annotations_equal(raw.annotations, annot, 1e-06)
```


## Complete Example

```python
# Workflow
'Test reading CTF marker file.\n\n    `testdata_ctf_mc.ds` has no trials or offsets therefore its a plain reading\n    of whatever is in the MarkerFile.mrk.\n    '
EXPECTED_ONSET = [0.0, 0.1425, 0.285, 0.42833333, 0.57083333, 0.71416667, 0.85666667, 0.99916667, 1.1425, 1.285, 1.4275, 1.57083333, 1.71333333, 1.85666667, 1.99916667, 2.14166667, 2.285, 2.4275, 2.57083333, 2.71333333, 2.85583333, 2.99916667, 3.14166667, 3.28416667, 3.4275, 3.57, 3.71333333, 3.85583333, 3.99833333, 4.14166667, 4.28416667, 4.42666667, 4.57, 4.7125, 4.85583333, 4.99833333]
fname = op.join(ctf_dir, 'testdata_ctf_mc.ds')
annot = read_annotations(fname)
assert_allclose(annot.onset, EXPECTED_ONSET)
raw = read_raw_ctf(fname)
_assert_annotations_equal(raw.annotations, annot, 1e-06)
```

## Next Steps


---

*Source: test_ctf.py:625 | Complexity: Intermediate | Last updated: 2026-05-18*