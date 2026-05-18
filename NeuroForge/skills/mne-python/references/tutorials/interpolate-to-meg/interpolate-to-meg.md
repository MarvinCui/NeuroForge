# How To: Interpolate To Meg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test interpolation_to for MEG data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.channels`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne.channels`
- `mne.channels.interpolation`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.utils`
- `mne.channels.interpolation`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test interpolation_to for MEG data.'

```python
'Test interpolation_to for MEG data.'
```

**Verification:**
```python
assert len(evoked.ch_names) == 100
```

### Step 2: Assign evoked = unknown.average(...)

```python
evoked = _load_data('meg')[1].average()
```

**Verification:**
```python
assert 'MEG 0112' in evoked.ch_names
```

### Step 3: Call evoked.pick()

```python
evoked.pick(evoked.ch_names[::4])
```

**Verification:**
```python
assert evoked_ctf.info['sfreq'] == evoked.info['sfreq']
```

### Step 4: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne.channels.channels, '_ALLOWED_INTERPOLATION_MODES', ('point',))
```

**Verification:**
```python
assert 0.9 < corrcoef < 0.92
```

### Step 5: Call evoked.resample()

```python
evoked.resample(evoked.info['sfreq'] / 2)
```

### Step 6: Assign kwargs = dict(...)

```python
kwargs = dict(mode='point', origin=(0.0, 0.0, 0.04))
```

### Step 7: Assign evoked_ctf = evoked.interpolate_to(...)

```python
evoked_ctf = evoked.interpolate_to('ctf151', **kwargs)
```

**Verification:**
```python
assert evoked_ctf.info['sfreq'] == evoked.info['sfreq']
```

### Step 8: Call evoked_ctf.pick()

```python
evoked_ctf.pick(evoked_ctf.ch_names[::4])
```

### Step 9: Assign evoked_rt = evoked_ctf.interpolate_to.pick(...)

```python
evoked_rt = evoked_ctf.interpolate_to('neuromag', **kwargs).pick(evoked.ch_names)
```

### Step 10: Assign corrcoef = value

```python
corrcoef = np.corrcoef(evoked.data.ravel(), evoked_rt.data.ravel())[0, 1]
```

**Verification:**
```python
assert 0.9 < corrcoef < 0.92
```

### Step 11: Assign unknown = value

```python
evoked_rt.info['bads'] = evoked_rt.ch_names
```

### Step 12: Call evoked_rt.interpolate_to()

```python
evoked_rt.interpolate_to('ctf151', **kwargs)
```

### Step 13: Call evoked_rt.interpolate_to()

```python
evoked_rt.interpolate_to('foo', **kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
'Test interpolation_to for MEG data.'
evoked = _load_data('meg')[1].average()
assert len(evoked.ch_names) == 100
evoked.pick(evoked.ch_names[::4])
assert 'MEG 0112' in evoked.ch_names
monkeypatch.setattr(mne.channels.channels, '_ALLOWED_INTERPOLATION_MODES', ('point',))
evoked.resample(evoked.info['sfreq'] / 2)
kwargs = dict(mode='point', origin=(0.0, 0.0, 0.04))
evoked_ctf = evoked.interpolate_to('ctf151', **kwargs)
assert evoked_ctf.info['sfreq'] == evoked.info['sfreq']
evoked_ctf.pick(evoked_ctf.ch_names[::4])
evoked_rt = evoked_ctf.interpolate_to('neuromag', **kwargs).pick(evoked.ch_names)
corrcoef = np.corrcoef(evoked.data.ravel(), evoked_rt.data.ravel())[0, 1]
assert 0.9 < corrcoef < 0.92
evoked_rt.info['bads'] = evoked_rt.ch_names
with pytest.raises(ValueError, match='No good MEG'):
    evoked_rt.interpolate_to('ctf151', **kwargs)
with pytest.raises(ValueError, match='Invalid value'):
    evoked_rt.interpolate_to('foo', **kwargs)
```

## Next Steps


---

*Source: test_interpolation.py:588 | Complexity: Advanced | Last updated: 2026-05-18*