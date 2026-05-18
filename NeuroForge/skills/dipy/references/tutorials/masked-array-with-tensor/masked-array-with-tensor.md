# How To: Masked Array With Tensor

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test masked array with tensor

## Prerequisites

**Required Modules:**
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign data = np.ones(...)

```python
data = np.ones((2, 4, 56))
```

### Step 2: Assign mask = np.array(...)

```python
mask = np.array([[True, False, False, True], [True, False, True, False]])
```

### Step 3: Assign unknown = read_bvals_bvecs(...)

```python
bval, bvec = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
```

### Step 4: Assign gtab = grad.gradient_table_from_bvals_bvecs(...)

```python
gtab = grad.gradient_table_from_bvals_bvecs(bval, bvec)
```

### Step 5: Assign tensor_model = TensorModel(...)

```python
tensor_model = TensorModel(gtab, return_leverages=True)
```

### Step 6: Assign tensor = tensor_model.fit(...)

```python
tensor = tensor_model.fit(data, mask=mask)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(tensor.shape, (2, 4))
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(tensor.fa.shape, (2, 4))
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(tensor.evals.shape, (2, 4, 3))
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(tensor.evecs.shape, (2, 4, 3, 3))
```

### Step 11: Assign tensor = value

```python
tensor = tensor[0]
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(tensor.shape, (4,))
```

### Step 13: Call npt.assert_equal()

```python
npt.assert_equal(tensor.fa.shape, (4,))
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(tensor.evals.shape, (4, 3))
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(tensor.evecs.shape, (4, 3, 3))
```

### Step 16: Assign tensor = value

```python
tensor = tensor[0]
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(tensor.shape, ())
```

### Step 18: Call npt.assert_equal()

```python
npt.assert_equal(tensor.fa.shape, ())
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(tensor.evals.shape, (3,))
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(tensor.evecs.shape, (3, 3))
```

### Step 21: Call npt.assert_equal()

```python
npt.assert_equal(type(tensor.model_params), np.ndarray)
```


## Complete Example

```python
# Workflow
data = np.ones((2, 4, 56))
mask = np.array([[True, False, False, True], [True, False, True, False]])
bval, bvec = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
gtab = grad.gradient_table_from_bvals_bvecs(bval, bvec)
tensor_model = TensorModel(gtab, return_leverages=True)
tensor = tensor_model.fit(data, mask=mask)
npt.assert_equal(tensor.shape, (2, 4))
npt.assert_equal(tensor.fa.shape, (2, 4))
npt.assert_equal(tensor.evals.shape, (2, 4, 3))
npt.assert_equal(tensor.evecs.shape, (2, 4, 3, 3))
tensor = tensor[0]
npt.assert_equal(tensor.shape, (4,))
npt.assert_equal(tensor.fa.shape, (4,))
npt.assert_equal(tensor.evals.shape, (4, 3))
npt.assert_equal(tensor.evecs.shape, (4, 3, 3))
tensor = tensor[0]
npt.assert_equal(tensor.shape, ())
npt.assert_equal(tensor.fa.shape, ())
npt.assert_equal(tensor.evals.shape, (3,))
npt.assert_equal(tensor.evecs.shape, (3, 3))
npt.assert_equal(type(tensor.model_params), np.ndarray)
```

## Next Steps


---

*Source: test_dti.py:586 | Complexity: Advanced | Last updated: 2026-05-18*