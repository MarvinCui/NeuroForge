# How To: Orient By Streamline

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test orient by streamline

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign streamlines = Streamlines(...)

```python
streamlines = Streamlines([np.array([[0, 0.0, 0], [1, 0.0, 0.0], [2, 0.0, 0.0]]), np.array([[2, 0.0, 0.0], [1, 0.0, 0], [0, 0, 0.0]])])
```

### Step 2: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 3: Assign unknown = value

```python
affine[:, 3] = [-1, 100, -20, 1]
```

### Step 4: Assign x_streamlines = Streamlines(...)

```python
x_streamlines = Streamlines([sl + affine[:3, 3] for sl in streamlines])
```

### Step 5: Assign standard_streamline = value

```python
standard_streamline = streamlines[0]
```

### Step 6: Assign flipped_sl = Streamlines(...)

```python
flipped_sl = Streamlines([streamlines[0], streamlines[1][::-1]])
```

### Step 7: Assign new_streamlines = orient_by_streamline(...)

```python
new_streamlines = orient_by_streamline(streamlines, standard_streamline, n_points=12, in_place=False)
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(new_streamlines, flipped_sl)
```

### Step 9: Call npt.assert_()

```python
npt.assert_(new_streamlines is not streamlines)
```

### Step 10: Assign x_flipped_sl = Streamlines(...)

```python
x_flipped_sl = Streamlines([s + affine[:3, 3] for s in flipped_sl])
```

### Step 11: Assign new_streamlines = orient_by_streamline(...)

```python
new_streamlines = orient_by_streamline(x_streamlines, standard_streamline, in_place=False)
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(new_streamlines, x_flipped_sl)
```

### Step 13: Call npt.assert_()

```python
npt.assert_(new_streamlines is not x_streamlines)
```

### Step 14: Assign new_streamlines = orient_by_streamline(...)

```python
new_streamlines = orient_by_streamline(streamlines, standard_streamline, in_place=False, as_generator=True)
```

### Step 15: Call npt.assert_()

```python
npt.assert_(isinstance(new_streamlines, types.GeneratorType))
```

### Step 16: Assign ll = Streamlines(...)

```python
ll = Streamlines(new_streamlines)
```

### Step 17: Call npt.assert_array_equal()

```python
npt.assert_array_equal(ll, flipped_sl)
```

### Step 18: Assign new_streamlines = orient_by_streamline(...)

```python
new_streamlines = orient_by_streamline(x_streamlines, standard_streamline, in_place=False, as_generator=True)
```

### Step 19: Call npt.assert_()

```python
npt.assert_(isinstance(new_streamlines, types.GeneratorType))
```

### Step 20: Assign ll = Streamlines(...)

```python
ll = Streamlines(new_streamlines)
```

### Step 21: Call npt.assert_array_equal()

```python
npt.assert_array_equal(ll, x_flipped_sl)
```

### Step 22: Assign new_streamlines = orient_by_streamline(...)

```python
new_streamlines = orient_by_streamline(streamlines, standard_streamline, in_place=True)
```

### Step 23: Call npt.assert_array_equal()

```python
npt.assert_array_equal(new_streamlines, flipped_sl)
```

### Step 24: Call npt.assert_()

```python
npt.assert_(new_streamlines is streamlines)
```


## Complete Example

```python
# Workflow
streamlines = Streamlines([np.array([[0, 0.0, 0], [1, 0.0, 0.0], [2, 0.0, 0.0]]), np.array([[2, 0.0, 0.0], [1, 0.0, 0], [0, 0, 0.0]])])
affine = np.eye(4)
affine[:, 3] = [-1, 100, -20, 1]
x_streamlines = Streamlines([sl + affine[:3, 3] for sl in streamlines])
standard_streamline = streamlines[0]
flipped_sl = Streamlines([streamlines[0], streamlines[1][::-1]])
new_streamlines = orient_by_streamline(streamlines, standard_streamline, n_points=12, in_place=False)
npt.assert_array_equal(new_streamlines, flipped_sl)
npt.assert_(new_streamlines is not streamlines)
x_flipped_sl = Streamlines([s + affine[:3, 3] for s in flipped_sl])
new_streamlines = orient_by_streamline(x_streamlines, standard_streamline, in_place=False)
npt.assert_array_equal(new_streamlines, x_flipped_sl)
npt.assert_(new_streamlines is not x_streamlines)
new_streamlines = orient_by_streamline(streamlines, standard_streamline, in_place=False, as_generator=True)
npt.assert_(isinstance(new_streamlines, types.GeneratorType))
ll = Streamlines(new_streamlines)
npt.assert_array_equal(ll, flipped_sl)
new_streamlines = orient_by_streamline(x_streamlines, standard_streamline, in_place=False, as_generator=True)
npt.assert_(isinstance(new_streamlines, types.GeneratorType))
ll = Streamlines(new_streamlines)
npt.assert_array_equal(ll, x_flipped_sl)
new_streamlines = orient_by_streamline(streamlines, standard_streamline, in_place=True)
npt.assert_array_equal(new_streamlines, flipped_sl)
npt.assert_(new_streamlines is streamlines)
```

## Next Steps


---

*Source: test_streamline.py:1109 | Complexity: Advanced | Last updated: 2026-05-18*