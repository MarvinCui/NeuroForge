# How To: Db Computation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test dB computation in plot methods (gh 11091).

## Prerequisites

**Required Modules:**
- `datetime`
- `re`
- `itertools`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.collections`
- `numpy.testing`
- `mne`
- `mne`
- `mne.epochs`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz.utils`
- `test_spectrum`
- `pandas.testing`


## Step-by-Step Guide

### Step 1: 'Test dB computation in plot methods (gh 11091).'

```python
'Test dB computation in plot methods (gh 11091).'
```

**Verification:**
```python
assert_array_equal(quadmesh1._mapped_colors, quadmesh2._mapped_colors)
```

### Step 2: Assign ampl = 2.0

```python
ampl = 2.0
```

### Step 3: Assign data = np.full(...)

```python
data = np.full((3, 2, 3), ampl ** 2)
```

### Step 4: Assign complex_data = np.full(...)

```python
complex_data = np.full((3, 2, 3), ampl + 0j)
```

### Step 5: Assign times = np.array(...)

```python
times = np.array([0.1, 0.2, 0.3])
```

### Step 6: Assign freqs = np.array(...)

```python
freqs = np.array([0.1, 0.2])
```

### Step 7: Assign info = mne.create_info(...)

```python
info = mne.create_info(['MEG 001', 'MEG 002', 'MEG 003'], 1000.0, ['mag', 'mag', 'mag'])
```

### Step 8: Assign kwargs = dict(...)

```python
kwargs = dict(times=times, freqs=freqs, nave=20, comment='test', method='crazy-tfr')
```

### Step 9: Assign tfr = AverageTFRArray(...)

```python
tfr = AverageTFRArray(info=info, data=data, **kwargs)
```

### Step 10: Assign complex_tfr = AverageTFRArray(...)

```python
complex_tfr = AverageTFRArray(info=info, data=complex_data, **kwargs)
```

### Step 11: Assign plot_kwargs = dict(...)

```python
plot_kwargs = dict(dB=True, combine='mean', vlim=(0, 7))
```

### Step 12: Assign fig1 = value

```python
fig1 = tfr.plot(**plot_kwargs)[0]
```

### Step 13: Assign fig2 = value

```python
fig2 = complex_tfr.plot(**plot_kwargs)[0]
```

### Step 14: Assign quadmesh1 = value

```python
quadmesh1 = fig1.axes[0].collections[0]
```

### Step 15: Assign quadmesh2 = value

```python
quadmesh2 = fig2.axes[0].collections[0]
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(quadmesh1._mapped_colors, quadmesh2._mapped_colors)
```


## Complete Example

```python
# Workflow
'Test dB computation in plot methods (gh 11091).'
ampl = 2.0
data = np.full((3, 2, 3), ampl ** 2)
complex_data = np.full((3, 2, 3), ampl + 0j)
times = np.array([0.1, 0.2, 0.3])
freqs = np.array([0.1, 0.2])
info = mne.create_info(['MEG 001', 'MEG 002', 'MEG 003'], 1000.0, ['mag', 'mag', 'mag'])
kwargs = dict(times=times, freqs=freqs, nave=20, comment='test', method='crazy-tfr')
tfr = AverageTFRArray(info=info, data=data, **kwargs)
complex_tfr = AverageTFRArray(info=info, data=complex_data, **kwargs)
plot_kwargs = dict(dB=True, combine='mean', vlim=(0, 7))
fig1 = tfr.plot(**plot_kwargs)[0]
fig2 = complex_tfr.plot(**plot_kwargs)[0]
quadmesh1 = fig1.axes[0].collections[0]
quadmesh2 = fig2.axes[0].collections[0]
if hasattr(quadmesh1, '_mapped_colors'):
    assert_array_equal(quadmesh1._mapped_colors, quadmesh2._mapped_colors)
```

## Next Steps


---

*Source: test_tfr.py:819 | Complexity: Advanced | Last updated: 2026-05-18*