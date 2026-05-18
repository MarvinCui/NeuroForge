# How To: Evoked Detrend

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test for detrending evoked data.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.evoked`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test for detrending evoked data.'

```python
'Test for detrending evoked data.'
```

**Verification:**
```python
assert_allclose(ave.data[picks], ave_normal.data[picks], rtol=1e-08, atol=1e-16)
```

### Step 2: Assign ave = read_evokeds(...)

```python
ave = read_evokeds(fname, 0)
```

### Step 3: Assign ave_normal = read_evokeds(...)

```python
ave_normal = read_evokeds(fname, 0)
```

### Step 4: Call ave.detrend()

```python
ave.detrend(0)
```

### Step 5: Assign picks = pick_types(...)

```python
picks = pick_types(ave.info, meg=True, eeg=True, exclude='bads')
```

### Step 6: Call assert_allclose()

```python
assert_allclose(ave.data[picks], ave_normal.data[picks], rtol=1e-08, atol=1e-16)
```


## Complete Example

```python
# Workflow
'Test for detrending evoked data.'
ave = read_evokeds(fname, 0)
ave_normal = read_evokeds(fname, 0)
ave.detrend(0)
ave_normal.data -= np.mean(ave_normal.data, axis=1)[:, np.newaxis]
picks = pick_types(ave.info, meg=True, eeg=True, exclude='bads')
assert_allclose(ave.data[picks], ave_normal.data[picks], rtol=1e-08, atol=1e-16)
```

## Next Steps


---

*Source: test_evoked.py:439 | Complexity: Intermediate | Last updated: 2026-05-18*