# How To: Mix Colormaps

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mix colormaps

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nilearn.plotting.cm`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign n = 100

```python
n = 100
```

**Verification:**
```python
assert mix_map.shape == (n, 4)
```

### Step 2: Assign foreground_map = rng.random(...)

```python
foreground_map = rng.random((n, 4))
```

**Verification:**
```python
assert np.all(mix_map[:, 3] >= foreground_map[:, 3])
```

### Step 3: Assign background_map = rng.random(...)

```python
background_map = rng.random((n, 4))
```

**Verification:**
```python
assert np.all(mix_map[:, 3] >= background_map[:, 3])
```

### Step 4: Assign mix_map = mix_colormaps(...)

```python
mix_map = mix_colormaps(foreground_map, background_map)
```

**Verification:**
```python
assert np.allclose(mix_map, background_map)
```

### Step 5: Assign background_map = rng.random(...)

```python
background_map = rng.random((n - 1, 4))
```

**Verification:**
```python
assert np.allclose(mix_map, foreground_map)
```

### Step 6: Assign foreground_map = rng.random(...)

```python
foreground_map = rng.random((n, 4))
```

**Verification:**
```python
assert np.allclose(mix_map[:, :3], foreground_map[:, :3])
```

### Step 7: Assign background_map = rng.random(...)

```python
background_map = rng.random((n, 4))
```

### Step 8: Assign unknown = 0

```python
foreground_map[:, 3] = 0
```

### Step 9: Assign mix_map = mix_colormaps(...)

```python
mix_map = mix_colormaps(foreground_map, background_map)
```

**Verification:**
```python
assert np.allclose(mix_map, background_map)
```

### Step 10: Assign foreground_map = rng.random(...)

```python
foreground_map = rng.random((n, 4))
```

### Step 11: Assign background_map = rng.random(...)

```python
background_map = rng.random((n, 4))
```

### Step 12: Assign unknown = 0

```python
background_map[:, 3] = 0
```

### Step 13: Assign mix_map = mix_colormaps(...)

```python
mix_map = mix_colormaps(foreground_map, background_map)
```

**Verification:**
```python
assert np.allclose(mix_map, foreground_map)
```

### Step 14: Assign foreground_map = rng.random(...)

```python
foreground_map = rng.random((n, 4))
```

### Step 15: Assign background_map = foreground_map

```python
background_map = foreground_map
```

### Step 16: Assign mix_map = mix_colormaps(...)

```python
mix_map = mix_colormaps(foreground_map, background_map)
```

**Verification:**
```python
assert np.allclose(mix_map[:, :3], foreground_map[:, :3])
```

### Step 17: Call mix_colormaps()

```python
mix_colormaps(foreground_map, background_map)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n = 100
foreground_map = rng.random((n, 4))
background_map = rng.random((n, 4))
mix_map = mix_colormaps(foreground_map, background_map)
assert mix_map.shape == (n, 4)
assert np.all(mix_map[:, 3] >= foreground_map[:, 3])
assert np.all(mix_map[:, 3] >= background_map[:, 3])
background_map = rng.random((n - 1, 4))
with pytest.raises(ValueError):
    mix_colormaps(foreground_map, background_map)
foreground_map = rng.random((n, 4))
background_map = rng.random((n, 4))
foreground_map[:, 3] = 0
mix_map = mix_colormaps(foreground_map, background_map)
assert np.allclose(mix_map, background_map)
foreground_map = rng.random((n, 4))
background_map = rng.random((n, 4))
background_map[:, 3] = 0
mix_map = mix_colormaps(foreground_map, background_map)
assert np.allclose(mix_map, foreground_map)
foreground_map = rng.random((n, 4))
background_map = foreground_map
mix_map = mix_colormaps(foreground_map, background_map)
assert np.allclose(mix_map[:, :3], foreground_map[:, :3])
```

## Next Steps


---

*Source: test_cm.py:31 | Complexity: Advanced | Last updated: 2026-05-18*