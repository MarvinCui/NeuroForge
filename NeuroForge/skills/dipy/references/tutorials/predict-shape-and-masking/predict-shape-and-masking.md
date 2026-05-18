# How To: Predict Shape And Masking

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: test predict shape and masking

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `importlib`
- `sys`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.shm`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: Assign unknown = get_fnames(...)

```python
dwi_fname, bval_fname, bvec_fname = get_fnames(name='stanford_hardi')
```

**Verification:**
```python
assert_equal(mask, results_pos)
```

### Step 2: Assign unknown = load_nifti(...)

```python
data, _ = load_nifti(dwi_fname)
```

**Verification:**
```python
assert_equal(results_arr.shape[-1], 45)
```

### Step 3: Assign data = np.squeeze(...)

```python
data = np.squeeze(data)
```

### Step 4: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(bval_fname, bvec_fname)
```

### Step 5: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 6: Assign mask = np.zeros(...)

```python
mask = np.zeros(data.shape[0:3], dtype=bool)
```

### Step 7: Assign unknown = 1

```python
mask[38:40, 45:50, 35:40] = 1
```

### Step 8: Call monkeypatch.setenv()

```python
monkeypatch.setenv('DIPY_NN_BACKEND', backend)
```

### Step 9: Assign resdnn_model = resdnn.HistoResDNN(...)

```python
resdnn_model = resdnn.HistoResDNN()
```

### Step 10: Call resdnn_model.fetch_default_weights()

```python
resdnn_model.fetch_default_weights()
```

### Step 11: Assign results_pos = np.sum(...)

```python
results_pos = np.sum(results_arr, axis=-1, dtype=bool)
```

### Step 12: Call assert_equal()

```python
assert_equal(mask, results_pos)
```

### Step 13: Call assert_equal()

```python
assert_equal(results_arr.shape[-1], 45)
```

### Step 14: Assign msg = '.*uses TensorFlow.*install PyTorch.*'

```python
msg = '.*uses TensorFlow.*install PyTorch.*'
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=DeprecationWarning)
```

### Step 16: Assign dipy_nn = importlib.reload(...)

```python
dipy_nn = importlib.reload(sys.modules['dipy.nn'])
```

### Step 17: Assign resdnn = value

```python
resdnn = dipy_nn.histo_resdnn
```

### Step 18: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=tournier07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 19: Assign results_arr = resdnn_model.predict(...)

```python
results_arr = resdnn_model.predict(data, gtab, mask=mask)
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
dwi_fname, bval_fname, bvec_fname = get_fnames(name='stanford_hardi')
data, _ = load_nifti(dwi_fname)
data = np.squeeze(data)
bvals, bvecs = read_bvals_bvecs(bval_fname, bvec_fname)
gtab = gradient_table(bvals, bvecs=bvecs)
mask = np.zeros(data.shape[0:3], dtype=bool)
mask[38:40, 45:50, 35:40] = 1
for backend in BACKENDS:
    monkeypatch.setenv('DIPY_NN_BACKEND', backend)
    with warnings.catch_warnings():
        msg = '.*uses TensorFlow.*install PyTorch.*'
        warnings.filterwarnings('ignore', message=msg, category=DeprecationWarning)
        dipy_nn = importlib.reload(sys.modules['dipy.nn'])
        resdnn = dipy_nn.histo_resdnn
    resdnn_model = resdnn.HistoResDNN()
    resdnn_model.fetch_default_weights()
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', message=tournier07_legacy_msg, category=PendingDeprecationWarning)
        results_arr = resdnn_model.predict(data, gtab, mask=mask)
    results_pos = np.sum(results_arr, axis=-1, dtype=bool)
    assert_equal(mask, results_pos)
    assert_equal(results_arr.shape[-1], 45)
```

## Next Steps


---

*Source: test_histo_resdnn.py:149 | Complexity: Advanced | Last updated: 2026-05-18*