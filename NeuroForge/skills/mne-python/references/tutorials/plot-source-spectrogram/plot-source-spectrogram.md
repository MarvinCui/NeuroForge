# How To: Plot Source Spectrogram

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting of source spectrogram.

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

### Step 1: 'Test plotting of source spectrogram.'

```python
'Test plotting of source spectrogram.'
```

### Step 2: Assign sample_src = read_source_spaces(...)

```python
sample_src = read_source_spaces(subjects_dir / 'sample' / 'bem' / 'sample-oct-6-src.fif')
```

### Step 3: Assign vertices = value

```python
vertices = [s['vertno'] for s in sample_src]
```

### Step 4: Assign n_times = 5

```python
n_times = 5
```

### Step 5: Assign n_verts = sum(...)

```python
n_verts = sum((len(v) for v in vertices))
```

### Step 6: Assign stc_data = np.ones(...)

```python
stc_data = np.ones((n_verts, n_times))
```

### Step 7: Assign stc = SourceEstimate(...)

```python
stc = SourceEstimate(stc_data, vertices, 1, 1)
```

### Step 8: Call plot_source_spectrogram()

```python
plot_source_spectrogram([stc, stc], [[1, 2], [3, 4]])
```

### Step 9: Call pytest.raises()

```python
pytest.raises(ValueError, plot_source_spectrogram, [], [])
```

### Step 10: Call pytest.raises()

```python
pytest.raises(ValueError, plot_source_spectrogram, [stc, stc], [[1, 2], [3, 4]], tmin=0)
```

### Step 11: Call pytest.raises()

```python
pytest.raises(ValueError, plot_source_spectrogram, [stc, stc], [[1, 2], [3, 4]], tmax=7)
```


## Complete Example

```python
# Workflow
'Test plotting of source spectrogram.'
sample_src = read_source_spaces(subjects_dir / 'sample' / 'bem' / 'sample-oct-6-src.fif')
vertices = [s['vertno'] for s in sample_src]
n_times = 5
n_verts = sum((len(v) for v in vertices))
stc_data = np.ones((n_verts, n_times))
stc = SourceEstimate(stc_data, vertices, 1, 1)
plot_source_spectrogram([stc, stc], [[1, 2], [3, 4]])
pytest.raises(ValueError, plot_source_spectrogram, [], [])
pytest.raises(ValueError, plot_source_spectrogram, [stc, stc], [[1, 2], [3, 4]], tmin=0)
pytest.raises(ValueError, plot_source_spectrogram, [stc, stc], [[1, 2], [3, 4]], tmax=7)
```

## Next Steps


---

*Source: test_misc.py:284 | Complexity: Advanced | Last updated: 2026-05-18*