# How To: Nnls Jacobian Func

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nnls jacobian func

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign b0 = 1000.0

```python
b0 = 1000.0
```

**Verification:**
```python
assert True
```

### Step 2: Assign unknown = read_bvals_bvecs(...)

```python
bval, bvecs = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
```

### Step 3: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(bval, bvecs=bvecs)
```

### Step 4: Assign B = value

```python
B = bval[1]
```

### Step 5: Assign D_orig = value

```python
D_orig = np.array([1.0, 1.0, 1.0, 0.0, 0.0, 1.0, -np.log(b0) * B]) / B
```

### Step 6: Assign X = dti.design_matrix(...)

```python
X = dti.design_matrix(gtab)
```

### Step 7: Assign Y = np.exp(...)

```python
Y = np.exp(np.dot(X, D_orig))
```

### Step 8: Assign scale = 10

```python
scale = 10
```

### Step 9: Assign error = rng.normal(...)

```python
error = rng.normal(scale=scale, size=Y.shape)
```

### Step 10: Assign Y = value

```python
Y = Y + error
```

### Step 11: Assign nlls = dti._NllsHelper(...)

```python
nlls = dti._NllsHelper()
```

### Step 12: Assign sigma_scalar = value

```python
sigma_scalar = 1.4826 * np.median(np.abs(error - np.median(error)))
```

### Step 13: Assign sigma_array = np.full_like(...)

```python
sigma_array = np.full_like(Y, sigma_scalar)
```

### Step 14: Assign weights = value

```python
weights = 1 / sigma ** 2
```

### Step 15: Assign args = value

```python
args = [D, X, Y, weights]
```

### Step 16: Call nlls.err_func()

```python
nlls.err_func(*args)
```

### Step 17: Assign args = value

```python
args = [X[i], Y[i], weights]
```

**Verification:**
```python
assert True
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
b0 = 1000.0
bval, bvecs = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
gtab = grad.gradient_table(bval, bvecs=bvecs)
B = bval[1]
D_orig = np.array([1.0, 1.0, 1.0, 0.0, 0.0, 1.0, -np.log(b0) * B]) / B
X = dti.design_matrix(gtab)
Y = np.exp(np.dot(X, D_orig))
scale = 10
error = rng.normal(scale=scale, size=Y.shape)
Y = Y + error
nlls = dti._NllsHelper()
sigma_scalar = 1.4826 * np.median(np.abs(error - np.median(error)))
sigma_array = np.full_like(Y, sigma_scalar)
for sigma in [sigma_scalar, sigma_array]:
    weights = 1 / sigma ** 2
    for D in [D_orig, np.zeros_like(D_orig)]:
        args = [D, X, Y, weights]
        nlls.err_func(*args)
        for i in range(len(X)):
            args = [X[i], Y[i], weights]
            assert True
```

## Next Steps


---

*Source: test_dti.py:722 | Complexity: Advanced | Last updated: 2026-05-18*