# How To: Dki Crossing Fibers Simulations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Testing DKI simulations of a crossing fiber

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.sims.voxel`
- `dipy.testing.decorators`
- `dipy.reconst.dti`


## Step-by-Step Guide

### Step 1: 'Testing DKI simulations of a crossing fiber'

```python
'Testing DKI simulations of a crossing fiber'
```

**Verification:**
```python
assert dt[i] != 0
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087], [0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
```

**Verification:**
```python
assert kt[i] != 0
```

### Step 3: Assign angles = value

```python
angles = [(80, 10), (80, 10), (20, 30), (20, 30)]
```

**Verification:**
```python
assert_array_almost_equal(dt, dt_ref)
```

### Step 4: Assign fie = 0.49

```python
fie = 0.49
```

**Verification:**
```python
assert_array_almost_equal(kt, kt_ref)
```

### Step 5: Assign frac = value

```python
frac = [fie * 50, (1 - fie) * 50, fie * 50, (1 - fie) * 50]
```

**Verification:**
```python
assert_array_almost_equal(signal, dki_signal(gtab_2s, dt_ref, kt_ref, S0=1.0, snr=None), decimal=5)
```

### Step 6: Assign unknown = multi_tensor_dki(...)

```python
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
```

### Step 7: Assign dt_ref = value

```python
dt_ref = [0.0010576161, 0.0001292542, 0.0004786179, 0.0002667081, 0.0001136643, 0.000988866]
```

### Step 8: Assign kt_ref = value

```python
kt_ref = [2.3529944, 0.8226448, 2.3011221, 0.2017312, -0.0437535, 0.0404011, 0.0355281, 0.2449859, 0.2157668, 0.349591, 0.0413366, 0.3461519, -0.0537046, 0.0133414, -0.017441]
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(dt, dt_ref)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(kt, kt_ref)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(signal, dki_signal(gtab_2s, dt_ref, kt_ref, S0=1.0, snr=None), decimal=5)
```

**Verification:**
```python
assert dt[i] != 0
```


## Complete Example

```python
# Workflow
'Testing DKI simulations of a crossing fiber'
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087], [0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
angles = [(80, 10), (80, 10), (20, 30), (20, 30)]
fie = 0.49
frac = [fie * 50, (1 - fie) * 50, fie * 50, (1 - fie) * 50]
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
for i in range(len(dt)):
    assert dt[i] != 0
for i in range(len(kt)):
    assert kt[i] != 0
dt_ref = [0.0010576161, 0.0001292542, 0.0004786179, 0.0002667081, 0.0001136643, 0.000988866]
kt_ref = [2.3529944, 0.8226448, 2.3011221, 0.2017312, -0.0437535, 0.0404011, 0.0355281, 0.2449859, 0.2157668, 0.349591, 0.0413366, 0.3461519, -0.0537046, 0.0133414, -0.017441]
assert_array_almost_equal(dt, dt_ref)
assert_array_almost_equal(kt, kt_ref)
assert_array_almost_equal(signal, dki_signal(gtab_2s, dt_ref, kt_ref, S0=1.0, snr=None), decimal=5)
```

## Next Steps


---

*Source: test_voxel.py:331 | Complexity: Advanced | Last updated: 2026-05-18*