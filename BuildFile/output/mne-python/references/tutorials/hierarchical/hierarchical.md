# How To: Hierarchical

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test hierarchical access.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `datetime`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `scipy.signal`
- `numpy.fft`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne._fiff.write`
- `mne.annotations`
- `mne.baseline`
- `mne.chpi`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas`


## Step-by-Step Guide

### Step 1: 'Test hierarchical access.'

```python
'Test hierarchical access.'
```

**Verification:**
```python
assert_equal(len(epochs_a), len(epochs_a1) + len(epochs_a2))
```

### Step 2: Assign unknown = _get_data(...)

```python
raw, events, picks = _get_data()
```

**Verification:**
```python
assert_equal(len(epochs_b), len(epochs_b1) + len(epochs_b2))
```

### Step 3: Assign event_id = value

```python
event_id = {'a/1': 1, 'a/2': 2, 'b/1': 3, 'b/2': 4}
```

**Verification:**
```python
assert_equal(len(epochs_1), len(epochs_a1) + len(epochs_b1))
```

### Step 4: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, preload=True)
```

**Verification:**
```python
assert_equal(len(epochs_2), len(epochs_a2) + len(epochs_b2))
```

### Step 5: Assign epochs_a1 = value

```python
epochs_a1 = epochs['a/1']
```

**Verification:**
```python
assert_equal(len(epochs), len(epochs_all))
```

### Step 6: Assign epochs_a2 = value

```python
epochs_a2 = epochs['a/2']
```

**Verification:**
```python
assert_array_equal(epochs.get_data(), epochs_all.get_data())
```

### Step 7: Assign epochs_b1 = value

```python
epochs_b1 = epochs['b/1']
```

### Step 8: Assign epochs_b2 = value

```python
epochs_b2 = epochs['b/2']
```

### Step 9: Assign epochs_a = value

```python
epochs_a = epochs['a']
```

### Step 10: Call assert_equal()

```python
assert_equal(len(epochs_a), len(epochs_a1) + len(epochs_a2))
```

### Step 11: Assign epochs_b = value

```python
epochs_b = epochs['b']
```

### Step 12: Call assert_equal()

```python
assert_equal(len(epochs_b), len(epochs_b1) + len(epochs_b2))
```

### Step 13: Assign epochs_1 = value

```python
epochs_1 = epochs['1']
```

### Step 14: Call assert_equal()

```python
assert_equal(len(epochs_1), len(epochs_a1) + len(epochs_b1))
```

### Step 15: Assign epochs_2 = value

```python
epochs_2 = epochs['2']
```

### Step 16: Call assert_equal()

```python
assert_equal(len(epochs_2), len(epochs_a2) + len(epochs_b2))
```

### Step 17: Assign epochs_all = value

```python
epochs_all = epochs['1', '2']
```

### Step 18: Call assert_equal()

```python
assert_equal(len(epochs), len(epochs_all))
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(epochs.get_data(), epochs_all.get_data())
```


## Complete Example

```python
# Workflow
'Test hierarchical access.'
raw, events, picks = _get_data()
event_id = {'a/1': 1, 'a/2': 2, 'b/1': 3, 'b/2': 4}
epochs = Epochs(raw, events, event_id, preload=True)
epochs_a1 = epochs['a/1']
epochs_a2 = epochs['a/2']
epochs_b1 = epochs['b/1']
epochs_b2 = epochs['b/2']
epochs_a = epochs['a']
assert_equal(len(epochs_a), len(epochs_a1) + len(epochs_a2))
epochs_b = epochs['b']
assert_equal(len(epochs_b), len(epochs_b1) + len(epochs_b2))
epochs_1 = epochs['1']
assert_equal(len(epochs_1), len(epochs_a1) + len(epochs_b1))
epochs_2 = epochs['2']
assert_equal(len(epochs_2), len(epochs_a2) + len(epochs_b2))
epochs_all = epochs['1', '2']
assert_equal(len(epochs), len(epochs_all))
assert_array_equal(epochs.get_data(), epochs_all.get_data())
```

## Next Steps


---

*Source: test_epochs.py:342 | Complexity: Advanced | Last updated: 2026-05-18*