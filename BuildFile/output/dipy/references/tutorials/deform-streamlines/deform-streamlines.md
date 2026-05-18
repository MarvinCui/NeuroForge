# How To: Deform Streamlines

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test deform streamlines

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `types`
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.testing.memory`
- `dipy.tracking.streamline`
- `dipy.tracking.streamlinespeed`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign deformation_field = rng.standard_normal(...)

```python
deformation_field = rng.standard_normal((200, 200, 200, 3))
```

**Verification:**
```python
assert_allclose(s, o.astype(np.float32), rtol=1e-06, atol=1e-06)
```

### Step 2: Assign stream2grid = np.array(...)

```python
stream2grid = np.array([[-0.13152201, -0.52553149, -0.06759869, -0.80014208], [1.01579851, 0.19840874, 0.18875411, 0.81826065], [-0.07047617, -0.9290094, -0.55623385, 0.55165017], [0.0, 0.0, 0.0, 1.0]])
```

### Step 3: Assign grid2world = np.array(...)

```python
grid2world = np.array([[0.83354727, 1.33876877, 1.0218087, 0.12809569], [0.83571344, 0.63824941, 0.20564267, 0.82740437], [-0.26574668, -0.66695577, 0.11636694, -0.02620037], [0.0, 0.0, 0.0, 1.0]])
```

### Step 4: Assign stream2world = np.dot(...)

```python
stream2world = np.dot(stream2grid, grid2world)
```

### Step 5: Assign new_streamlines = deform_streamlines(...)

```python
new_streamlines = deform_streamlines(streamlines, deformation_field, stream2grid, grid2world, stream2grid, grid2world)
```

### Step 6: Assign streamlines_in_grid = transform_streamlines(...)

```python
streamlines_in_grid = transform_streamlines(streamlines, stream2grid)
```

### Step 7: Assign disps = values_from_volume(...)

```python
disps = values_from_volume(deformation_field, streamlines_in_grid, np.eye(4))
```

### Step 8: Assign new_streamlines_world = transform_streamlines(...)

```python
new_streamlines_world = transform_streamlines(new_streamlines, stream2world)
```

### Step 9: Assign orig_streamlines_world = np.subtract(...)

```python
orig_streamlines_world = np.subtract(np.array(new_streamlines_world, dtype=object), np.array(disps, dtype=object))
```

### Step 10: Assign orig_streamlines = transform_streamlines(...)

```python
orig_streamlines = transform_streamlines(orig_streamlines_world, np.linalg.inv(stream2world))
```

### Step 11: Call assert_allclose()

```python
assert_allclose(s, o.astype(np.float32), rtol=1e-06, atol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
deformation_field = rng.standard_normal((200, 200, 200, 3))
stream2grid = np.array([[-0.13152201, -0.52553149, -0.06759869, -0.80014208], [1.01579851, 0.19840874, 0.18875411, 0.81826065], [-0.07047617, -0.9290094, -0.55623385, 0.55165017], [0.0, 0.0, 0.0, 1.0]])
grid2world = np.array([[0.83354727, 1.33876877, 1.0218087, 0.12809569], [0.83571344, 0.63824941, 0.20564267, 0.82740437], [-0.26574668, -0.66695577, 0.11636694, -0.02620037], [0.0, 0.0, 0.0, 1.0]])
stream2world = np.dot(stream2grid, grid2world)
new_streamlines = deform_streamlines(streamlines, deformation_field, stream2grid, grid2world, stream2grid, grid2world)
streamlines_in_grid = transform_streamlines(streamlines, stream2grid)
disps = values_from_volume(deformation_field, streamlines_in_grid, np.eye(4))
new_streamlines_world = transform_streamlines(new_streamlines, stream2world)
orig_streamlines_world = np.subtract(np.array(new_streamlines_world, dtype=object), np.array(disps, dtype=object))
orig_streamlines = transform_streamlines(orig_streamlines_world, np.linalg.inv(stream2world))
for o, s in zip(orig_streamlines, streamlines):
    assert_allclose(s, o.astype(np.float32), rtol=1e-06, atol=1e-06)
```

## Next Steps


---

*Source: test_streamline.py:586 | Complexity: Advanced | Last updated: 2026-05-18*