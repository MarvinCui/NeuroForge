# How To: Add Noise

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test add noise

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dti`
- `dipy.sims.phantom`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign N = 50

```python
N = 50
```

**Verification:**
```python
assert_(np.abs(np.var(vol_noise - vol) - sigma ** 2) < 1)
```

### Step 2: Assign S0 = 100

```python
S0 = 100
```

### Step 3: Assign options = value

```python
options = {'func': f, 't': np.linspace(0, 2 * np.pi, N), 'datashape': (10, 10, 10, len(bvals)), 'origin': (5, 5, 5), 'scale': (3, 3, 3), 'angles': np.linspace(0, 2 * np.pi, 16), 'radii': np.linspace(0.2, 2, 6), 'S0': S0, 'rng': rng}
```

### Step 4: Assign vol = orbital_phantom(...)

```python
vol = orbital_phantom(gtab=gtab, **options)
```

### Step 5: Assign vol_noise = orbital_phantom(...)

```python
vol_noise = orbital_phantom(gtab=gtab, snr=snr, **options)
```

### Step 6: Assign sigma = value

```python
sigma = S0 / snr
```

### Step 7: Call assert_()

```python
assert_(np.abs(np.var(vol_noise - vol) - sigma ** 2) < 1)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
N = 50
S0 = 100
options = {'func': f, 't': np.linspace(0, 2 * np.pi, N), 'datashape': (10, 10, 10, len(bvals)), 'origin': (5, 5, 5), 'scale': (3, 3, 3), 'angles': np.linspace(0, 2 * np.pi, 16), 'radii': np.linspace(0.2, 2, 6), 'S0': S0, 'rng': rng}
vol = orbital_phantom(gtab=gtab, **options)
for snr in [10, 20, 30, 50]:
    vol_noise = orbital_phantom(gtab=gtab, snr=snr, **options)
    sigma = S0 / snr
    assert_(np.abs(np.var(vol_noise - vol) - sigma ** 2) < 1)
```

## Next Steps


---

*Source: test_phantom.py:60 | Complexity: Intermediate | Last updated: 2026-05-18*