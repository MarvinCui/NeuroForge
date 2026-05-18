# How To: Plot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test TFR plotting.

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

### Step 1: 'Test TFR plotting.'

```python
'Test TFR plotting.'
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((3, 2, 3))
```

### Step 3: Assign times = np.array(...)

```python
times = np.array([0.1, 0.2, 0.3])
```

### Step 4: Assign freqs = np.array(...)

```python
freqs = np.array([0.1, 0.2])
```

### Step 5: Assign info = mne.create_info(...)

```python
info = mne.create_info(['MEG 001', 'MEG 002', 'MEG 003'], 1000.0, ['mag', 'mag', 'mag'])
```

### Step 6: Assign tfr = AverageTFRArray(...)

```python
tfr = AverageTFRArray(info=info, data=data, times=times, freqs=freqs, nave=20, comment='test', method='crazy-tfr')
```

### Step 7: Assign fig = value

```python
fig = tfr.plot(picks=[1], cmap='RdBu_r')[0]
```

### Step 8: Call _fake_keypress()

```python
_fake_keypress(fig, 'up')
```

### Step 9: Call _fake_keypress()

```python
_fake_keypress(fig, ' ')
```

### Step 10: Call _fake_keypress()

```python
_fake_keypress(fig, 'down')
```

### Step 11: Call _fake_keypress()

```python
_fake_keypress(fig, ' ')
```

### Step 12: Call _fake_keypress()

```python
_fake_keypress(fig, '+')
```

### Step 13: Call _fake_keypress()

```python
_fake_keypress(fig, ' ')
```

### Step 14: Call _fake_keypress()

```python
_fake_keypress(fig, '-')
```

### Step 15: Call _fake_keypress()

```python
_fake_keypress(fig, ' ')
```

### Step 16: Call _fake_keypress()

```python
_fake_keypress(fig, 'pageup')
```

### Step 17: Call _fake_keypress()

```python
_fake_keypress(fig, ' ')
```

### Step 18: Call _fake_keypress()

```python
_fake_keypress(fig, 'pagedown')
```

### Step 19: Assign cbar = value

```python
cbar = fig.get_axes()[0].CB
```

### Step 20: Assign ax = value

```python
ax = cbar.cbar.ax
```

### Step 21: Call _fake_click()

```python
_fake_click(fig, ax, (0.1, 0.1))
```

### Step 22: Call _fake_click()

```python
_fake_click(fig, ax, (0.1, 0.2), kind='motion')
```

### Step 23: Call _fake_click()

```python
_fake_click(fig, ax, (0.1, 0.3), kind='release')
```

### Step 24: Call _fake_click()

```python
_fake_click(fig, ax, (0.1, 0.1), button=3)
```

### Step 25: Call _fake_click()

```python
_fake_click(fig, ax, (0.1, 0.2), button=3, kind='motion')
```

### Step 26: Call _fake_click()

```python
_fake_click(fig, ax, (0.1, 0.3), kind='release')
```

### Step 27: Call _fake_scroll()

```python
_fake_scroll(fig, 0.5, 0.5, -0.5)
```

### Step 28: Call _fake_scroll()

```python
_fake_scroll(fig, 0.5, 0.5, 0.5)
```

### Step 29: Call plt.close()

```python
plt.close('all')
```


## Complete Example

```python
# Workflow
'Test TFR plotting.'
data = np.zeros((3, 2, 3))
times = np.array([0.1, 0.2, 0.3])
freqs = np.array([0.1, 0.2])
info = mne.create_info(['MEG 001', 'MEG 002', 'MEG 003'], 1000.0, ['mag', 'mag', 'mag'])
tfr = AverageTFRArray(info=info, data=data, times=times, freqs=freqs, nave=20, comment='test', method='crazy-tfr')
fig = tfr.plot(picks=[1], cmap='RdBu_r')[0]
_fake_keypress(fig, 'up')
_fake_keypress(fig, ' ')
_fake_keypress(fig, 'down')
_fake_keypress(fig, ' ')
_fake_keypress(fig, '+')
_fake_keypress(fig, ' ')
_fake_keypress(fig, '-')
_fake_keypress(fig, ' ')
_fake_keypress(fig, 'pageup')
_fake_keypress(fig, ' ')
_fake_keypress(fig, 'pagedown')
cbar = fig.get_axes()[0].CB
ax = cbar.cbar.ax
_fake_click(fig, ax, (0.1, 0.1))
_fake_click(fig, ax, (0.1, 0.2), kind='motion')
_fake_click(fig, ax, (0.1, 0.3), kind='release')
_fake_click(fig, ax, (0.1, 0.1), button=3)
_fake_click(fig, ax, (0.1, 0.2), button=3, kind='motion')
_fake_click(fig, ax, (0.1, 0.3), kind='release')
_fake_scroll(fig, 0.5, 0.5, -0.5)
_fake_scroll(fig, 0.5, 0.5, 0.5)
plt.close('all')
```

## Next Steps


---

*Source: test_tfr.py:842 | Complexity: Advanced | Last updated: 2026-05-18*