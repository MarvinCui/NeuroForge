# How To: Mcsd Model Delta

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mcsd model delta

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

### Step 2: Assign gtab = get_3shell_gtab(...)

```python
gtab = get_3shell_gtab()
```

### Step 3: Assign iso = value

```python
iso = response.iso
```

### Step 4: Assign unknown = value

```python
theta, phi = (default_sphere.theta, default_sphere.phi)
```

### Step 5: Assign wm_delta = model.delta.copy(...)

```python
wm_delta = model.delta.copy()
```

### Step 6: Assign unknown = 0.0

```python
wm_delta[:iso] = 0.0
```

### Step 7: Assign wm_delta = _expand(...)

```python
wm_delta = _expand(model.m_values, iso, wm_delta)
```

### Step 8: Assign fit = model.fit(...)

```python
fit = model.fit(signal)
```

### Step 9: Assign m = value

```python
m = model.m_values
```

### Step 10: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(fit.shm_coeff[m != 0], 0.0, 2)
```

### Step 11: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 12: Assign response = multi_shell_fiber_response(...)

```python
response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
```

### Step 13: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 14: Assign model = MultiShellDeconvModel(...)

```python
model = MultiShellDeconvModel(gtab, response)
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 16: Assign B = shm.real_sh_descoteaux_from_index(...)

```python
B = shm.real_sh_descoteaux_from_index(response.m_values, response.l_values, theta[:, None], phi[:, None])
```

### Step 17: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 18: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 19: Assign signal = model.predict(...)

```python
signal = model.predict(wm_delta, gtab=gtab)
```

### Step 20: Assign g = GradientTable(...)

```python
g = GradientTable(default_sphere.vertices * s)
```

### Step 21: Assign signal = model.predict(...)

```python
signal = model.predict(wm_delta, gtab=g)
```

### Step 22: Assign expected = np.dot(...)

```python
expected = np.dot(response.response[i, iso:], B.T)
```

### Step 23: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(signal, expected)
```


## Complete Example

```python
# Workflow
sh_order_max = 8
gtab = get_3shell_gtab()
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model = MultiShellDeconvModel(gtab, response)
iso = response.iso
theta, phi = (default_sphere.theta, default_sphere.phi)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    B = shm.real_sh_descoteaux_from_index(response.m_values, response.l_values, theta[:, None], phi[:, None])
wm_delta = model.delta.copy()
wm_delta[:iso] = 0.0
wm_delta = _expand(model.m_values, iso, wm_delta)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    for i, s in enumerate([0, 1000, 2000, 3500]):
        g = GradientTable(default_sphere.vertices * s)
        signal = model.predict(wm_delta, gtab=g)
        expected = np.dot(response.response[i, iso:], B.T)
        npt.assert_array_almost_equal(signal, expected)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    signal = model.predict(wm_delta, gtab=gtab)
fit = model.fit(signal)
m = model.m_values
npt.assert_array_almost_equal(fit.shm_coeff[m != 0], 0.0, 2)
```

## Next Steps


---

*Source: test_mcsd.py:74 | Complexity: Advanced | Last updated: 2026-05-18*