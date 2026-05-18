# How To: Repr

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test repr of Raw.

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
# Fixtures: sfreq
```

## Step-by-Step Guide

### Step 1: 'Test repr of Raw.'

```python
'Test repr of Raw.'
```

**Verification:**
```python
assert r == f'<RawArray | 3 x {sample_count} (10.0 s), ~{size_str}, data loaded>'
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(3, sfreq)
```

**Verification:**
```python
assert raw._repr_html_()
```

### Step 3: Assign sample_count = value

```python
sample_count = 10 * sfreq
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(np.zeros((3, sample_count)), info)
```

### Step 5: Assign r = repr(...)

```python
r = repr(raw)
```

### Step 6: Assign size_str = sizeof_fmt(...)

```python
size_str = sizeof_fmt(raw._size)
```

**Verification:**
```python
assert r == f'<RawArray | 3 x {sample_count} (10.0 s), ~{size_str}, data loaded>'
```


## Complete Example

```python
# Setup
# Fixtures: sfreq

# Workflow
'Test repr of Raw.'
info = create_info(3, sfreq)
sample_count = 10 * sfreq
raw = RawArray(np.zeros((3, sample_count)), info)
r = repr(raw)
size_str = sizeof_fmt(raw._size)
assert r == f'<RawArray | 3 x {sample_count} (10.0 s), ~{size_str}, data loaded>'
assert raw._repr_html_()
```

## Next Steps


---

*Source: test_raw.py:818 | Complexity: Intermediate | Last updated: 2026-05-18*