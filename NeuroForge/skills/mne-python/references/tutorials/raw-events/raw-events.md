# How To: Raw Events

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test creating stim channel from raw SQD file.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.kit.constants`
- `mne.io.kit.coreg`
- `mne.io.kit.kit`
- `mne.io.tests.test_raw`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test creating stim channel from raw SQD file.'

```python
'Test creating stim channel from raw SQD file.'
```

**Verification:**
```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(255, 254, 255, 254, 255, 0))
```

### Step 2: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(sqd_path)
```

**Verification:**
```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 1, 0, 1, 0))
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(255, 254, 255, 254, 255, 0))
```

**Verification:**
```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 128, 0, 128, 0))
```

### Step 4: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(sqd_path, slope='+')
```

**Verification:**
```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 160, 0, 160, 0))
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 1, 0, 1, 0))
```

**Verification:**
```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 160, 0, 160, 0))
```

### Step 6: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(sqd_path, stim='<', slope='+')
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 128, 0, 128, 0))
```

### Step 8: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(sqd_path, stim='<', slope='+', stim_code='channel')
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 160, 0, 160, 0))
```

### Step 10: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(sqd_path, stim=range(160, 162), slope='+', stim_code='channel')
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 160, 0, 160, 0))
```

### Step 12: Assign out = value

```python
out = [[269, a, b], [281, b, c], [1552, c, d], [1564, d, e]]
```

### Step 13: Call out.append()

```python
out.append([2000, e, f])
```


## Complete Example

```python
# Workflow
'Test creating stim channel from raw SQD file.'

def evts(a, b, c, d, e, f=None):
    out = [[269, a, b], [281, b, c], [1552, c, d], [1564, d, e]]
    if f is not None:
        out.append([2000, e, f])
    return out
raw = read_raw_kit(sqd_path)
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(255, 254, 255, 254, 255, 0))
raw = read_raw_kit(sqd_path, slope='+')
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 1, 0, 1, 0))
raw = read_raw_kit(sqd_path, stim='<', slope='+')
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 128, 0, 128, 0))
raw = read_raw_kit(sqd_path, stim='<', slope='+', stim_code='channel')
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 160, 0, 160, 0))
raw = read_raw_kit(sqd_path, stim=range(160, 162), slope='+', stim_code='channel')
assert_array_equal(find_events(raw, output='step', consecutive=True), evts(0, 160, 0, 160, 0))
```

## Next Steps


---

*Source: test_kit.py:295 | Complexity: Advanced | Last updated: 2026-05-18*