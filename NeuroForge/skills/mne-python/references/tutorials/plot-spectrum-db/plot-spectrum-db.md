# How To: Plot Spectrum Db

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that we properly handle amplitude/power and dB.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: raw_spectrum, dB, amplitude
```

## Step-by-Step Guide

### Step 1: 'Test that we properly handle amplitude/power and dB.'

```python
'Test that we properly handle amplitude/power and dB.'
```

**Verification:**
```python
assert want == got, f'expected {want}, got {got}'
```

### Step 2: Assign idx = 7

```python
idx = 7
```

### Step 3: Assign power = 3

```python
power = 3
```

### Step 4: Assign freqs = np.linspace(...)

```python
freqs = np.linspace(1, 100, 100)
```

### Step 5: Assign data = np.full(...)

```python
data = np.full((1, freqs.size), np.finfo(float).tiny)
```

### Step 6: Assign unknown = power

```python
data[0, idx] = power
```

### Step 7: Assign info = create_info(...)

```python
info = create_info(ch_names=['delta'], sfreq=1000, ch_types='eeg')
```

### Step 8: Assign psd = SpectrumArray(...)

```python
psd = SpectrumArray(data=data, info=info, freqs=freqs)
```

### Step 9: Assign trace = value

```python
trace = list(filter(lambda x: len(x.get_data()[0]) == len(freqs), fig.axes[0].lines))[0]
```

### Step 10: Assign got = value

```python
got = trace.get_data()[1][idx]
```

### Step 11: Assign want = value

```python
want = power * 1000000000000.0
```

**Verification:**
```python
assert want == got, f'expected {want}, got {got}'
```

### Step 12: Assign fig = psd.plot(...)

```python
fig = psd.plot(dB=dB, amplitude=amplitude)
```

### Step 13: Assign want = np.sqrt(...)

```python
want = np.sqrt(want)
```

### Step 14: Assign want = value

```python
want = (20 if amplitude else 10) * np.log10(want)
```


## Complete Example

```python
# Setup
# Fixtures: raw_spectrum, dB, amplitude

# Workflow
'Test that we properly handle amplitude/power and dB.'
idx = 7
power = 3
freqs = np.linspace(1, 100, 100)
data = np.full((1, freqs.size), np.finfo(float).tiny)
data[0, idx] = power
info = create_info(ch_names=['delta'], sfreq=1000, ch_types='eeg')
psd = SpectrumArray(data=data, info=info, freqs=freqs)
with pytest.warns(RuntimeWarning, match='Channel locations not available'):
    fig = psd.plot(dB=dB, amplitude=amplitude)
trace = list(filter(lambda x: len(x.get_data()[0]) == len(freqs), fig.axes[0].lines))[0]
got = trace.get_data()[1][idx]
want = power * 1000000000000.0
if amplitude:
    want = np.sqrt(want)
if dB:
    want = (20 if amplitude else 10) * np.log10(want)
assert want == got, f'expected {want}, got {got}'
```

## Next Steps


---

*Source: test_spectrum.py:741 | Complexity: Advanced | Last updated: 2026-05-18*