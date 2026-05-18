# How To: Plot Montage Scale

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test montage.plot with non-default scale using subplot axes.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.channels`
- `mne.io`


## Step-by-Step Guide

### Step 1: 'Test montage.plot with non-default scale using subplot axes.'

```python
'Test montage.plot with non-default scale using subplot axes.'
```

### Step 2: Assign montage = make_standard_montage(...)

```python
montage = make_standard_montage('GSN-HydroCel-129')
```

### Step 3: Assign ax = value

```python
ax = plt.subplots(2, 1)[1][1]
```

### Step 4: Assign picks = value

```python
picks = montage.ch_names
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(montage.ch_names, sfreq=256, ch_types='eeg')
```

### Step 6: Assign raw = RawArray.set_montage(...)

```python
raw = RawArray(np.zeros((len(montage.ch_names), 1)), info, copy=None, verbose=False).set_montage(montage)
```

### Step 7: Call raw.pick.get_montage.plot()

```python
raw.pick(picks).get_montage().plot(axes=ax, show_names=False, scale=0.1)
```


## Complete Example

```python
# Workflow
'Test montage.plot with non-default scale using subplot axes.'
montage = make_standard_montage('GSN-HydroCel-129')
ax = plt.subplots(2, 1)[1][1]
picks = montage.ch_names
info = create_info(montage.ch_names, sfreq=256, ch_types='eeg')
raw = RawArray(np.zeros((len(montage.ch_names), 1)), info, copy=None, verbose=False).set_montage(montage)
raw.pick(picks).get_montage().plot(axes=ax, show_names=False, scale=0.1)
```

## Next Steps


---

*Source: test_montage.py:93 | Complexity: Intermediate | Last updated: 2026-05-18*