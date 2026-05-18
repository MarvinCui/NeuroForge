# How To: Compute Microstructure Uncertainty Ambiguity

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test microstructure uncertainty and ambiguity metrics.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.force`


## Step-by-Step Guide

### Step 1: 'Test microstructure uncertainty and ambiguity metrics.'

```python
'Test microstructure uncertainty and ambiguity metrics.'
```

**Verification:**
```python
assert unc_narrow.shape == (2,)
```

### Step 2: Assign vals_narrow = np.array(...)

```python
vals_narrow = np.array([[0.5, 0.51, 0.49, 0.5, 0.5], [0.5, 0.51, 0.49, 0.5, 0.5]], dtype=np.float32)
```

**Verification:**
```python
assert amb_narrow.shape == (2,)
```

### Step 3: Assign weights_uniform = np.array(...)

```python
weights_uniform = np.array([[0.2, 0.2, 0.2, 0.2, 0.2], [0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
```

**Verification:**
```python
assert_array_less(unc_narrow, 0.5)
```

### Step 4: Assign prior_range = 1.0

```python
prior_range = 1.0
```

**Verification:**
```python
assert_array_less(amb_narrow, 0.5)
```

### Step 5: Assign unknown = compute_microstructure_uncertainty_ambiguity(...)

```python
unc_narrow, amb_narrow = compute_microstructure_uncertainty_ambiguity(vals_narrow, weights_uniform, prior_range)
```

**Verification:**
```python
assert unc_wide[0] > unc_narrow[0]
```

### Step 6: Call assert_array_less()

```python
assert_array_less(unc_narrow, 0.5)
```

**Verification:**
```python
assert amb_wide[0] > amb_narrow[0]
```

### Step 7: Call assert_array_less()

```python
assert_array_less(amb_narrow, 0.5)
```

**Verification:**
```python
assert np.all(unc_wide >= 0)
```

### Step 8: Assign vals_wide = np.array(...)

```python
vals_wide = np.array([[0.0, 0.25, 0.5, 0.75, 1.0], [0.0, 0.25, 0.5, 0.75, 1.0]], dtype=np.float32)
```

**Verification:**
```python
assert np.all(amb_wide >= 0)
```

### Step 9: Assign unknown = compute_microstructure_uncertainty_ambiguity(...)

```python
unc_wide, amb_wide = compute_microstructure_uncertainty_ambiguity(vals_wide, weights_uniform, prior_range)
```

**Verification:**
```python
assert unc_conc[0] < unc_wide[0]
```

### Step 10: Assign weights_conc = np.array(...)

```python
weights_conc = np.array([[0.9, 0.025, 0.025, 0.025, 0.025], [0.9, 0.025, 0.025, 0.025, 0.025]], dtype=np.float32)
```

### Step 11: Assign unknown = compute_microstructure_uncertainty_ambiguity(...)

```python
unc_conc, amb_conc = compute_microstructure_uncertainty_ambiguity(vals_wide, weights_conc, prior_range)
```

**Verification:**
```python
assert unc_conc[0] < unc_wide[0]
```


## Complete Example

```python
# Workflow
'Test microstructure uncertainty and ambiguity metrics.'
vals_narrow = np.array([[0.5, 0.51, 0.49, 0.5, 0.5], [0.5, 0.51, 0.49, 0.5, 0.5]], dtype=np.float32)
weights_uniform = np.array([[0.2, 0.2, 0.2, 0.2, 0.2], [0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
prior_range = 1.0
unc_narrow, amb_narrow = compute_microstructure_uncertainty_ambiguity(vals_narrow, weights_uniform, prior_range)
assert unc_narrow.shape == (2,)
assert amb_narrow.shape == (2,)
assert_array_less(unc_narrow, 0.5)
assert_array_less(amb_narrow, 0.5)
vals_wide = np.array([[0.0, 0.25, 0.5, 0.75, 1.0], [0.0, 0.25, 0.5, 0.75, 1.0]], dtype=np.float32)
unc_wide, amb_wide = compute_microstructure_uncertainty_ambiguity(vals_wide, weights_uniform, prior_range)
assert unc_wide[0] > unc_narrow[0]
assert amb_wide[0] > amb_narrow[0]
assert np.all(unc_wide >= 0)
assert np.all(amb_wide >= 0)
weights_conc = np.array([[0.9, 0.025, 0.025, 0.025, 0.025], [0.9, 0.025, 0.025, 0.025, 0.025]], dtype=np.float32)
unc_conc, amb_conc = compute_microstructure_uncertainty_ambiguity(vals_wide, weights_conc, prior_range)
assert unc_conc[0] < unc_wide[0]
```

## Next Steps


---

*Source: test_force.py:166 | Complexity: Advanced | Last updated: 2026-05-18*