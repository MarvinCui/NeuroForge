# How To: Invalid Arguments

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test error messages raised by invalid arguments.

## Prerequisites

**Required Modules:**
- `datetime`
- `itertools`
- `re`
- `pathlib`
- `numpy`
- `pytest`
- `mne`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`


## Step-by-Step Guide

### Step 1: 'Test error messages raised by invalid arguments.'

```python
'Test error messages raised by invalid arguments.'
```

### Step 2: Assign unknown = value

```python
n_ch, n_times = (2, 100)
```

### Step 3: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(n_ch, n_times)
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(n_ch, 100.0, 'eeg')
```

### Step 5: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, first_samp=0)
```

### Step 6: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=None, flat=-1)
```

### Step 7: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=-1, flat=None)
```

### Step 8: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=None, flat=dict(eeg=1, eog=-1))
```

### Step 9: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=dict(eeg=1, eog=-1), flat=None)
```

### Step 10: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=None, flat=None)
```

### Step 11: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=dict(eeg=1), flat=None, bad_percent=-1)
```

### Step 12: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=dict(eeg=1), flat=None, min_duration=-1)
```

### Step 13: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=dict(eeg=1), flat=None, min_duration=1.0)
```

### Step 14: Call annotate_amplitude()

```python
annotate_amplitude(raw, peak=dict(eeg=1), flat=None, min_duration=10)
```


## Complete Example

```python
# Workflow
'Test error messages raised by invalid arguments.'
n_ch, n_times = (2, 100)
data = np.random.RandomState(0).randn(n_ch, n_times)
info = create_info(n_ch, 100.0, 'eeg')
raw = RawArray(data, info, first_samp=0)
with pytest.raises(ValueError, match="Argument 'flat' should define a positive threshold. Provided: '-1'."):
    annotate_amplitude(raw, peak=None, flat=-1)
with pytest.raises(ValueError, match="Argument 'peak' should define a positive threshold. Provided: '-1'."):
    annotate_amplitude(raw, peak=-1, flat=None)
with pytest.raises(ValueError, match="Argument 'flat' should define positive thresholds. Provided for channel type 'eog': '-1'."):
    annotate_amplitude(raw, peak=None, flat=dict(eeg=1, eog=-1))
with pytest.raises(ValueError, match="Argument 'peak' should define positive thresholds. Provided for channel type 'eog': '-1'."):
    annotate_amplitude(raw, peak=dict(eeg=1, eog=-1), flat=None)
with pytest.raises(ValueError, match="At least one of the arguments 'peak' or 'flat' must not be None."):
    annotate_amplitude(raw, peak=None, flat=None)
with pytest.raises(ValueError, match="Argument 'bad_percent' should define a percentage between 0% and 100%. Provided: -1.0%."):
    annotate_amplitude(raw, peak=dict(eeg=1), flat=None, bad_percent=-1)
with pytest.raises(ValueError, match="Argument 'min_duration' should define a positive duration in seconds. Provided: '-1.0' seconds."):
    annotate_amplitude(raw, peak=dict(eeg=1), flat=None, min_duration=-1)
with pytest.raises(ValueError, match=re.escape("Argument 'min_duration' should define a positive duration in seconds shorter than the raw duration (1.0 seconds). Provided: '1.0' seconds.")):
    annotate_amplitude(raw, peak=dict(eeg=1), flat=None, min_duration=1.0)
with pytest.raises(ValueError, match=re.escape("Argument 'min_duration' should define a positive duration in seconds shorter than the raw duration (1.0 seconds). Provided: '10.0' seconds.")):
    annotate_amplitude(raw, peak=dict(eeg=1), flat=None, min_duration=10)
```

## Next Steps


---

*Source: test_annotate_amplitude.py:315 | Complexity: Advanced | Last updated: 2026-05-18*