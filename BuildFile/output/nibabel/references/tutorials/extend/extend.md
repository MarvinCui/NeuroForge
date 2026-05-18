# How To: Extend

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test extend

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

### Step 1: Assign total_nb_rows = value

```python
total_nb_rows = DATA['tractogram'].streamlines.total_nb_rows
```

**Verification:**
```python
assert len(sdict) == len(sdict2)
```

### Step 2: Assign sdict = PerArraySequenceDict(...)

```python
sdict = PerArraySequenceDict(total_nb_rows, DATA['data_per_point'])
```

**Verification:**
```python
assert_arrays_equal(sdict[k][:len(DATA['tractogram'])], DATA['tractogram'].data_per_point[k])
```

### Step 3: Assign list_nb_points = value

```python
list_nb_points = [2, 7, 4]
```

**Verification:**
```python
assert_arrays_equal(sdict[k][len(DATA['tractogram']):], new_data[k])
```

### Step 4: Assign data_per_point_shapes = value

```python
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:]}
```

**Verification:**
```python
assert_arrays_equal(sdict[k], sdict_orig[k])
```

### Step 5: Assign unknown = make_fake_tractogram(...)

```python
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
```

### Step 6: Assign sdict2 = PerArraySequenceDict(...)

```python
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
```

### Step 7: Call sdict.extend()

```python
sdict.extend(sdict2)
```

**Verification:**
```python
assert len(sdict) == len(sdict2)
```

### Step 8: Assign sdict_orig = copy.deepcopy(...)

```python
sdict_orig = copy.deepcopy(sdict)
```

### Step 9: Call sdict.extend()

```python
sdict.extend(PerArraySequenceDict())
```

### Step 10: Assign data_per_point_shapes = value

```python
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:], 'other': (7,)}
```

### Step 11: Assign unknown = make_fake_tractogram(...)

```python
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
```

### Step 12: Assign sdict2 = PerArraySequenceDict(...)

```python
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
```

### Step 13: Assign data_per_point_shapes = value

```python
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'other': DATA['fa'][0].shape[1:]}
```

### Step 14: Assign unknown = make_fake_tractogram(...)

```python
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
```

### Step 15: Assign sdict2 = PerArraySequenceDict(...)

```python
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
```

### Step 16: Assign data_per_point_shapes = value

```python
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:] + (3,)}
```

### Step 17: Assign unknown = make_fake_tractogram(...)

```python
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
```

### Step 18: Assign sdict2 = PerArraySequenceDict(...)

```python
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
```

### Step 19: Call assert_arrays_equal()

```python
assert_arrays_equal(sdict[k][:len(DATA['tractogram'])], DATA['tractogram'].data_per_point[k])
```

### Step 20: Call assert_arrays_equal()

```python
assert_arrays_equal(sdict[k][len(DATA['tractogram']):], new_data[k])
```

### Step 21: Call assert_arrays_equal()

```python
assert_arrays_equal(sdict[k], sdict_orig[k])
```

### Step 22: Call sdict.extend()

```python
sdict.extend(sdict2)
```

### Step 23: Call sdict.extend()

```python
sdict.extend(sdict2)
```

### Step 24: Call sdict.extend()

```python
sdict.extend(sdict2)
```


## Complete Example

```python
# Workflow
total_nb_rows = DATA['tractogram'].streamlines.total_nb_rows
sdict = PerArraySequenceDict(total_nb_rows, DATA['data_per_point'])
list_nb_points = [2, 7, 4]
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:]}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
sdict.extend(sdict2)
assert len(sdict) == len(sdict2)
for k in DATA['tractogram'].data_per_point:
    assert_arrays_equal(sdict[k][:len(DATA['tractogram'])], DATA['tractogram'].data_per_point[k])
    assert_arrays_equal(sdict[k][len(DATA['tractogram']):], new_data[k])
sdict_orig = copy.deepcopy(sdict)
sdict.extend(PerArraySequenceDict())
for k in sdict_orig.keys():
    assert_arrays_equal(sdict[k], sdict_orig[k])
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:], 'other': (7,)}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'other': DATA['fa'][0].shape[1:]}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
data_per_point_shapes = {'colors': DATA['colors'][0].shape[1:], 'fa': DATA['fa'][0].shape[1:] + (3,)}
_, new_data, _ = make_fake_tractogram(list_nb_points, data_per_point_shapes, rng=DATA['rng'])
sdict2 = PerArraySequenceDict(np.sum(list_nb_points), new_data)
with pytest.raises(ValueError):
    sdict.extend(sdict2)
```

## Next Steps


---

*Source: test_tractogram.py:381 | Complexity: Advanced | Last updated: 2026-05-18*