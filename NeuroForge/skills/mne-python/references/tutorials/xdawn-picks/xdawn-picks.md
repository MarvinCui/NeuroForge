# How To: Xdawn Picks

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test picking with Xdawn.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.fixes`
- `mne.io`
- `mne.decoding.xdawn`
- `mne.preprocessing.xdawn`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `mne.decoding`


## Step-by-Step Guide

### Step 1: 'Test picking with Xdawn.'

```python
'Test picking with Xdawn.'
```

**Verification:**
```python
assert epochs_out.info['ch_names'] == epochs.ch_names
```

### Step 2: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(10, 2, 10)
```

**Verification:**
```python
assert not (epochs_out.get_data([0])[:, 0] != data[:, 0]).any()
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(2, 1000.0, ('eeg', 'misc'))
```

**Verification:**
```python
assert_array_equal(epochs_out.get_data([1])[:, 0], data[:, 1])
```

### Step 4: Assign epochs = EpochsArray(...)

```python
epochs = EpochsArray(data, info)
```

### Step 5: Assign xd = Xdawn(...)

```python
xd = Xdawn(correct_overlap=False)
```

### Step 6: Call xd.fit()

```python
xd.fit(epochs)
```

### Step 7: Assign epochs_out = value

```python
epochs_out = xd.apply(epochs)['1']
```

**Verification:**
```python
assert epochs_out.info['ch_names'] == epochs.ch_names
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(epochs_out.get_data([1])[:, 0], data[:, 1])
```


## Complete Example

```python
# Workflow
'Test picking with Xdawn.'
data = np.random.RandomState(0).randn(10, 2, 10)
info = create_info(2, 1000.0, ('eeg', 'misc'))
epochs = EpochsArray(data, info)
xd = Xdawn(correct_overlap=False)
xd.fit(epochs)
epochs_out = xd.apply(epochs)['1']
assert epochs_out.info['ch_names'] == epochs.ch_names
assert not (epochs_out.get_data([0])[:, 0] != data[:, 0]).any()
assert_array_equal(epochs_out.get_data([1])[:, 0], data[:, 1])
```

## Next Steps


---

*Source: test_xdawn.py:55 | Complexity: Advanced | Last updated: 2026-05-18*