# How To: Low Level Fixed Effects

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test low level fixed effects

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `sklearn.datasets`
- `sklearn.linear_model`
- `nilearn.glm.contrasts`
- `nilearn.glm.first_level`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign p = 100

```python
p = 100
```

**Verification:**
```python
assert_almost_equal(Xf, 1.5 * X1)
```

### Step 2: Assign unknown = value

```python
X1, V1 = (rng.standard_normal(p), np.ones(p))
```

**Verification:**
```python
assert_almost_equal(Vf, 1.25 * V1)
```

### Step 3: Assign unknown = value

```python
X2, V2 = (2 * X1, 4 * V1)
```

**Verification:**
```python
assert_almost_equal(tf, (Xf / np.sqrt(Vf)).ravel())
```

### Step 4: Assign unknown = _compute_fixed_effects_params(...)

```python
Xf, Vf, tf, zf = _compute_fixed_effects_params([X1, X2], [V1, V2], dofs=[100, 100], precision_weighted=False)
```

**Verification:**
```python
assert_almost_equal(zf, st.norm.isf(st.t.sf(tf, 200)))
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(Xf, 1.5 * X1)
```

**Verification:**
```python
assert_almost_equal(Xw, 1.2 * X1)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(Vf, 1.25 * V1)
```

**Verification:**
```python
assert_almost_equal(Vw, 0.8 * V1)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(tf, (Xf / np.sqrt(Vf)).ravel())
```

**Verification:**
```python
assert_almost_equal(Xw, 1.5 * XX1)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(zf, st.norm.isf(st.t.sf(tf, 200)))
```

**Verification:**
```python
assert_almost_equal(Vw, 1.25 * V1)
```

### Step 9: Assign unknown = _compute_fixed_effects_params(...)

```python
Xw, Vw, _, _ = _compute_fixed_effects_params([X1, X2], [V1, V2], dofs=[200, 200], precision_weighted=True)
```

**Verification:**
```python
assert_almost_equal(Xw, 1.5 * X1[:, np.newaxis])
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(Xw, 1.2 * X1)
```

**Verification:**
```python
assert_almost_equal(Vw, 1.25 * V1)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(Vw, 0.8 * V1)
```

### Step 12: Assign XX1 = np.vstack(...)

```python
XX1 = np.vstack((X1, X1))
```

### Step 13: Assign XX2 = np.vstack(...)

```python
XX2 = np.vstack((X2, X2))
```

### Step 14: Assign unknown = _compute_fixed_effects_params(...)

```python
Xw, Vw, *_ = _compute_fixed_effects_params([XX1, XX2], [V1, V2], dofs=[200, 200], precision_weighted=False)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(Xw, 1.5 * XX1)
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(Vw, 1.25 * V1)
```

### Step 17: Assign unknown = _compute_fixed_effects_params(...)

```python
Xw, Vw, *_ = _compute_fixed_effects_params([X1[:, np.newaxis], X2[:, np.newaxis]], [V1, V2], dofs=[200, 200], precision_weighted=False)
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(Xw, 1.5 * X1[:, np.newaxis])
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(Vw, 1.25 * V1)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
p = 100
X1, V1 = (rng.standard_normal(p), np.ones(p))
X2, V2 = (2 * X1, 4 * V1)
Xf, Vf, tf, zf = _compute_fixed_effects_params([X1, X2], [V1, V2], dofs=[100, 100], precision_weighted=False)
assert_almost_equal(Xf, 1.5 * X1)
assert_almost_equal(Vf, 1.25 * V1)
assert_almost_equal(tf, (Xf / np.sqrt(Vf)).ravel())
assert_almost_equal(zf, st.norm.isf(st.t.sf(tf, 200)))
Xw, Vw, _, _ = _compute_fixed_effects_params([X1, X2], [V1, V2], dofs=[200, 200], precision_weighted=True)
assert_almost_equal(Xw, 1.2 * X1)
assert_almost_equal(Vw, 0.8 * V1)
XX1 = np.vstack((X1, X1))
XX2 = np.vstack((X2, X2))
Xw, Vw, *_ = _compute_fixed_effects_params([XX1, XX2], [V1, V2], dofs=[200, 200], precision_weighted=False)
assert_almost_equal(Xw, 1.5 * XX1)
assert_almost_equal(Vw, 1.25 * V1)
Xw, Vw, *_ = _compute_fixed_effects_params([X1[:, np.newaxis], X2[:, np.newaxis]], [V1, V2], dofs=[200, 200], precision_weighted=False)
assert_almost_equal(Xw, 1.5 * X1[:, np.newaxis])
assert_almost_equal(Vw, 1.25 * V1)
```

## Next Steps


---

*Source: test_contrasts.py:190 | Complexity: Advanced | Last updated: 2026-05-18*