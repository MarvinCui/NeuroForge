# How To: Convert Tensor

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test convert tensor

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.utils`


## Step-by-Step Guide

### Step 1: Assign tensor = np.array(...)

```python
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
```

### Step 2: Assign converted_tensor = convert_tensors(...)

```python
converted_tensor = convert_tensors(tensor, 'dipy', 'mrtrix')
```

### Step 3: Assign expected_tensor = np.array(...)

```python
expected_tensor = np.array([[[[1, 3, 6, 2, 4, 5]]]])
```

### Step 4: Call npt.assert_array_equal()

```python
npt.assert_array_equal(converted_tensor, expected_tensor)
```

### Step 5: Assign tensor = np.array(...)

```python
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
```

### Step 6: Assign converted_tensor = convert_tensors(...)

```python
converted_tensor = convert_tensors(tensor, 'mrtrix', 'ants')
```

### Step 7: Assign expected_tensor = np.array(...)

```python
expected_tensor = np.array([[[[[1, 4, 2, 5, 6, 3]]]]])
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(converted_tensor, expected_tensor)
```

### Step 9: Assign tensor = np.array(...)

```python
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
```

### Step 10: Assign converted_tensor = convert_tensors(...)

```python
converted_tensor = convert_tensors(tensor, 'ants', 'fsl')
```

### Step 11: Assign expected_tensor = np.array(...)

```python
expected_tensor = np.array([[[[1, 2, 4, 3, 5, 6]]]])
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(converted_tensor, expected_tensor)
```

### Step 13: Assign tensor = np.array(...)

```python
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
```

### Step 14: Assign converted_tensor = convert_tensors(...)

```python
converted_tensor = convert_tensors(tensor, 'fsl', 'dipy')
```

### Step 15: Assign expected_tensor = np.array(...)

```python
expected_tensor = np.array([[[[1, 2, 4, 3, 5, 6]]]])
```

### Step 16: Call npt.assert_array_equal()

```python
npt.assert_array_equal(converted_tensor, expected_tensor)
```

### Step 17: Assign tensor = np.array(...)

```python
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
```

### Step 18: Assign converted_tensor = convert_tensors(...)

```python
converted_tensor = convert_tensors(tensor, 'dipy', 'ants')
```

### Step 19: Assign expected_tensor = np.array(...)

```python
expected_tensor = np.array([[[[[1, 2, 3, 4, 5, 6]]]]])
```

### Step 20: Call npt.assert_array_equal()

```python
npt.assert_array_equal(converted_tensor, expected_tensor)
```

### Step 21: Assign tensor = np.array(...)

```python
tensor = np.array([[[[[1, 2, 3, 4, 5, 6]]]]])
```

### Step 22: Assign converted_tensor = convert_tensors(...)

```python
converted_tensor = convert_tensors(tensor, 'ants', 'dipy')
```

### Step 23: Assign expected_tensor = np.array(...)

```python
expected_tensor = np.array([1, 2, 3, 4, 5, 6])
```

### Step 24: Call npt.assert_array_equal()

```python
npt.assert_array_equal(converted_tensor, expected_tensor)
```

### Step 25: Assign tensor = np.array(...)

```python
tensor = np.array([[[[[1, 2, 3, 4, 5, 6]]]]])
```

### Step 26: Assign converted_tensor = convert_tensors(...)

```python
converted_tensor = convert_tensors(tensor, 'dipy', 'dipy')
```

### Step 27: Call npt.assert_array_equal()

```python
npt.assert_array_equal(converted_tensor, tensor)
```

### Step 28: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, convert_tensors, tensor, 'amico', 'dipy')
```

### Step 29: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, convert_tensors, tensor, 'dipy', 'amico')
```


## Complete Example

```python
# Workflow
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
converted_tensor = convert_tensors(tensor, 'dipy', 'mrtrix')
expected_tensor = np.array([[[[1, 3, 6, 2, 4, 5]]]])
npt.assert_array_equal(converted_tensor, expected_tensor)
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
converted_tensor = convert_tensors(tensor, 'mrtrix', 'ants')
expected_tensor = np.array([[[[[1, 4, 2, 5, 6, 3]]]]])
npt.assert_array_equal(converted_tensor, expected_tensor)
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
converted_tensor = convert_tensors(tensor, 'ants', 'fsl')
expected_tensor = np.array([[[[1, 2, 4, 3, 5, 6]]]])
npt.assert_array_equal(converted_tensor, expected_tensor)
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
converted_tensor = convert_tensors(tensor, 'fsl', 'dipy')
expected_tensor = np.array([[[[1, 2, 4, 3, 5, 6]]]])
npt.assert_array_equal(converted_tensor, expected_tensor)
tensor = np.array([[[[1, 2, 3, 4, 5, 6]]]])
converted_tensor = convert_tensors(tensor, 'dipy', 'ants')
expected_tensor = np.array([[[[[1, 2, 3, 4, 5, 6]]]]])
npt.assert_array_equal(converted_tensor, expected_tensor)
tensor = np.array([[[[[1, 2, 3, 4, 5, 6]]]]])
converted_tensor = convert_tensors(tensor, 'ants', 'dipy')
expected_tensor = np.array([1, 2, 3, 4, 5, 6])
npt.assert_array_equal(converted_tensor, expected_tensor)
tensor = np.array([[[[[1, 2, 3, 4, 5, 6]]]]])
converted_tensor = convert_tensors(tensor, 'dipy', 'dipy')
npt.assert_array_equal(converted_tensor, tensor)
npt.assert_raises(ValueError, convert_tensors, tensor, 'amico', 'dipy')
npt.assert_raises(ValueError, convert_tensors, tensor, 'dipy', 'amico')
```

## Next Steps


---

*Source: test_utils.py:56 | Complexity: Advanced | Last updated: 2026-05-18*