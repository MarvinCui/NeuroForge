# How To: Plot Event Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plot_event error with cmap.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test plot_event error with cmap.'

```python
'Test plot_event error with cmap.'
```

### Step 2: Assign onset = np.linspace(...)

```python
onset = np.linspace(0, 19.0, 20)
```

### Step 3: Assign duration = np.full(...)

```python
duration = np.full(20, 0.5)
```

### Step 4: Assign trial_idx = np.arange(...)

```python
trial_idx = np.arange(20)
```

### Step 5: Assign condition_ids = value

```python
condition_ids = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k']
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

### Step 10: Call plot_event()

```python
plot_event(model_event, cmap='tab10')
```


## Complete Example

```python
# Workflow
'Test plot_event error with cmap.'
onset = np.linspace(0, 19.0, 20)
duration = np.full(20, 0.5)
trial_idx = np.arange(20)
trial_idx[11:] -= 10
condition_ids = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k']
modulation = np.full(20, 1)
modulation[[1, 5, 15]] = 0.5
trial_type = np.array([condition_ids[i] for i in trial_idx])
model_event = pd.DataFrame({'onset': onset, 'duration': duration, 'trial_type': trial_type, 'modulation': modulation})
with pytest.raises(ValueError, match='The number of event types is greater than colors in colormap'):
    plot_event(model_event, cmap='tab10')
```

## Next Steps


---

*Source: test_matrix_plotting.py:238 | Complexity: Advanced | Last updated: 2026-05-18*