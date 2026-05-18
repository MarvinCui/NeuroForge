# How To: Phantom

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test phantom

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dti`
- `dipy.sims.phantom`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign N = 50

```python
N = 50
```

**Verification:**
```python
assert_array_almost_equal(FA.max(), expected_fa, decimal=2)
```

### Step 2: Assign vol = orbital_phantom(...)

```python
vol = orbital_phantom(gtab=gtab, func=f, t=np.linspace(0, 2 * np.pi, N), datashape=(10, 10, 10, len(bvals)), origin=(5, 5, 5), scale=(3, 3, 3), angles=np.linspace(0, 2 * np.pi, 16), radii=np.linspace(0.2, 2, 6), S0=100)
```

### Step 3: Assign m = TensorModel(...)

```python
m = TensorModel(gtab)
```

### Step 4: Assign t = m.fit(...)

```python
t = m.fit(vol)
```

### Step 5: Assign FA = value

```python
FA = t.fa
```

### Step 6: Assign unknown = 0

```python
FA[np.isnan(FA)] = 0
```

### Step 7: Assign unknown = value

```python
l1, l2, l3 = (0.0015, 0.0004, 0.0004)
```

### Step 8: Assign expected_fa = value

```python
expected_fa = np.sqrt(0.5) * np.sqrt((l1 - l2) ** 2 + (l2 - l3) ** 2 + (l3 - l1) ** 2) / np.sqrt(l1 ** 2 + l2 ** 2 + l3 ** 2)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(FA.max(), expected_fa, decimal=2)
```


## Complete Example

```python
# Workflow
N = 50
vol = orbital_phantom(gtab=gtab, func=f, t=np.linspace(0, 2 * np.pi, N), datashape=(10, 10, 10, len(bvals)), origin=(5, 5, 5), scale=(3, 3, 3), angles=np.linspace(0, 2 * np.pi, 16), radii=np.linspace(0.2, 2, 6), S0=100)
m = TensorModel(gtab)
t = m.fit(vol)
FA = t.fa
FA[np.isnan(FA)] = 0
l1, l2, l3 = (0.0015, 0.0004, 0.0004)
expected_fa = np.sqrt(0.5) * np.sqrt((l1 - l2) ** 2 + (l2 - l3) ** 2 + (l3 - l1) ** 2) / np.sqrt(l1 ** 2 + l2 ** 2 + l3 ** 2)
assert_array_almost_equal(FA.max(), expected_fa, decimal=2)
```

## Next Steps


---

*Source: test_phantom.py:28 | Complexity: Advanced | Last updated: 2026-05-18*