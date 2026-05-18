# How To: Kurtosis Elements

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Testing symmetry of the elements of the KT

As an 4th order tensor, KT has 81 elements. However, due to diffusion
symmetry the KT is fully characterized by 15 independent elements. This
test checks for this property.

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

### Step 1: 'Testing symmetry of the elements of the KT\n\n    As an 4th order tensor, KT has 81 elements. However, due to diffusion\n    symmetry the KT is fully characterized by 15 independent elements. This\n    test checks for this property.\n    '

```python
'Testing symmetry of the elements of the KT\n\n    As an 4th order tensor, KT has 81 elements. However, due to diffusion\n    symmetry the KT is fully characterized by 15 independent elements. This\n    test checks for this property.\n    '
```

**Verification:**
```python
assert_almost_equal(kurtosis_element(mD, frac, i, k, j, ell), kt_ref[key])
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087], [0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
```

**Verification:**
```python
assert_almost_equal(kurtosis_element(mD, frac, i, k, j, ell), kurtosis_element(mD, frac, i, k, j, ell, DT=D, MD=MD))
```

### Step 3: Assign angles = value

```python
angles = [(80, 10), (80, 10), (20, 30), (20, 30)]
```

### Step 4: Assign fie = 0.49

```python
fie = 0.49
```

### Step 5: Assign frac = value

```python
frac = [fie * 50, (1 - fie) * 50, fie * 50, (1 - fie) * 50]
```

### Step 6: Assign sticks = _check_directions(...)

```python
sticks = _check_directions(angles)
```

### Step 7: Assign mD = np.zeros(...)

```python
mD = np.zeros((len(frac), 3, 3))
```

### Step 8: Assign D = np.zeros(...)

```python
D = np.zeros((3, 3))
```

### Step 9: Assign MD = value

```python
MD = (D[0][0] + D[1][1] + D[2][2]) / 3
```

### Step 10: Assign kt_ref = value

```python
kt_ref = {1: kurtosis_element(mD, frac, 0, 0, 0, 0), 16: kurtosis_element(mD, frac, 1, 1, 1, 1), 81: kurtosis_element(mD, frac, 2, 2, 2, 2), 2: kurtosis_element(mD, frac, 0, 0, 0, 1), 3: kurtosis_element(mD, frac, 0, 0, 0, 2), 8: kurtosis_element(mD, frac, 0, 1, 1, 1), 24: kurtosis_element(mD, frac, 1, 1, 1, 2), 27: kurtosis_element(mD, frac, 0, 2, 2, 2), 54: kurtosis_element(mD, frac, 1, 2, 2, 2), 4: kurtosis_element(mD, frac, 0, 0, 1, 1), 9: kurtosis_element(mD, frac, 0, 0, 2, 2), 36: kurtosis_element(mD, frac, 1, 1, 2, 2), 6: kurtosis_element(mD, frac, 0, 0, 1, 2), 12: kurtosis_element(mD, frac, 0, 1, 1, 2), 18: kurtosis_element(mD, frac, 0, 1, 2, 2)}
```

### Step 11: Assign xyz = value

```python
xyz = [0, 1, 2]
```

### Step 12: Assign R = all_tensor_evecs(...)

```python
R = all_tensor_evecs(sticks[i])
```

### Step 13: Assign unknown = np.dot(...)

```python
mD[i] = np.dot(np.dot(R, np.diag(mevals[i])), R.T)
```

### Step 14: Assign D = value

```python
D = D + frac[i] * mD[i]
```

### Step 15: Assign key = value

```python
key = (i + 1) * (j + 1) * (k + 1) * (ell + 1)
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(kurtosis_element(mD, frac, i, k, j, ell), kt_ref[key])
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(kurtosis_element(mD, frac, i, k, j, ell), kurtosis_element(mD, frac, i, k, j, ell, DT=D, MD=MD))
```


## Complete Example

```python
# Workflow
'Testing symmetry of the elements of the KT\n\n    As an 4th order tensor, KT has 81 elements. However, due to diffusion\n    symmetry the KT is fully characterized by 15 independent elements. This\n    test checks for this property.\n    '
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087], [0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
angles = [(80, 10), (80, 10), (20, 30), (20, 30)]
fie = 0.49
frac = [fie * 50, (1 - fie) * 50, fie * 50, (1 - fie) * 50]
sticks = _check_directions(angles)
mD = np.zeros((len(frac), 3, 3))
for i in range(len(frac)):
    R = all_tensor_evecs(sticks[i])
    mD[i] = np.dot(np.dot(R, np.diag(mevals[i])), R.T)
D = np.zeros((3, 3))
for i in range(len(frac)):
    D = D + frac[i] * mD[i]
MD = (D[0][0] + D[1][1] + D[2][2]) / 3
kt_ref = {1: kurtosis_element(mD, frac, 0, 0, 0, 0), 16: kurtosis_element(mD, frac, 1, 1, 1, 1), 81: kurtosis_element(mD, frac, 2, 2, 2, 2), 2: kurtosis_element(mD, frac, 0, 0, 0, 1), 3: kurtosis_element(mD, frac, 0, 0, 0, 2), 8: kurtosis_element(mD, frac, 0, 1, 1, 1), 24: kurtosis_element(mD, frac, 1, 1, 1, 2), 27: kurtosis_element(mD, frac, 0, 2, 2, 2), 54: kurtosis_element(mD, frac, 1, 2, 2, 2), 4: kurtosis_element(mD, frac, 0, 0, 1, 1), 9: kurtosis_element(mD, frac, 0, 0, 2, 2), 36: kurtosis_element(mD, frac, 1, 1, 2, 2), 6: kurtosis_element(mD, frac, 0, 0, 1, 2), 12: kurtosis_element(mD, frac, 0, 1, 1, 2), 18: kurtosis_element(mD, frac, 0, 1, 2, 2)}
xyz = [0, 1, 2]
for i in xyz:
    for j in xyz:
        for k in xyz:
            for ell in xyz:
                key = (i + 1) * (j + 1) * (k + 1) * (ell + 1)
                assert_almost_equal(kurtosis_element(mD, frac, i, k, j, ell), kt_ref[key])
                assert_almost_equal(kurtosis_element(mD, frac, i, k, j, ell), kurtosis_element(mD, frac, i, k, j, ell, DT=D, MD=MD))
```

## Next Steps


---

*Source: test_voxel.py:186 | Complexity: Advanced | Last updated: 2026-05-18*