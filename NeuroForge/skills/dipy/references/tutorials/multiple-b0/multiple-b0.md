# How To: Multiple B0

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multiple b0

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

### Step 1: Assign signal = multi_tensor(...)

```python
signal = multi_tensor(gtab_with_multiple_b0, mevals, snr=None, S0=S0, fractions=[f * 100, 100 * (1 - f)])
```

### Step 2: Assign data_single = value

```python
data_single = signal[0]
```

### Step 3: Assign msg = 'Bounds for this fit have been set from experiments .*'

```python
msg = 'Bounds for this fit have been set from experiments .*'
```

### Step 4: Call ivim_model_multiple_b0.fit()

```python
ivim_model_multiple_b0.fit(data_single)
```

### Step 5: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=UserWarning)
```

### Step 6: Assign ivim_model_multiple_b0 = IvimModel(...)

```python
ivim_model_multiple_b0 = IvimModel(gtab_with_multiple_b0, fit_method='trr')
```


## Complete Example

```python
# Workflow
signal = multi_tensor(gtab_with_multiple_b0, mevals, snr=None, S0=S0, fractions=[f * 100, 100 * (1 - f)])
data_single = signal[0]
msg = 'Bounds for this fit have been set from experiments .*'
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=msg, category=UserWarning)
    ivim_model_multiple_b0 = IvimModel(gtab_with_multiple_b0, fit_method='trr')
ivim_model_multiple_b0.fit(data_single)
```

## Next Steps


---

*Source: test_ivim.py:445 | Complexity: Intermediate | Last updated: 2026-05-18*