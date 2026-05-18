# How To: Length

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test length

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking._utils`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`
- `dipy.tracking.vox2track`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign n_streamlines = 50

```python
n_streamlines = 50
```

### Step 2: Assign n_pts = 100

```python
n_pts = 100
```

### Step 3: Assign t = np.linspace(...)

```python
t = np.linspace(-10, 10, n_pts)
```

### Step 4: Assign bundle = value

```python
bundle = []
```

### Step 5: Assign start = rng.integers(...)

```python
start = rng.integers(10, 30, n_streamlines)
```

### Step 6: Assign end = rng.integers(...)

```python
end = rng.integers(60, 100, n_streamlines)
```

### Step 7: Assign bundle = value

```python
bundle = [10 * streamline[start[i]:end[i]] for i, streamline in enumerate(bundle)]
```

### Step 8: Assign bundle_lengths = length(...)

```python
bundle_lengths = length(bundle)
```

### Step 9: Assign pts = value

```python
pts = np.vstack((np.cos(2 * t / np.pi), np.zeros(t.shape) + i, t)).T
```

### Step 10: Call bundle.append()

```python
bundle.append(pts)
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal(this_length, metrics.length(bundle[idx]))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n_streamlines = 50
n_pts = 100
t = np.linspace(-10, 10, n_pts)
bundle = []
for i in np.linspace(3, 5, n_streamlines):
    pts = np.vstack((np.cos(2 * t / np.pi), np.zeros(t.shape) + i, t)).T
    bundle.append(pts)
start = rng.integers(10, 30, n_streamlines)
end = rng.integers(60, 100, n_streamlines)
bundle = [10 * streamline[start[i]:end[i]] for i, streamline in enumerate(bundle)]
bundle_lengths = length(bundle)
for idx, this_length in enumerate(bundle_lengths):
    npt.assert_equal(this_length, metrics.length(bundle[idx]))
```

## Next Steps


---

*Source: test_utils.py:643 | Complexity: Advanced | Last updated: 2026-05-18*