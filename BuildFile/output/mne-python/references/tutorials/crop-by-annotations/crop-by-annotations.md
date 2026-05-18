# How To: Crop By Annotations

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test crop by annotations of raw.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `os`
- `re`
- `contextlib`
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne._fiff.utils`
- `mne.io`
- `mne.io.base`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: meas_date, first_samp
```

## Step-by-Step Guide

### Step 1: 'Test crop by annotations of raw.'

```python
'Test crop by annotations of raw.'
```

**Verification:**
```python
assert len(raws) == 2
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert len(raws[0].annotations) == 1
```

### Step 3: Assign raw = mne.io.RawArray(...)

```python
raw = mne.io.RawArray(raw.get_data(), raw.info, first_samp=first_samp)
```

**Verification:**
```python
assert raws[0].times[-1] == pytest.approx(annot[:1].duration[0], rel=0.001)
```

### Step 4: Assign onset = np.array(...)

```python
onset = np.array([0, 1.5], float)
```

**Verification:**
```python
assert raws[0].annotations.description[0] == annot.description[0]
```

### Step 5: Assign annot = mne.Annotations(...)

```python
annot = mne.Annotations(onset=onset, duration=[1, 0.5], description=['a', 'b'], orig_time=raw.info['meas_date'])
```

**Verification:**
```python
assert len(raws[1].annotations) == 1
```

### Step 6: Call raw.set_annotations()

```python
raw.set_annotations(annot)
```

**Verification:**
```python
assert raws[1].times[-1] == pytest.approx(annot[1:2].duration[0], rel=0.005)
```

### Step 7: Assign raws = raw.crop_by_annotations(...)

```python
raws = raw.crop_by_annotations()
```

**Verification:**
```python
assert raws[1].annotations.description[0] == annot.description[1]
```

### Step 8: Call raw.set_meas_date()

```python
raw.set_meas_date(None)
```


## Complete Example

```python
# Setup
# Fixtures: meas_date, first_samp

# Workflow
'Test crop by annotations of raw.'
raw = read_raw_fif(raw_fname)
if meas_date is None:
    raw.set_meas_date(None)
raw = mne.io.RawArray(raw.get_data(), raw.info, first_samp=first_samp)
onset = np.array([0, 1.5], float)
if meas_date is not None:
    onset += raw.first_time
annot = mne.Annotations(onset=onset, duration=[1, 0.5], description=['a', 'b'], orig_time=raw.info['meas_date'])
raw.set_annotations(annot)
raws = raw.crop_by_annotations()
assert len(raws) == 2
assert len(raws[0].annotations) == 1
assert raws[0].times[-1] == pytest.approx(annot[:1].duration[0], rel=0.001)
assert raws[0].annotations.description[0] == annot.description[0]
assert len(raws[1].annotations) == 1
assert raws[1].times[-1] == pytest.approx(annot[1:2].duration[0], rel=0.005)
assert raws[1].annotations.description[0] == annot.description[1]
```

## Next Steps


---

*Source: test_raw.py:634 | Complexity: Advanced | Last updated: 2026-05-18*