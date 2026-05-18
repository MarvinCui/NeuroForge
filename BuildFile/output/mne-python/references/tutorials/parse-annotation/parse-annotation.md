# How To: Parse Annotation

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

**Verification:**
```python
assert_allclose(annotations.onset, want_onset)
```

### Step 2: Assign annot = b'+180\x14Lights off\x14Close door\x14\x00\x00\x00\x00\x00+180\x14Lights off\x14\x00\x00\x00\x00\x00\x00\x00\x00+180\x14Close door\x14\x00\x00\x00\x00\x00\x00\x00\x00+3.14\x1504.20\x14nothing\x14\x00\x00\x00\x00+1800.2\x1525.5\x14Apnea\x14\x00\x00\x00\x00\x00\x00\x00+123\x14\x14\x00\x00\x00\x00\x00\x00\x00'

```python
annot = b'+180\x14Lights off\x14Close door\x14\x00\x00\x00\x00\x00+180\x14Lights off\x14\x00\x00\x00\x00\x00\x00\x00\x00+180\x14Close door\x14\x00\x00\x00\x00\x00\x00\x00\x00+3.14\x1504.20\x14nothing\x14\x00\x00\x00\x00+1800.2\x1525.5\x14Apnea\x14\x00\x00\x00\x00\x00\x00\x00+123\x14\x14\x00\x00\x00\x00\x00\x00\x00'
```

**Verification:**
```python
assert_allclose(annotations.duration, want_duration)
```

### Step 3: Assign annot_file = value

```python
annot_file = tmp_path / 'annotations.txt'
```

**Verification:**
```python
assert_array_equal(annotations.description, want_description)
```

### Step 4: Assign annot = value

```python
annot = [a for a in bytes(annot)]
```

### Step 5: Assign unknown = value

```python
annot[1::2] = [a * 256 for a in annot[1::2]]
```

### Step 6: Assign tal_channel_A = np.array(...)

```python
tal_channel_A = np.array(list(map(sum, zip(annot[0::2], annot[1::2]))), dtype=np.int64)
```

### Step 7: Assign unknown = zip(...)

```python
want_onset, want_duration, want_description = zip(*[[3.14, 4.2, 'nothing'], [180.0, 0.0, 'Lights off'], [180.0, 0.0, 'Close door'], [180.0, 0.0, 'Lights off'], [180.0, 0.0, 'Close door'], [1800.2, 25.5, 'Apnea']])
```

### Step 8: Call f.write()

```python
f.write(annot)
```

### Step 9: Assign tal_channel_B = _read_ch(...)

```python
tal_channel_B = _read_ch(fid, subtype='EDF', dtype='<i2', samp=(len(annot) - 1) // 2, dtype_byte='This_parameter_is_not_used')
```

### Step 10: Assign annotations = _read_annotations_edf(...)

```python
annotations = _read_annotations_edf([tal_channel])
```

### Step 11: Call assert_allclose()

```python
assert_allclose(annotations.onset, want_onset)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(annotations.duration, want_duration)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(annotations.description, want_description)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test parsing the tal channel.'
annot = b'+180\x14Lights off\x14Close door\x14\x00\x00\x00\x00\x00+180\x14Lights off\x14\x00\x00\x00\x00\x00\x00\x00\x00+180\x14Close door\x14\x00\x00\x00\x00\x00\x00\x00\x00+3.14\x1504.20\x14nothing\x14\x00\x00\x00\x00+1800.2\x1525.5\x14Apnea\x14\x00\x00\x00\x00\x00\x00\x00+123\x14\x14\x00\x00\x00\x00\x00\x00\x00'
annot_file = tmp_path / 'annotations.txt'
with open(annot_file, 'wb') as f:
    f.write(annot)
annot = [a for a in bytes(annot)]
annot[1::2] = [a * 256 for a in annot[1::2]]
tal_channel_A = np.array(list(map(sum, zip(annot[0::2], annot[1::2]))), dtype=np.int64)
with open(annot_file, 'rb') as fid:
    tal_channel_B = _read_ch(fid, subtype='EDF', dtype='<i2', samp=(len(annot) - 1) // 2, dtype_byte='This_parameter_is_not_used')
want_onset, want_duration, want_description = zip(*[[3.14, 4.2, 'nothing'], [180.0, 0.0, 'Lights off'], [180.0, 0.0, 'Close door'], [180.0, 0.0, 'Lights off'], [180.0, 0.0, 'Close door'], [1800.2, 25.5, 'Apnea']])
for tal_channel in [tal_channel_A, tal_channel_B]:
    annotations = _read_annotations_edf([tal_channel])
    assert_allclose(annotations.onset, want_onset)
    assert_allclose(annotations.duration, want_duration)
    assert_array_equal(annotations.description, want_description)
```

## Next Steps


---

*Source: test_edf.py:328 | Complexity: Advanced | Last updated: 2026-05-18*