# How To: Outlier Funcs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test functions that define outliers.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dti`
- `dipy.reconst.weights_method`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test functions that define outliers.'

```python
'Test functions that define outliers.'
```

**Verification:**
```python
assert_equal(outlier[0], True)
```

### Step 2: Assign b0 = 1000.0

```python
b0 = 1000.0
```

**Verification:**
```python
assert_equal(outlier[1:], np.zeros_like(outlier[1:], dtype=bool))
```

### Step 3: Assign unknown = read_bvals_bvecs(...)

```python
bval, bvecs = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
```

**Verification:**
```python
assert_equal(outlier.sum(), Y.shape[0])
```

### Step 4: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(bval, bvecs=bvecs)
```

### Step 5: Assign B = value

```python
B = bval[1]
```

### Step 6: Assign D_orig = value

```python
D_orig = np.array([1.0, 1.0, 1.0, 0.0, 0.0, 1.0, -np.log(b0) * B]) / B
```

### Step 7: Assign design_matrix = dti.design_matrix(...)

```python
design_matrix = dti.design_matrix(gtab)
```

### Step 8: Assign log_pred_sig = np.dot(...)

```python
log_pred_sig = np.dot(design_matrix, D_orig)
```

### Step 9: Assign pred_sig = np.exp(...)

```python
pred_sig = np.exp(log_pred_sig)
```

### Step 10: Assign scale = 1

```python
scale = 1
```

### Step 11: Assign error = rng.normal(...)

```python
error = rng.normal(scale=scale, size=pred_sig.shape)
```

### Step 12: Assign Y = value

```python
Y = pred_sig + error
```

### Step 13: Assign unknown = MIN_POSITIVE_SIGNAL

```python
Y[Y < MIN_POSITIVE_SIGNAL] = MIN_POSITIVE_SIGNAL
```

### Step 14: Assign unknown = value

```python
Y[0] = Y[0] * 100
```

### Step 15: Assign residuals = value

```python
residuals = Y - pred_sig
```

### Step 16: Assign log_residuals = value

```python
log_residuals = np.log(Y) - log_pred_sig
```

### Step 17: Assign leverages = value

```python
leverages = np.ones_like(Y) * D_orig.shape[0] / Y.shape[0]
```

### Step 18: Assign C = scale

```python
C = scale
```

### Step 19: Assign outlier = outlier_func(...)

```python
outlier = outlier_func(residuals, log_residuals, pred_sig, design_matrix, leverages, C, cutoff=6)
```

### Step 20: Call assert_equal()

```python
assert_equal(outlier[0], True)
```

### Step 21: Call assert_equal()

```python
assert_equal(outlier[1:], np.zeros_like(outlier[1:], dtype=bool))
```

### Step 22: Assign outlier = outlier_func(...)

```python
outlier = outlier_func(residuals, log_residuals, pred_sig, design_matrix, leverages, C, cutoff=0.0)
```

### Step 23: Call assert_equal()

```python
assert_equal(outlier.sum(), Y.shape[0])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test functions that define outliers.'
b0 = 1000.0
bval, bvecs = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
gtab = grad.gradient_table(bval, bvecs=bvecs)
B = bval[1]
D_orig = np.array([1.0, 1.0, 1.0, 0.0, 0.0, 1.0, -np.log(b0) * B]) / B
design_matrix = dti.design_matrix(gtab)
log_pred_sig = np.dot(design_matrix, D_orig)
pred_sig = np.exp(log_pred_sig)
scale = 1
error = rng.normal(scale=scale, size=pred_sig.shape)
Y = pred_sig + error
Y[Y < MIN_POSITIVE_SIGNAL] = MIN_POSITIVE_SIGNAL
Y[0] = Y[0] * 100
residuals = Y - pred_sig
log_residuals = np.log(Y) - log_pred_sig
leverages = np.ones_like(Y) * D_orig.shape[0] / Y.shape[0]
C = scale
for outlier_func in [simple_cutoff, two_eyes_cutoff]:
    outlier = outlier_func(residuals, log_residuals, pred_sig, design_matrix, leverages, C, cutoff=6)
    assert_equal(outlier[0], True)
    assert_equal(outlier[1:], np.zeros_like(outlier[1:], dtype=bool))
    outlier = outlier_func(residuals, log_residuals, pred_sig, design_matrix, leverages, C, cutoff=0.0)
    assert_equal(outlier.sum(), Y.shape[0])
```

## Next Steps


---

*Source: test_weights_method.py:26 | Complexity: Advanced | Last updated: 2026-05-18*