# How To: Validate If List Of Axes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test validation of axes.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `cycler`
- `matplotlib`
- `numpy.testing`
- `mne`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.viz`
- `mne.viz.ui_events`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test validation of axes.'

```python
'Test validation of axes.'
```

### Step 2: Assign unknown = plt.subplots(...)

```python
fig, ax = plt.subplots(2, 2)
```

### Step 3: Call pytest.raises()

```python
pytest.raises(ValueError, _validate_if_list_of_axes, ax)
```

### Step 4: Assign ax_flat = ax.ravel(...)

```python
ax_flat = ax.ravel()
```

### Step 5: Assign ax = ax.ravel.tolist(...)

```python
ax = ax.ravel().tolist()
```

### Step 6: Call _validate_if_list_of_axes()

```python
_validate_if_list_of_axes(ax_flat)
```

### Step 7: Call _validate_if_list_of_axes()

```python
_validate_if_list_of_axes(ax_flat, 4)
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, _validate_if_list_of_axes, ax_flat, 5)
```

### Step 9: Call pytest.raises()

```python
pytest.raises(ValueError, _validate_if_list_of_axes, ax, 3)
```

### Step 10: Call pytest.raises()

```python
pytest.raises(TypeError, _validate_if_list_of_axes, 'error')
```

### Step 11: Call pytest.raises()

```python
pytest.raises(TypeError, _validate_if_list_of_axes, ['error'] * 2)
```

### Step 12: Call pytest.raises()

```python
pytest.raises(TypeError, _validate_if_list_of_axes, ax[0])
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, _validate_if_list_of_axes, ax, 3)
```

### Step 14: Assign unknown = 23

```python
ax_flat[2] = 23
```

### Step 15: Call pytest.raises()

```python
pytest.raises(TypeError, _validate_if_list_of_axes, ax_flat)
```

### Step 16: Call _validate_if_list_of_axes()

```python
_validate_if_list_of_axes(ax, 4)
```

### Step 17: Call plt.close()

```python
plt.close('all')
```


## Complete Example

```python
# Workflow
'Test validation of axes.'
fig, ax = plt.subplots(2, 2)
pytest.raises(ValueError, _validate_if_list_of_axes, ax)
ax_flat = ax.ravel()
ax = ax.ravel().tolist()
_validate_if_list_of_axes(ax_flat)
_validate_if_list_of_axes(ax_flat, 4)
pytest.raises(ValueError, _validate_if_list_of_axes, ax_flat, 5)
pytest.raises(ValueError, _validate_if_list_of_axes, ax, 3)
pytest.raises(TypeError, _validate_if_list_of_axes, 'error')
pytest.raises(TypeError, _validate_if_list_of_axes, ['error'] * 2)
pytest.raises(TypeError, _validate_if_list_of_axes, ax[0])
pytest.raises(ValueError, _validate_if_list_of_axes, ax, 3)
ax_flat[2] = 23
pytest.raises(TypeError, _validate_if_list_of_axes, ax_flat)
_validate_if_list_of_axes(ax, 4)
plt.close('all')
```

## Next Steps


---

*Source: test_utils.py:158 | Complexity: Advanced | Last updated: 2026-05-18*