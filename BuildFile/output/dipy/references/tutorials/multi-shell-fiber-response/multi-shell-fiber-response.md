# How To: Multi Shell Fiber Response

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multi shell fiber response

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

### Step 1: Assign sh_order_max = 8

```python
sh_order_max = 8
```

### Step 2: Call npt.assert_equal()

```python
npt.assert_equal(response.response.shape, (4, 7))
```

### Step 3: Assign btens = value

```python
btens = ['LTE', 'PTE', 'STE', 'CTE']
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(response.response.shape, (4, 7))
```

### Step 5: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 6: Assign response = multi_shell_fiber_response(...)

```python
response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
```

### Step 7: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 8: Assign response = multi_shell_fiber_response(...)

```python
response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response, btens=btens)
```

### Step 9: Call warnings.simplefilter()

```python
warnings.simplefilter('always', category=PendingDeprecationWarning)
```

### Step 10: Assign response = multi_shell_fiber_response(...)

```python
response = multi_shell_fiber_response(sh_order_max, [1000, 2000, 3500], wm_response, gm_response, csf_response)
```

### Step 11: Call npt.assert_()

```python
npt.assert_(len(w) > 1)
```

### Step 12: Call npt.assert_()

```python
npt.assert_(issubclass(w[-1].category, UserWarning))
```

### Step 13: Call npt.assert_()

```python
npt.assert_('No b0 given. Proceeding either way.' in str(w[-1].message))
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(response.response.shape, (3, 7))
```


## Complete Example

```python
# Workflow
sh_order_max = 8
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
npt.assert_equal(response.response.shape, (4, 7))
btens = ['LTE', 'PTE', 'STE', 'CTE']
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response, btens=btens)
npt.assert_equal(response.response.shape, (4, 7))
with warnings.catch_warnings(record=True) as w:
    warnings.simplefilter('always', category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [1000, 2000, 3500], wm_response, gm_response, csf_response)
    npt.assert_(len(w) > 1)
    npt.assert_(issubclass(w[-1].category, UserWarning))
    npt.assert_('No b0 given. Proceeding either way.' in str(w[-1].message))
    npt.assert_equal(response.response.shape, (3, 7))
```

## Next Steps


---

*Source: test_mcsd.py:258 | Complexity: Advanced | Last updated: 2026-05-18*