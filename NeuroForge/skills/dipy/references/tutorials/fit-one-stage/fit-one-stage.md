# How To: Fit One Stage

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test to check the results for the one_stage linear fit.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.reconst.ivim`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: '\n    Test to check the results for the one_stage linear fit.\n    '

```python
'\n    Test to check the results for the one_stage linear fit.\n    '
```

**Verification:**
```python
assert_array_almost_equal(fit.model_params, linear_fit_params)
```

### Step 2: Assign msg = 'Bounds for this fit have been set from experiments .*'

```python
msg = 'Bounds for this fit have been set from experiments .*'
```

**Verification:**
```python
assert_array_almost_equal(fit.predict(gtab), linear_fit_signal)
```

### Step 3: Assign fit = model.fit(...)

```python
fit = model.fit(data_single)
```

### Step 4: Assign linear_fit_params = value

```python
linear_fit_params = [988.83414, 0.119707191, 0.0079117697, 0.00093009521]
```

### Step 5: Assign linear_fit_signal = value

```python
linear_fit_signal = [988.83414044, 971.77122546, 955.46786293, 939.87125905, 924.93258982, 896.85182201, 870.90346447, 846.81187693, 824.34108781, 803.28900104, 783.48245048, 764.77297789, 747.03322866, 669.54798887, 605.03328304, 549.00852235, 499.21077611, 454.40299244, 413.83192296, 376.98072773, 343.45531017]
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fit.model_params, linear_fit_params)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fit.predict(gtab), linear_fit_signal)
```

### Step 8: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=UserWarning)
```

### Step 9: Assign model = IvimModel(...)

```python
model = IvimModel(gtab, two_stage=False)
```


## Complete Example

```python
# Workflow
'\n    Test to check the results for the one_stage linear fit.\n    '
msg = 'Bounds for this fit have been set from experiments .*'
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=msg, category=UserWarning)
    model = IvimModel(gtab, two_stage=False)
fit = model.fit(data_single)
linear_fit_params = [988.83414, 0.119707191, 0.0079117697, 0.00093009521]
linear_fit_signal = [988.83414044, 971.77122546, 955.46786293, 939.87125905, 924.93258982, 896.85182201, 870.90346447, 846.81187693, 824.34108781, 803.28900104, 783.48245048, 764.77297789, 747.03322866, 669.54798887, 605.03328304, 549.00852235, 499.21077611, 454.40299244, 413.83192296, 376.98072773, 343.45531017]
assert_array_almost_equal(fit.model_params, linear_fit_params)
assert_array_almost_equal(fit.predict(gtab), linear_fit_signal)
```

## Next Steps


---

*Source: test_ivim.py:564 | Complexity: Advanced | Last updated: 2026-05-18*