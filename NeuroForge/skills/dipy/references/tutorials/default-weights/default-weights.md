# How To: Default Weights

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: test default weights

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `importlib`
- `sys`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: Assign file_path = get_fnames(...)

```python
file_path = get_fnames(name='evac_test_data')
```

### Step 2: Assign input_arr = value

```python
input_arr = np.load(file_path)['input'][0]
```

### Step 3: Assign output_arr = value

```python
output_arr = np.load(file_path)['output'][0]
```

### Step 4: Call monkeypatch.setenv()

```python
monkeypatch.setenv('DIPY_NN_BACKEND', backend)
```

### Step 5: Assign evac_model = evac.EVACPlus(...)

```python
evac_model = evac.EVACPlus()
```

### Step 6: Assign results_arr = evac_model.predict(...)

```python
results_arr = evac_model.predict(input_arr, np.eye(4), return_prob=True)
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(results_arr, output_arr, decimal=2)
```

### Step 8: Assign msg = '.*uses TensorFlow.*install PyTorch.*'

```python
msg = '.*uses TensorFlow.*install PyTorch.*'
```

### Step 9: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=DeprecationWarning)
```

### Step 10: Assign dipy_nn = importlib.reload(...)

```python
dipy_nn = importlib.reload(sys.modules['dipy.nn'])
```

### Step 11: Assign evac = value

```python
evac = dipy_nn.evac
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
file_path = get_fnames(name='evac_test_data')
input_arr = np.load(file_path)['input'][0]
output_arr = np.load(file_path)['output'][0]
for backend in BACKENDS:
    monkeypatch.setenv('DIPY_NN_BACKEND', backend)
    with warnings.catch_warnings():
        msg = '.*uses TensorFlow.*install PyTorch.*'
        warnings.filterwarnings('ignore', message=msg, category=DeprecationWarning)
        dipy_nn = importlib.reload(sys.modules['dipy.nn'])
        evac = dipy_nn.evac
    evac_model = evac.EVACPlus()
    results_arr = evac_model.predict(input_arr, np.eye(4), return_prob=True)
    npt.assert_almost_equal(results_arr, output_arr, decimal=2)
```

## Next Steps


---

*Source: test_evac.py:23 | Complexity: Advanced | Last updated: 2026-05-18*