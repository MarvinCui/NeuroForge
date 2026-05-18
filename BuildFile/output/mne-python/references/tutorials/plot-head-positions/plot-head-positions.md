# How To: Plot Head Positions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting of head positions.

## Prerequisites

**Required Modules:**
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `matplotlib.figure`
- `numpy.testing`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.defaults`
- `mne.fixes`
- `mne.io`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`
- `mne.viz`
- `mne.viz._3d`
- `mne.viz.utils`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.viz`


## Step-by-Step Guide

### Step 1: 'Test plotting of head positions.'

```python
'Test plotting of head positions.'
```

**Verification:**
```python
assert len(fig.axes) == 6
```

### Step 2: Assign info = read_info(...)

```python
info = read_info(evoked_fname)
```

**Verification:**
```python
assert len(fig.axes) == 8
```

### Step 3: Assign pos = np.random.RandomState.randn(...)

```python
pos = np.random.RandomState(0).randn(4, 10)
```

### Step 4: Assign unknown = np.arange(...)

```python
pos[:, 0] = np.arange(len(pos))
```

### Step 5: Assign destination = value

```python
destination = (0.0, 0.0, 0.04)
```

### Step 6: Assign fig = plot_head_positions(...)

```python
fig = plot_head_positions(pos)
```

**Verification:**
```python
assert len(fig.axes) == 6
```

### Step 7: Call plot_head_positions()

```python
plot_head_positions(pos, mode='field', info=info, destination=destination)
```

### Step 8: Assign fig = plot_head_positions(...)

```python
fig = plot_head_positions([pos, pos], totals=True)
```

**Verification:**
```python
assert len(fig.axes) == 8
```

### Step 9: Assign unknown = plt.subplots(...)

```python
fig, ax = plt.subplots()
```

### Step 10: Assign unknown = plt.subplots(...)

```python
fig, ax = plt.subplots(subplot_kw=dict(projection='3d'))
```

### Step 11: Call plot_head_positions()

```python
plot_head_positions(pos, mode='field', info=info, axes=ax)
```

### Step 12: Call plot_head_positions()

```python
plot_head_positions(pos, mode='field', info=info, axes=ax)
```

### Step 13: Call plot_head_positions()

```python
plot_head_positions(['foo'])
```

### Step 14: Call plot_head_positions()

```python
plot_head_positions(pos[:, :9])
```

### Step 15: Call plot_head_positions()

```python
plot_head_positions(pos, 'foo')
```

### Step 16: Call plot_head_positions()

```python
plot_head_positions(pos, axes=1.0)
```


## Complete Example

```python
# Workflow
'Test plotting of head positions.'
info = read_info(evoked_fname)
pos = np.random.RandomState(0).randn(4, 10)
pos[:, 0] = np.arange(len(pos))
destination = (0.0, 0.0, 0.04)
fig = plot_head_positions(pos)
assert len(fig.axes) == 6
plot_head_positions(pos, mode='field', info=info, destination=destination)
fig = plot_head_positions([pos, pos], totals=True)
assert len(fig.axes) == 8
fig, ax = plt.subplots()
with pytest.raises(TypeError, match='instance of Axes3D'):
    plot_head_positions(pos, mode='field', info=info, axes=ax)
fig, ax = plt.subplots(subplot_kw=dict(projection='3d'))
plot_head_positions(pos, mode='field', info=info, axes=ax)
with pytest.raises(TypeError, match='must be an instance of ndarray'):
    plot_head_positions(['foo'])
with pytest.raises(ValueError, match='must be dim'):
    plot_head_positions(pos[:, :9])
with pytest.raises(ValueError, match='Allowed values'):
    plot_head_positions(pos, 'foo')
with pytest.raises(ValueError, match='shape'):
    plot_head_positions(pos, axes=1.0)
```

## Next Steps


---

*Source: test_3d.py:97 | Complexity: Advanced | Last updated: 2026-05-18*