# How To: Show Event Plot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot_event.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.helpers`
- `nilearn.conftest`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.glm.tests._testing`
- `nilearn.plotting.matrix._utils`
- `nilearn.plotting.matrix.matrix_plotting`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test plot_event.'

```python
'Test plot_event.'
```

**Verification:**
```python
assert fig is not None
```

### Step 2: Assign onset = np.linspace(...)

```python
onset = np.linspace(0, 19.0, 20)
```

**Verification:**
```python
assert fig is not None
```

### Step 3: Assign duration = np.full(...)

```python
duration = np.full(20, 0.5)
```

**Verification:**
```python
assert (tmp_path / 'event.png').exists()
```

### Step 4: Assign trial_idx = np.arange(...)

```python
trial_idx = np.arange(20)
```

**Verification:**
```python
assert fig is None
```

### Step 5: Assign condition_ids = value

```python
condition_ids = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
```

**Verification:**
```python
assert (tmp_path / 'event.pdf').exists()
```

### Step 6: Assign modulation = np.full(...)

```python
modulation = np.full(20, 1)
```

### Step 7: Assign unknown = 0.5

```python
modulation[[1, 5, 15]] = 0.5
```

### Step 8: Assign trial_type = np.array(...)

```python
trial_type = np.array([condition_ids[i] for i in trial_idx])
```

### Step 9: Assign model_event = pd.DataFrame(...)

```python
model_event = pd.DataFrame({'onset': onset, 'duration': duration, 'trial_type': trial_type, 'modulation': modulation})
```

### Step 10: Assign fig = plot_event(...)

```python
fig = plot_event(model_event)
```

**Verification:**
```python
assert fig is not None
```

### Step 11: Assign fig = plot_event(...)

```python
fig = plot_event([model_event, model_event])
```

**Verification:**
```python
assert fig is not None
```

### Step 12: Assign fig = plot_event(...)

```python
fig = plot_event(model_event, output_file=tmp_path / 'event.png')
```

**Verification:**
```python
assert (tmp_path / 'event.png').exists()
```

### Step 13: Call plot_event()

```python
plot_event(model_event, output_file=tmp_path / 'event.pdf')
```

**Verification:**
```python
assert (tmp_path / 'event.pdf').exists()
```

### Step 14: Call pytest.skip()

```python
pytest.skip('Saving figures is not supported when GIL is disabled.')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test plot_event.'
onset = np.linspace(0, 19.0, 20)
duration = np.full(20, 0.5)
trial_idx = np.arange(20)
trial_idx[10:] -= 10
condition_ids = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
modulation = np.full(20, 1)
modulation[[1, 5, 15]] = 0.5
trial_type = np.array([condition_ids[i] for i in trial_idx])
model_event = pd.DataFrame({'onset': onset, 'duration': duration, 'trial_type': trial_type, 'modulation': modulation})
fig = plot_event(model_event)
assert fig is not None
fig = plot_event([model_event, model_event])
assert fig is not None
if not is_gil_enabled():
    pytest.skip('Saving figures is not supported when GIL is disabled.')
fig = plot_event(model_event, output_file=tmp_path / 'event.png')
assert (tmp_path / 'event.png').exists()
assert fig is None
plot_event(model_event, output_file=tmp_path / 'event.pdf')
assert (tmp_path / 'event.pdf').exists()
```

## Next Steps


---

*Source: test_matrix_plotting.py:190 | Complexity: Advanced | Last updated: 2026-05-18*