# How To: Annotation Epoching

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that annotations work properly with concatenated edges.

## Prerequisites

**Required Modules:**
- `sys`
- `collections`
- `datetime`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that annotations work properly with concatenated edges.'

```python
'Test that annotations work properly with concatenated edges.'
```

**Verification:**
```python
assert raw.annotations is not None
```

### Step 2: Assign data = np.ones(...)

```python
data = np.ones((1, 1000))
```

**Verification:**
```python
assert len(raw.annotations) == 4
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(1, 1000.0, 'eeg')
```

**Verification:**
```python
assert np.isin(raw.annotations.description, ['BAD boundary']).sum() == 2
```

### Step 4: Assign raw = concatenate_raws(...)

```python
raw = concatenate_raws([RawArray(data, info) for ii in range(3)])
```

**Verification:**
```python
assert np.isin(raw.annotations.description, ['EDGE boundary']).sum() == 2
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.duration, 0.0)
```

**Verification:**
```python
assert_array_equal(raw.annotations.duration, 0.0)
```

### Step 6: Assign events = np.array(...)

```python
events = np.array([[a, 0, 1] for a in [0, 500, 1000, 1500, 2000]])
```

**Verification:**
```python
assert_equal(len(epochs.drop_log), len(events))
```

### Step 7: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, tmin=0, tmax=0.999, baseline=None, preload=True)
```

**Verification:**
```python
assert_equal(len(epochs), 3)
```

### Step 8: Call assert_equal()

```python
assert_equal(len(epochs.drop_log), len(events))
```

**Verification:**
```python
assert_equal([0, 2, 4], epochs.selection)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(epochs), 3)
```

### Step 10: Call assert_equal()

```python
assert_equal([0, 2, 4], epochs.selection)
```


## Complete Example

```python
# Workflow
'Test that annotations work properly with concatenated edges.'
data = np.ones((1, 1000))
info = create_info(1, 1000.0, 'eeg')
raw = concatenate_raws([RawArray(data, info) for ii in range(3)])
assert raw.annotations is not None
assert len(raw.annotations) == 4
assert np.isin(raw.annotations.description, ['BAD boundary']).sum() == 2
assert np.isin(raw.annotations.description, ['EDGE boundary']).sum() == 2
assert_array_equal(raw.annotations.duration, 0.0)
events = np.array([[a, 0, 1] for a in [0, 500, 1000, 1500, 2000]])
epochs = Epochs(raw, events, tmin=0, tmax=0.999, baseline=None, preload=True)
assert_equal(len(epochs.drop_log), len(events))
assert_equal(len(epochs), 3)
assert_equal([0, 2, 4], epochs.selection)
```

## Next Steps


---

*Source: test_annotations.py:616 | Complexity: Advanced | Last updated: 2026-05-18*