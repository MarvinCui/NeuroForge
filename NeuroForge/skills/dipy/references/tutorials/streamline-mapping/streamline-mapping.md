# How To: Streamline Mapping

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test streamline mapping

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign streamlines = value

```python
streamlines = [np.array([[0, 0, 0], [0, 0, 0], [0, 2, 2]], 'float'), np.array([[0, 0, 0], [0, 1, 1], [0, 2, 2]], 'float'), np.array([[0, 2, 2], [0, 1, 1], [0, 0, 0]], 'float')]
```

### Step 2: Assign mapping = streamline_mapping(...)

```python
mapping = streamline_mapping(streamlines, affine=np.eye(4))
```

### Step 3: Assign expected = value

```python
expected = {(0, 0, 0): [0, 1, 2], (0, 2, 2): [0, 1, 2], (0, 1, 1): [1, 2]}
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(mapping, expected)
```

### Step 5: Assign mapping = streamline_mapping(...)

```python
mapping = streamline_mapping(streamlines, affine=np.eye(4), mapping_as_streamlines=True)
```

### Step 6: Assign expected = value

```python
expected = {k: [streamlines[i] for i in indices] for k, indices in expected.items()}
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(mapping, expected)
```

### Step 8: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 9: Assign unknown = 0.5

```python
affine[:3, 3] = 0.5
```

### Step 10: Assign mapping = streamline_mapping(...)

```python
mapping = streamline_mapping(streamlines, affine=affine, mapping_as_streamlines=True)
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal(mapping, expected)
```

### Step 12: Assign affine = np.diag(...)

```python
affine = np.diag([0.5, 0.5, 0.5, 1.0])
```

### Step 13: Assign unknown = 0.25

```python
affine[:3, 3] = 0.25
```

### Step 14: Assign expected = value

```python
expected = {tuple((i * 2 for i in key)): value for key, value in expected.items()}
```

### Step 15: Assign mapping = streamline_mapping(...)

```python
mapping = streamline_mapping(streamlines, affine=affine, mapping_as_streamlines=True)
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(mapping, expected)
```


## Complete Example

```python
# Workflow
streamlines = [np.array([[0, 0, 0], [0, 0, 0], [0, 2, 2]], 'float'), np.array([[0, 0, 0], [0, 1, 1], [0, 2, 2]], 'float'), np.array([[0, 2, 2], [0, 1, 1], [0, 0, 0]], 'float')]
mapping = streamline_mapping(streamlines, affine=np.eye(4))
expected = {(0, 0, 0): [0, 1, 2], (0, 2, 2): [0, 1, 2], (0, 1, 1): [1, 2]}
npt.assert_equal(mapping, expected)
mapping = streamline_mapping(streamlines, affine=np.eye(4), mapping_as_streamlines=True)
expected = {k: [streamlines[i] for i in indices] for k, indices in expected.items()}
npt.assert_equal(mapping, expected)
affine = np.eye(4)
affine[:3, 3] = 0.5
mapping = streamline_mapping(streamlines, affine=affine, mapping_as_streamlines=True)
npt.assert_equal(mapping, expected)
affine = np.diag([0.5, 0.5, 0.5, 1.0])
affine[:3, 3] = 0.25
expected = {tuple((i * 2 for i in key)): value for key, value in expected.items()}
mapping = streamline_mapping(streamlines, affine=affine, mapping_as_streamlines=True)
npt.assert_equal(mapping, expected)
```

## Next Steps


---

*Source: test_utils.py:608 | Complexity: Advanced | Last updated: 2026-05-18*