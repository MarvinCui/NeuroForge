# How To: Tractogram Add New Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test tractogram add new data

## Prerequisites

**Required Modules:**
- `copy`
- `operator`
- `unittest`
- `warnings`
- `collections`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `tractogram`


## Step-by-Step Guide

### Step 1: Assign t = unknown.copy(...)

```python
t = DATA['simple_tractogram'].copy()
```

**Verification:**
```python
assert_tractogram_equal(t, DATA['tractogram'])
```

### Step 2: Assign unknown = value

```python
t.data_per_point['fa'] = DATA['fa']
```

**Verification:**
```python
assert_tractogram_item_equal(t[i], item)
```

### Step 3: Assign unknown = value

```python
t.data_per_point['colors'] = DATA['colors']
```

**Verification:**
```python
assert_tractogram_equal(t, DATA['tractogram'])
```

### Step 4: Assign unknown = value

```python
t.data_per_streamline['mean_curvature'] = DATA['mean_curvature']
```

### Step 5: Assign unknown = value

```python
t.data_per_streamline['mean_torsion'] = DATA['mean_torsion']
```

### Step 6: Assign unknown = value

```python
t.data_per_streamline['mean_colors'] = DATA['mean_colors']
```

### Step 7: Assign unknown = value

```python
t.data_per_streamline['clusters_labels'] = DATA['clusters_labels']
```

### Step 8: Call assert_tractogram_equal()

```python
assert_tractogram_equal(t, DATA['tractogram'])
```

### Step 9: Assign r_tractogram = value

```python
r_tractogram = t[::-1]
```

### Step 10: Call check_tractogram()

```python
check_tractogram(r_tractogram, t.streamlines[::-1], t.data_per_streamline[::-1], t.data_per_point[::-1])
```

### Step 11: Assign t = Tractogram(...)

```python
t = Tractogram(DATA['streamlines'] * 2, affine_to_rasmm=np.eye(4))
```

### Step 12: Assign t = value

```python
t = t[:len(DATA['streamlines'])]
```

### Step 13: Assign unknown = value

```python
t.data_per_point['fa'] = DATA['fa']
```

### Step 14: Assign unknown = value

```python
t.data_per_point['colors'] = DATA['colors']
```

### Step 15: Assign unknown = value

```python
t.data_per_streamline['mean_curvature'] = DATA['mean_curvature']
```

### Step 16: Assign unknown = value

```python
t.data_per_streamline['mean_torsion'] = DATA['mean_torsion']
```

### Step 17: Assign unknown = value

```python
t.data_per_streamline['mean_colors'] = DATA['mean_colors']
```

### Step 18: Assign unknown = value

```python
t.data_per_streamline['clusters_labels'] = DATA['clusters_labels']
```

### Step 19: Call assert_tractogram_equal()

```python
assert_tractogram_equal(t, DATA['tractogram'])
```

### Step 20: Call assert_tractogram_item_equal()

```python
assert_tractogram_item_equal(t[i], item)
```


## Complete Example

```python
# Workflow
t = DATA['simple_tractogram'].copy()
t.data_per_point['fa'] = DATA['fa']
t.data_per_point['colors'] = DATA['colors']
t.data_per_streamline['mean_curvature'] = DATA['mean_curvature']
t.data_per_streamline['mean_torsion'] = DATA['mean_torsion']
t.data_per_streamline['mean_colors'] = DATA['mean_colors']
t.data_per_streamline['clusters_labels'] = DATA['clusters_labels']
assert_tractogram_equal(t, DATA['tractogram'])
for i, item in enumerate(t):
    assert_tractogram_item_equal(t[i], item)
r_tractogram = t[::-1]
check_tractogram(r_tractogram, t.streamlines[::-1], t.data_per_streamline[::-1], t.data_per_point[::-1])
t = Tractogram(DATA['streamlines'] * 2, affine_to_rasmm=np.eye(4))
t = t[:len(DATA['streamlines'])]
t.data_per_point['fa'] = DATA['fa']
t.data_per_point['colors'] = DATA['colors']
t.data_per_streamline['mean_curvature'] = DATA['mean_curvature']
t.data_per_streamline['mean_torsion'] = DATA['mean_torsion']
t.data_per_streamline['mean_colors'] = DATA['mean_colors']
t.data_per_streamline['clusters_labels'] = DATA['clusters_labels']
assert_tractogram_equal(t, DATA['tractogram'])
```

## Next Steps


---

*Source: test_tractogram.py:593 | Complexity: Advanced | Last updated: 2026-05-18*