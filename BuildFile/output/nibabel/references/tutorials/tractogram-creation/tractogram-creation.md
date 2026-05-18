# How To: Tractogram Creation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test tractogram creation

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

### Step 1: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram()
```

**Verification:**
```python
assert tractogram.affine_to_rasmm is None
```

### Step 2: Call check_tractogram()

```python
check_tractogram(tractogram)
```

**Verification:**
```python
assert_array_equal(tractogram.affine_to_rasmm, affine)
```

### Step 3: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(streamlines=DATA['streamlines'])
```

**Verification:**
```python
assert is_data_dict(tractogram.data_per_streamline)
```

### Step 4: Call check_tractogram()

```python
check_tractogram(tractogram, DATA['streamlines'])
```

**Verification:**
```python
assert is_data_dict(tractogram.data_per_point)
```

### Step 5: Assign affine = np.diag(...)

```python
affine = np.diag([1, 2, 3, 1])
```

**Verification:**
```python
assert_tractogram_equal(tractogram2, tractogram)
```

### Step 6: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(affine_to_rasmm=affine)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(tractogram.affine_to_rasmm, affine)
```

### Step 8: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
```

### Step 9: Call check_tractogram()

```python
check_tractogram(tractogram, DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
```

**Verification:**
```python
assert is_data_dict(tractogram.data_per_streamline)
```

### Step 10: Assign tractogram2 = Tractogram(...)

```python
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
```

### Step 11: Call assert_tractogram_equal()

```python
assert_tractogram_equal(tractogram2, tractogram)
```

### Step 12: Assign tractogram = LazyTractogram(...)

```python
tractogram = LazyTractogram(DATA['streamlines_func'], DATA['data_per_streamline_func'], DATA['data_per_point_func'])
```

### Step 13: Assign tractogram2 = Tractogram(...)

```python
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
```

### Step 14: Assign wrong_data = value

```python
wrong_data = [[(1, 0, 0)] * 1, [(0, 1, 0), (0, 1)], [(0, 0, 1)] * 5]
```

### Step 15: Assign data_per_point = value

```python
data_per_point = {'wrong_data': wrong_data}
```

### Step 16: Assign wrong_data = value

```python
wrong_data = [[(1, 0, 0)] * 1, [(0, 1)] * 2, [(0, 0, 1)] * 5]
```

### Step 17: Assign data_per_point = value

```python
data_per_point = {'wrong_data': wrong_data}
```

### Step 18: Call Tractogram()

```python
Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
```

### Step 19: Call Tractogram()

```python
Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
```


## Complete Example

```python
# Workflow
tractogram = Tractogram()
check_tractogram(tractogram)
assert tractogram.affine_to_rasmm is None
tractogram = Tractogram(streamlines=DATA['streamlines'])
check_tractogram(tractogram, DATA['streamlines'])
affine = np.diag([1, 2, 3, 1])
tractogram = Tractogram(affine_to_rasmm=affine)
assert_array_equal(tractogram.affine_to_rasmm, affine)
tractogram = Tractogram(DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
check_tractogram(tractogram, DATA['streamlines'], DATA['data_per_streamline'], DATA['data_per_point'])
assert is_data_dict(tractogram.data_per_streamline)
assert is_data_dict(tractogram.data_per_point)
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
assert_tractogram_equal(tractogram2, tractogram)
tractogram = LazyTractogram(DATA['streamlines_func'], DATA['data_per_streamline_func'], DATA['data_per_point_func'])
tractogram2 = Tractogram(tractogram.streamlines, tractogram.data_per_streamline, tractogram.data_per_point)
wrong_data = [[(1, 0, 0)] * 1, [(0, 1, 0), (0, 1)], [(0, 0, 1)] * 5]
data_per_point = {'wrong_data': wrong_data}
with pytest.raises(ValueError):
    Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
wrong_data = [[(1, 0, 0)] * 1, [(0, 1)] * 2, [(0, 0, 1)] * 5]
data_per_point = {'wrong_data': wrong_data}
with pytest.raises(ValueError):
    Tractogram(streamlines=DATA['streamlines'], data_per_point=data_per_point)
```

## Next Steps


---

*Source: test_tractogram.py:492 | Complexity: Advanced | Last updated: 2026-05-18*