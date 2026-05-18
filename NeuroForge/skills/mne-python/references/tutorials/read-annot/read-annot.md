# How To: Read Annot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test parsing the tal channel.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `contextlib`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.edf.edf`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test parsing the tal channel.'

```python
'Test parsing the tal channel.'
```

### Step 2: Assign EXPECTED_ANNOTATIONS = value

```python
EXPECTED_ANNOTATIONS = [[180.0, 0, 'Lights off'], [180.0, 0, 'Close door'], [180.0, 0, 'Lights off'], [180.0, 0, 'Close door'], [3.14, 4.2, 'nothing'], [1800.2, 25.5, 'Apnea']]
```

### Step 3: Assign EXPECTED_ONSET = value

```python
EXPECTED_ONSET = [180.0, 180.0, 180.0, 180.0, 3.14, 1800.2]
```

### Step 4: Assign EXPECTED_DURATION = value

```python
EXPECTED_DURATION = [0, 0, 0, 0, 4.2, 25.5]
```

### Step 5: Assign EXPECTED_DESC = value

```python
EXPECTED_DESC = ['Lights off', 'Close door', 'Lights off', 'Close door', 'nothing', 'Apnea']
```

### Step 6: Assign EXPECTED_ANNOTATIONS = Annotations(...)

```python
EXPECTED_ANNOTATIONS = Annotations(onset=EXPECTED_ONSET, duration=EXPECTED_DURATION, description=EXPECTED_DESC, orig_time=None)
```

### Step 7: Assign annot = b'+180\x14Lights off\x14Close door\x14\x00\x00\x00\x00\x00+180\x14Lights off\x14\x00\x00\x00\x00\x00\x00\x00\x00+180\x14Close door\x14\x00\x00\x00\x00\x00\x00\x00\x00+3.14\x1504.20\x14nothing\x14\x00\x00\x00\x00+1800.2\x1525.5\x14Apnea\x14\x00\x00\x00\x00\x00\x00\x00+123\x14\x14\x00\x00\x00\x00\x00\x00\x00'

```python
annot = b'+180\x14Lights off\x14Close door\x14\x00\x00\x00\x00\x00+180\x14Lights off\x14\x00\x00\x00\x00\x00\x00\x00\x00+180\x14Close door\x14\x00\x00\x00\x00\x00\x00\x00\x00+3.14\x1504.20\x14nothing\x14\x00\x00\x00\x00+1800.2\x1525.5\x14Apnea\x14\x00\x00\x00\x00\x00\x00\x00+123\x14\x14\x00\x00\x00\x00\x00\x00\x00'
```

### Step 8: Assign annot_file = value

```python
annot_file = tmp_path / 'annotations.txt'
```

### Step 9: Assign annotations = _read_annotations_edf(...)

```python
annotations = _read_annotations_edf(annotations=str(annot_file))
```

### Step 10: Call _assert_annotations_equal()

```python
_assert_annotations_equal(annotations, EXPECTED_ANNOTATIONS)
```

### Step 11: Assign annotations = _read_annotations_edf(...)

```python
annotations = _read_annotations_edf([ch_data])
```

### Step 12: Call _assert_annotations_equal()

```python
_assert_annotations_equal(annotations, EXPECTED_ANNOTATIONS)
```

### Step 13: Call f.write()

```python
f.write(annot)
```

### Step 14: Assign ch_data = np.fromfile(...)

```python
ch_data = np.fromfile(fid, dtype='<i2', count=len(annot))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test parsing the tal channel.'
EXPECTED_ANNOTATIONS = [[180.0, 0, 'Lights off'], [180.0, 0, 'Close door'], [180.0, 0, 'Lights off'], [180.0, 0, 'Close door'], [3.14, 4.2, 'nothing'], [1800.2, 25.5, 'Apnea']]
EXPECTED_ONSET = [180.0, 180.0, 180.0, 180.0, 3.14, 1800.2]
EXPECTED_DURATION = [0, 0, 0, 0, 4.2, 25.5]
EXPECTED_DESC = ['Lights off', 'Close door', 'Lights off', 'Close door', 'nothing', 'Apnea']
EXPECTED_ANNOTATIONS = Annotations(onset=EXPECTED_ONSET, duration=EXPECTED_DURATION, description=EXPECTED_DESC, orig_time=None)
annot = b'+180\x14Lights off\x14Close door\x14\x00\x00\x00\x00\x00+180\x14Lights off\x14\x00\x00\x00\x00\x00\x00\x00\x00+180\x14Close door\x14\x00\x00\x00\x00\x00\x00\x00\x00+3.14\x1504.20\x14nothing\x14\x00\x00\x00\x00+1800.2\x1525.5\x14Apnea\x14\x00\x00\x00\x00\x00\x00\x00+123\x14\x14\x00\x00\x00\x00\x00\x00\x00'
annot_file = tmp_path / 'annotations.txt'
with open(annot_file, 'wb') as f:
    f.write(annot)
annotations = _read_annotations_edf(annotations=str(annot_file))
_assert_annotations_equal(annotations, EXPECTED_ANNOTATIONS)
with open(annot_file, 'rb') as fid:
    ch_data = np.fromfile(fid, dtype='<i2', count=len(annot))
annotations = _read_annotations_edf([ch_data])
_assert_annotations_equal(annotations, EXPECTED_ANNOTATIONS)
```

## Next Steps


---

*Source: test_edf.py:443 | Complexity: Advanced | Last updated: 2026-05-18*