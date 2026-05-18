# How To: Compute Distance To Sensors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test computation of distances between vertices and sensors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.fixes`
- `mne.source_estimate`
- `mne.source_space`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: picks, limits
```

## Step-by-Step Guide

### Step 1: 'Test computation of distances between vertices and sensors.'

```python
'Test computation of distances between vertices and sensors.'
```

**Verification:**
```python
assert depths.shape == (n_verts, n_picks)
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname_src)
```

**Verification:**
```python
assert limits[0] * 5 > depths.min()
```

### Step 3: Assign fwd = mne.read_forward_solution(...)

```python
fwd = mne.read_forward_solution(fname_fwd)
```

**Verification:**
```python
assert_array_less(limits[0], depths)
```

### Step 4: Assign info = value

```python
info = fwd['info']
```

**Verification:**
```python
assert_array_less(depths, limits[1])
```

### Step 5: Assign trans = read_trans(...)

```python
trans = read_trans(trans_fname)
```

**Verification:**
```python
assert_allclose(depths, depths2, rtol=1e-05)
```

### Step 6: Assign n_picks = len(...)

```python
n_picks = len(_picks_to_idx(info, use_picks, 'data', exclude=()))
```

### Step 7: Assign unknown = value

```python
src[0]['inuse'] = fwd['src'][0]['inuse']
```

### Step 8: Assign unknown = value

```python
src[1]['inuse'] = fwd['src'][1]['inuse']
```

### Step 9: Assign unknown = value

```python
src[0]['nuse'] = fwd['src'][0]['nuse']
```

### Step 10: Assign unknown = value

```python
src[1]['nuse'] = fwd['src'][1]['nuse']
```

### Step 11: Assign n_verts = value

```python
n_verts = src[0]['nuse'] + src[1]['nuse']
```

### Step 12: Assign depths = compute_distance_to_sensors(...)

```python
depths = compute_distance_to_sensors(src, info=info, picks=use_picks, trans=trans)
```

**Verification:**
```python
assert depths.shape == (n_verts, n_picks)
```

### Step 13: Call assert_array_less()

```python
assert_array_less(limits[0], depths)
```

### Step 14: Call assert_array_less()

```python
assert_array_less(depths, limits[1])
```

### Step 15: Assign depths2 = compute_distance_to_sensors(...)

```python
depths2 = compute_distance_to_sensors(src=fwd['src'], info=info, picks=use_picks, trans=None)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(depths, depths2, rtol=1e-05)
```

### Step 17: Assign kwargs = dict(...)

```python
kwargs = dict()
```

### Step 18: Assign unknown = True

```python
kwargs[picks] = True
```

### Step 19: Assign use_picks = pick_types(...)

```python
use_picks = pick_types(info, **kwargs, exclude=())
```

### Step 20: Assign use_picks = picks

```python
use_picks = picks
```

### Step 21: Assign unknown = None

```python
info['dev_head_t'] = None
```

### Step 22: Assign unknown = None

```python
info['dev_head_t'] = None
```

### Step 23: Call compute_distance_to_sensors()

```python
compute_distance_to_sensors(src, info, use_picks, trans)
```


## Complete Example

```python
# Setup
# Fixtures: picks, limits

# Workflow
'Test computation of distances between vertices and sensors.'
src = read_source_spaces(fname_src)
fwd = mne.read_forward_solution(fname_fwd)
info = fwd['info']
trans = read_trans(trans_fname)
if isinstance(picks, str):
    kwargs = dict()
    kwargs[picks] = True
    if picks == 'eeg':
        info['dev_head_t'] = None
    use_picks = pick_types(info, **kwargs, exclude=())
else:
    use_picks = picks
n_picks = len(_picks_to_idx(info, use_picks, 'data', exclude=()))
src[0]['inuse'] = fwd['src'][0]['inuse']
src[1]['inuse'] = fwd['src'][1]['inuse']
src[0]['nuse'] = fwd['src'][0]['nuse']
src[1]['nuse'] = fwd['src'][1]['nuse']
n_verts = src[0]['nuse'] + src[1]['nuse']
depths = compute_distance_to_sensors(src, info=info, picks=use_picks, trans=trans)
assert depths.shape == (n_verts, n_picks)
assert limits[0] * 5 > depths.min()
assert_array_less(limits[0], depths)
assert_array_less(depths, limits[1])
depths2 = compute_distance_to_sensors(src=fwd['src'], info=info, picks=use_picks, trans=None)
assert_allclose(depths, depths2, rtol=1e-05)
if picks != 'eeg':
    info['dev_head_t'] = None
    with pytest.raises(ValueError, match='Transform between meg<->head'):
        compute_distance_to_sensors(src, info, use_picks, trans)
```

## Next Steps


---

*Source: test_source_space.py:81 | Complexity: Advanced | Last updated: 2026-05-18*