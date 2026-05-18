# How To: Minmax Normalize

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test minmax normalize

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.reconst.odf`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign bvalue = 3000

```python
bvalue = 3000
```

**Verification:**
```python
assert_equal(odf2.max(), 1)
```

### Step 2: Assign S0 = 1

```python
S0 = 1
```

**Verification:**
```python
assert_equal(odf2.min(), 0)
```

### Step 3: Assign SNR = 100

```python
SNR = 100
```

**Verification:**
```python
assert_equal(odf3.max(), 1)
```

### Step 4: Assign sphere = get_sphere(...)

```python
sphere = get_sphere(name='symmetric362')
```

**Verification:**
```python
assert_equal(odf3.min(), 0)
```

### Step 5: Assign bvecs = np.concatenate(...)

```python
bvecs = np.concatenate(([[0, 0, 0]], sphere.vertices))
```

### Step 6: Assign bvals = value

```python
bvals = np.zeros(len(bvecs)) + bvalue
```

### Step 7: Assign unknown = 0

```python
bvals[0] = 0
```

### Step 8: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 9: Assign evals = np.array(...)

```python
evals = np.array(([0.0017, 0.0003, 0.0003], [0.0017, 0.0003, 0.0003]))
```

### Step 10: Call multi_tensor()

```python
multi_tensor(gtab, evals, S0=S0, angles=[(0, 0), (90, 0)], fractions=[50, 50], snr=SNR)
```

### Step 11: Assign odf = multi_tensor_odf(...)

```python
odf = multi_tensor_odf(sphere.vertices, evals, angles=[(0, 0), (90, 0)], fractions=[50, 50])
```

### Step 12: Assign odf2 = minmax_normalize(...)

```python
odf2 = minmax_normalize(odf)
```

### Step 13: Call assert_equal()

```python
assert_equal(odf2.max(), 1)
```

### Step 14: Call assert_equal()

```python
assert_equal(odf2.min(), 0)
```

### Step 15: Assign odf3 = np.empty(...)

```python
odf3 = np.empty(odf.shape)
```

### Step 16: Assign odf3 = minmax_normalize(...)

```python
odf3 = minmax_normalize(odf, out=odf3)
```

### Step 17: Call assert_equal()

```python
assert_equal(odf3.max(), 1)
```

### Step 18: Call assert_equal()

```python
assert_equal(odf3.min(), 0)
```


## Complete Example

```python
# Workflow
bvalue = 3000
S0 = 1
SNR = 100
sphere = get_sphere(name='symmetric362')
bvecs = np.concatenate(([[0, 0, 0]], sphere.vertices))
bvals = np.zeros(len(bvecs)) + bvalue
bvals[0] = 0
gtab = gradient_table(bvals, bvecs=bvecs)
evals = np.array(([0.0017, 0.0003, 0.0003], [0.0017, 0.0003, 0.0003]))
multi_tensor(gtab, evals, S0=S0, angles=[(0, 0), (90, 0)], fractions=[50, 50], snr=SNR)
odf = multi_tensor_odf(sphere.vertices, evals, angles=[(0, 0), (90, 0)], fractions=[50, 50])
odf2 = minmax_normalize(odf)
assert_equal(odf2.max(), 1)
assert_equal(odf2.min(), 0)
odf3 = np.empty(odf.shape)
odf3 = minmax_normalize(odf, out=odf3)
assert_equal(odf3.max(), 1)
assert_equal(odf3.min(), 0)
```

## Next Steps


---

*Source: test_odf.py:39 | Complexity: Advanced | Last updated: 2026-05-18*