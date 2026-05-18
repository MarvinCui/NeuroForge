# How To: Multishelldeconvmodel Response

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test MultiShellDeconvModel response

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.reconst`
- `dipy.reconst.mcsd`
- `dipy.sims.voxel`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign gtab = get_3shell_gtab(...)

```python
gtab = get_3shell_gtab()
```

### Step 2: Assign sh_order_max = 8

```python
sh_order_max = 8
```

### Step 3: Assign responses = np.array(...)

```python
responses = np.array([wm_response, gm_response, csf_response])
```

### Step 4: Assign response_1 = value

```python
response_1 = model_1.response.response
```

### Step 5: Assign response_2 = value

```python
response_2 = model_2.response.response
```

### Step 6: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(response_1, response_2, 0)
```

### Step 7: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, MultiShellDeconvModel, gtab, np.ones((4, 3, 4)))
```

### Step 8: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, MultiShellDeconvModel, gtab, np.ones((3, 3, 4)), iso=3)
```

### Step 9: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 10: Assign response = multi_shell_fiber_response(...)

```python
response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
```

### Step 11: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 12: Assign model_1 = MultiShellDeconvModel(...)

```python
model_1 = MultiShellDeconvModel(gtab, response, sh_order_max=sh_order_max)
```

### Step 13: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 14: Assign model_2 = MultiShellDeconvModel(...)

```python
model_2 = MultiShellDeconvModel(gtab, responses, sh_order_max=sh_order_max)
```


## Complete Example

```python
# Workflow
gtab = get_3shell_gtab()
sh_order_max = 8
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model_1 = MultiShellDeconvModel(gtab, response, sh_order_max=sh_order_max)
responses = np.array([wm_response, gm_response, csf_response])
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model_2 = MultiShellDeconvModel(gtab, responses, sh_order_max=sh_order_max)
response_1 = model_1.response.response
response_2 = model_2.response.response
npt.assert_array_almost_equal(response_1, response_2, 0)
npt.assert_raises(ValueError, MultiShellDeconvModel, gtab, np.ones((4, 3, 4)))
npt.assert_raises(ValueError, MultiShellDeconvModel, gtab, np.ones((3, 3, 4)), iso=3)
```

## Next Steps


---

*Source: test_mcsd.py:136 | Complexity: Advanced | Last updated: 2026-05-18*