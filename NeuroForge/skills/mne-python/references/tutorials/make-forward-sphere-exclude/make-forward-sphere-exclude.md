# How To: Make Forward Sphere Exclude

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that points are excluded that are outside BEM sphere inner layer.

## Prerequisites

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.dipole`
- `mne.forward`
- `mne.forward._compute_forward`
- `mne.forward._make_forward`
- `mne.forward.tests.test_forward`
- `mne.io`
- `mne.simulation`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that points are excluded that are outside BEM sphere inner layer.'

```python
'Test that points are excluded that are outside BEM sphere inner layer.'
```

**Verification:**
```python
assert src[0]['nuse'] == 2102
```

### Step 2: Assign r0 = value

```python
r0 = (0.0, 0.0, 0.04)
```

**Verification:**
```python
assert fwd['nsource'] == src[0]['nuse']
```

### Step 3: Assign inner_radius = 0.08

```python
inner_radius = 0.08
```

**Verification:**
```python
assert fwd_small['nsource'] < src[0]['nuse']
```

### Step 4: Assign head_radius = value

```python
head_radius = inner_radius / 0.9
```

**Verification:**
```python
assert_allclose(fwd_data[:, idx], fwd_small_data)
```

### Step 5: Assign bem = make_sphere_model(...)

```python
bem = make_sphere_model(r0=r0, head_radius=head_radius)
```

**Verification:**
```python
assert fwd_small_2['nsource'] == fwd_small['nsource']
```

### Step 6: Assign src = setup_volume_source_space(...)

```python
src = setup_volume_source_space(pos=10.0, sphere=r0 + (inner_radius,), mindist=1, exclude=10)
```

**Verification:**
```python
assert_allclose(fwd_small_data, fwd_small_2_data)
```

### Step 7: Assign trans = Transform(...)

```python
trans = Transform('mri', 'head')
```

### Step 8: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw)
```

### Step 9: Call raw.pick()

```python
raw.pick(raw.ch_names[:1])
```

### Step 10: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(raw.info, trans, src, bem, mindist=0)
```

**Verification:**
```python
assert fwd['nsource'] == src[0]['nuse']
```

### Step 11: Assign bem_small = make_sphere_model(...)

```python
bem_small = make_sphere_model(r0=r0, head_radius=head_radius - 0.01 / 0.9)
```

### Step 12: Assign fwd_small = make_forward_solution(...)

```python
fwd_small = make_forward_solution(raw.info, trans, src, bem_small, mindist=0)
```

**Verification:**
```python
assert fwd_small['nsource'] < src[0]['nuse']
```

### Step 13: Assign idx = np.searchsorted(...)

```python
idx = np.searchsorted(fwd['src'][0]['vertno'], fwd_small['src'][0]['vertno'])
```

### Step 14: Assign fwd_data = np.reshape(...)

```python
fwd_data = np.reshape(fwd['sol']['data'], (len(raw.ch_names), -1, 3))
```

### Step 15: Assign fwd_small_data = np.reshape(...)

```python
fwd_small_data = np.reshape(fwd_small['sol']['data'], (len(raw.ch_names), -1, 3))
```

### Step 16: Call assert_allclose()

```python
assert_allclose(fwd_data[:, idx], fwd_small_data)
```

### Step 17: Assign fwd_small_2 = make_forward_solution(...)

```python
fwd_small_2 = make_forward_solution(raw.info, trans, src, bem, mindist=9.999)
```

**Verification:**
```python
assert fwd_small_2['nsource'] == fwd_small['nsource']
```

### Step 18: Assign fwd_small_2_data = np.reshape(...)

```python
fwd_small_2_data = np.reshape(fwd_small_2['sol']['data'], (len(raw.ch_names), -1, 3))
```

### Step 19: Call assert_allclose()

```python
assert_allclose(fwd_small_data, fwd_small_2_data)
```


## Complete Example

```python
# Workflow
'Test that points are excluded that are outside BEM sphere inner layer.'
r0 = (0.0, 0.0, 0.04)
inner_radius = 0.08
head_radius = inner_radius / 0.9
bem = make_sphere_model(r0=r0, head_radius=head_radius)
src = setup_volume_source_space(pos=10.0, sphere=r0 + (inner_radius,), mindist=1, exclude=10)
assert src[0]['nuse'] == 2102
trans = Transform('mri', 'head')
raw = read_raw_fif(fname_raw)
raw.pick(raw.ch_names[:1])
fwd = make_forward_solution(raw.info, trans, src, bem, mindist=0)
assert fwd['nsource'] == src[0]['nuse']
bem_small = make_sphere_model(r0=r0, head_radius=head_radius - 0.01 / 0.9)
fwd_small = make_forward_solution(raw.info, trans, src, bem_small, mindist=0)
assert fwd_small['nsource'] < src[0]['nuse']
idx = np.searchsorted(fwd['src'][0]['vertno'], fwd_small['src'][0]['vertno'])
fwd_data = np.reshape(fwd['sol']['data'], (len(raw.ch_names), -1, 3))
fwd_small_data = np.reshape(fwd_small['sol']['data'], (len(raw.ch_names), -1, 3))
assert_allclose(fwd_data[:, idx], fwd_small_data)
fwd_small_2 = make_forward_solution(raw.info, trans, src, bem, mindist=9.999)
assert fwd_small_2['nsource'] == fwd_small['nsource']
fwd_small_2_data = np.reshape(fwd_small_2['sol']['data'], (len(raw.ch_names), -1, 3))
assert_allclose(fwd_small_data, fwd_small_2_data)
```

## Next Steps


---

*Source: test_make_forward.py:616 | Complexity: Advanced | Last updated: 2026-05-18*