# How To: Connectivity Matrix With Generator

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test connectivity_matrix works with generator inputs.

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

### Step 1: 'Test connectivity_matrix works with generator inputs.'

```python
'Test connectivity_matrix works with generator inputs.'
```

### Step 2: Assign label_volume = np.array(...)

```python
label_volume = np.array([[[3, 0, 0], [0, 0, 5], [0, 0, 4]]])
```

### Step 3: Assign streamlines = value

```python
streamlines = [np.array([[0, 0, 0], [0, 1, 2], [0, 2, 2]], 'float'), np.array([[0, 0, 0], [0, 1, 1], [0, 2, 2]], 'float'), np.array([[0, 2, 2], [0, 1, 1], [0, 0, 0]], 'float')]
```

### Step 4: Assign matrix = connectivity_matrix(...)

```python
matrix = connectivity_matrix(streamline_generator(), np.eye(4), label_volume, symmetric=False)
```

### Step 5: Assign expected = np.zeros(...)

```python
expected = np.zeros((6, 6), 'int')
```

### Step 6: Assign unknown = 2

```python
expected[3, 4] = 2
```

### Step 7: Assign unknown = 1

```python
expected[4, 3] = 1
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(matrix, expected)
```

### Step 9: Assign matrix = connectivity_matrix(...)

```python
matrix = connectivity_matrix(streamline_generator(), np.eye(4), label_volume, symmetric=False, discard_stream_size=1)
```

### Step 10: Call npt.assert_array_equal()

```python
npt.assert_array_equal(matrix, expected)
```

### Step 11: Assign expected_inclusive = np.zeros(...)

```python
expected_inclusive = np.zeros((6, 6), 'int')
```

### Step 12: Assign unknown = 2

```python
expected_inclusive[3, 4] = 2
```

### Step 13: Assign unknown = 1

```python
expected_inclusive[4, 3] = 1
```

### Step 14: Assign unknown = 1

```python
expected_inclusive[3, 5] = 1
```

### Step 15: Assign unknown = 1

```python
expected_inclusive[5, 4] = 1
```

### Step 16: Assign unknown = 1

```python
expected_inclusive[0, 3:5] = 1
```

### Step 17: Assign unknown = 1

```python
expected_inclusive[3:5, 0] = 1
```

### Step 18: Assign matrix = connectivity_matrix(...)

```python
matrix = connectivity_matrix(streamline_generator(), np.eye(4), label_volume, symmetric=False, inclusive=True, discard_stream_size=1)
```

### Step 19: Call npt.assert_array_equal()

```python
npt.assert_array_equal(matrix, expected_inclusive)
```

### Step 20: yield from streamlines

```python
yield from streamlines
```


## Complete Example

```python
# Workflow
'Test connectivity_matrix works with generator inputs.'
label_volume = np.array([[[3, 0, 0], [0, 0, 5], [0, 0, 4]]])
streamlines = [np.array([[0, 0, 0], [0, 1, 2], [0, 2, 2]], 'float'), np.array([[0, 0, 0], [0, 1, 1], [0, 2, 2]], 'float'), np.array([[0, 2, 2], [0, 1, 1], [0, 0, 0]], 'float')]

def streamline_generator():
    yield from streamlines
matrix = connectivity_matrix(streamline_generator(), np.eye(4), label_volume, symmetric=False)
expected = np.zeros((6, 6), 'int')
expected[3, 4] = 2
expected[4, 3] = 1
npt.assert_array_equal(matrix, expected)
matrix = connectivity_matrix(streamline_generator(), np.eye(4), label_volume, symmetric=False, discard_stream_size=1)
npt.assert_array_equal(matrix, expected)
expected_inclusive = np.zeros((6, 6), 'int')
expected_inclusive[3, 4] = 2
expected_inclusive[4, 3] = 1
expected_inclusive[3, 5] = 1
expected_inclusive[5, 4] = 1
expected_inclusive[0, 3:5] = 1
expected_inclusive[3:5, 0] = 1
matrix = connectivity_matrix(streamline_generator(), np.eye(4), label_volume, symmetric=False, inclusive=True, discard_stream_size=1)
npt.assert_array_equal(matrix, expected_inclusive)
```

## Next Steps


---

*Source: test_utils.py:265 | Complexity: Advanced | Last updated: 2026-05-18*