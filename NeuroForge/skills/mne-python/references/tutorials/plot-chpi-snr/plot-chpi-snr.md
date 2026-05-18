# How To: Plot Chpi Snr

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting cHPI SNRs.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.chpi`
- `mne.datasets`
- `mne.filter`
- `mne.io`
- `mne.minimum_norm`
- `mne.time_frequency`
- `mne.utils`
- `mne.viz`
- `mne.viz.misc`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test plotting cHPI SNRs.'

```python
'Test plotting cHPI SNRs.'
```

**Verification:**
```python
assert len(fig.axes) == len(result) - 2
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
```

**Verification:**
```python
assert len(fig.axes[0].lines) == len(result['freqs'])
```

### Step 3: Assign result = compute_chpi_snr(...)

```python
result = compute_chpi_snr(raw)
```

**Verification:**
```python
assert len(fig.legends) == 1
```

### Step 4: Assign fig = plot_chpi_snr(...)

```python
fig = plot_chpi_snr(result)
```

**Verification:**
```python
assert len(texts) == len(result['freqs'])
```

### Step 5: Assign texts = value

```python
texts = [entry.get_text() for entry in fig.legends[0].get_texts()]
```

**Verification:**
```python
assert_array_equal(freqs, result['freqs'])
```

### Step 6: Assign freqs = value

```python
freqs = [float(text.split()[0]) for text in texts]
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(freqs, result['freqs'])
```

### Step 8: Assign unknown = plt.subplots(...)

```python
_, axs = plt.subplots(2, 3)
```

### Step 9: Assign _ = plot_chpi_snr(...)

```python
_ = plot_chpi_snr(result, axes=axs.ravel())
```

### Step 10: Assign unknown = plt.subplots(...)

```python
_, axs = plt.subplots(5)
```

### Step 11: Assign _ = plot_chpi_snr(...)

```python
_ = plot_chpi_snr(result, axes=axs.ravel())
```


## Complete Example

```python
# Workflow
'Test plotting cHPI SNRs.'
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
result = compute_chpi_snr(raw)
fig = plot_chpi_snr(result)
assert len(fig.axes) == len(result) - 2
assert len(fig.axes[0].lines) == len(result['freqs'])
assert len(fig.legends) == 1
texts = [entry.get_text() for entry in fig.legends[0].get_texts()]
assert len(texts) == len(result['freqs'])
freqs = [float(text.split()[0]) for text in texts]
assert_array_equal(freqs, result['freqs'])
_, axs = plt.subplots(2, 3)
_ = plot_chpi_snr(result, axes=axs.ravel())
_, axs = plt.subplots(5)
with pytest.raises(ValueError, match='a list of 6 axes, got length 5'):
    _ = plot_chpi_snr(result, axes=axs.ravel())
```

## Next Steps


---

*Source: test_misc.py:371 | Complexity: Advanced | Last updated: 2026-05-18*