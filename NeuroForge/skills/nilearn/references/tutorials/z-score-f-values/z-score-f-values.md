# How To: Z Score F Values

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test z score f values

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.linalg`
- `scipy.stats`
- `numpy.testing`
- `scipy.stats`
- `nilearn._utils.data_gen`
- `nilearn.glm._utils`
- `nilearn.glm.first_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign f_val = rng.f(...)

```python
f_val = rng.f(1, 48, size=10)
```

**Verification:**
```python
assert_array_almost_equal(z_score(p_val, one_minus_pvalue=cdf_val), z_val)
```

### Step 2: Assign p_val = sps.f.sf(...)

```python
p_val = sps.f.sf(f_val, 42, 10000000000.0)
```

**Verification:**
```python
assert_array_almost_equal(norm.sf(z_score(p_val)), p_val)
```

### Step 3: Assign cdf_val = sps.f.cdf(...)

```python
cdf_val = sps.f.cdf(f_val, 42, 10000000000.0)
```

**Verification:**
```python
assert_array_almost_equal(z_score(p, one_minus_pvalue=cdf), z)
```

### Step 4: Assign p_val = np.array(...)

```python
p_val = np.array(np.minimum(np.maximum(p_val, 1e-300), 1.0 - 1e-16))
```

### Step 5: Assign cdf_val = np.array(...)

```python
cdf_val = np.array(np.minimum(np.maximum(cdf_val, 1e-300), 1.0 - 1e-16))
```

### Step 6: Assign z_val_sf = norm.isf(...)

```python
z_val_sf = norm.isf(p_val)
```

### Step 7: Assign z_val_cdf = norm.ppf(...)

```python
z_val_cdf = norm.ppf(cdf_val)
```

### Step 8: Assign z_val = np.zeros(...)

```python
z_val = np.zeros(p_val.size)
```

### Step 9: Assign unknown = value

```python
z_val[np.atleast_1d(z_val_sf < 0)] = z_val_cdf[z_val_sf < 0]
```

### Step 10: Assign unknown = value

```python
z_val[np.atleast_1d(z_val_sf >= 0)] = z_val_sf[z_val_sf >= 0]
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(z_score(p_val, one_minus_pvalue=cdf_val), z_val)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(norm.sf(z_score(p_val)), p_val)
```

### Step 13: Assign p = sps.t.sf(...)

```python
p = sps.t.sf(t, 10000000000.0)
```

### Step 14: Assign cdf = sps.t.cdf(...)

```python
cdf = sps.t.cdf(t, 10000000000.0)
```

### Step 15: Assign z_sf = norm.isf(...)

```python
z_sf = norm.isf(p)
```

### Step 16: Assign z_cdf = norm.ppf(...)

```python
z_cdf = norm.ppf(cdf)
```

### Step 17: Assign z = value

```python
z = z_sf if p <= 0.5 else z_cdf
```

### Step 18: Call assert_array_almost_equal()

```python
assert_array_almost_equal(z_score(p, one_minus_pvalue=cdf), z)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
f_val = rng.f(1, 48, size=10)
p_val = sps.f.sf(f_val, 42, 10000000000.0)
cdf_val = sps.f.cdf(f_val, 42, 10000000000.0)
p_val = np.array(np.minimum(np.maximum(p_val, 1e-300), 1.0 - 1e-16))
cdf_val = np.array(np.minimum(np.maximum(cdf_val, 1e-300), 1.0 - 1e-16))
z_val_sf = norm.isf(p_val)
z_val_cdf = norm.ppf(cdf_val)
z_val = np.zeros(p_val.size)
z_val[np.atleast_1d(z_val_sf < 0)] = z_val_cdf[z_val_sf < 0]
z_val[np.atleast_1d(z_val_sf >= 0)] = z_val_sf[z_val_sf >= 0]
assert_array_almost_equal(z_score(p_val, one_minus_pvalue=cdf_val), z_val)
assert_array_almost_equal(norm.sf(z_score(p_val)), p_val)
for t in [33.75, -8.3]:
    p = sps.t.sf(t, 10000000000.0)
    cdf = sps.t.cdf(t, 10000000000.0)
    z_sf = norm.isf(p)
    z_cdf = norm.ppf(cdf)
    z = z_sf if p <= 0.5 else z_cdf
    assert_array_almost_equal(z_score(p, one_minus_pvalue=cdf), z)
```

## Next Steps


---

*Source: test_utils.py:75 | Complexity: Advanced | Last updated: 2026-05-18*