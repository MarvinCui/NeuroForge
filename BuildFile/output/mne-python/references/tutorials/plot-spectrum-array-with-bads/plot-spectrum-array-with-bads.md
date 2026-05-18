# How To: Plot Spectrum Array With Bads

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting a spectrum array with bads.

## Prerequisites

**Required Modules:**
- `datetime`
- `re`
- `functools`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.spectrum`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas.testing`
- `mne.utils.dataframe`
- `matplotlib.pyplot`


## Step-by-Step Guide

### Step 1: 'Test plotting a spectrum array with bads.'

```python
'Test plotting a spectrum array with bads.'
```

### Step 2: Assign raw = RawArray(...)

```python
raw = RawArray(np.random.randn(3, 1000), create_info(3, 1000, 'eeg'))
```

### Step 3: Assign unknown = value

```python
raw.info['bads'] = [raw.ch_names[1]]
```

### Step 4: Assign spectrum = raw.compute_psd(...)

```python
spectrum = raw.compute_psd()
```

### Step 5: Assign spectrum2 = SpectrumArray(...)

```python
spectrum2 = SpectrumArray(spectrum.get_data(exclude=()), spectrum.info, spectrum.freqs)
```

### Step 6: Call spectrum2.plot()

```python
spectrum2.plot(spatial_colors=False)
```

### Step 7: Call SpectrumArray()

```python
SpectrumArray(spectrum.get_data(), spectrum.info, spectrum.freqs)
```


## Complete Example

```python
# Workflow
'Test plotting a spectrum array with bads.'
raw = RawArray(np.random.randn(3, 1000), create_info(3, 1000, 'eeg'))
raw.info['bads'] = [raw.ch_names[1]]
spectrum = raw.compute_psd()
with pytest.raises(ValueError, match=re.escape('number of good + bad data channels')):
    SpectrumArray(spectrum.get_data(), spectrum.info, spectrum.freqs)
spectrum2 = SpectrumArray(spectrum.get_data(exclude=()), spectrum.info, spectrum.freqs)
spectrum2.plot(spatial_colors=False)
```

## Next Steps


---

*Source: test_spectrum.py:724 | Complexity: Intermediate | Last updated: 2026-05-18*