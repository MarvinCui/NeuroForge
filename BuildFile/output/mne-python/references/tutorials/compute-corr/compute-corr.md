# How To: Compute Corr

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Anscombe's Quartett.

## Prerequisites

**Required Modules:**
- `copy`
- `datetime`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.time_frequency`
- `mne.utils`
- `mne.utils.numerics`
- `sklearn.decomposition`


## Step-by-Step Guide

### Step 1: "Test Anscombe's Quartett."

```python
"Test Anscombe's Quartett."
```

**Verification:**
```python
assert_allclose(r, r2)
```

### Step 2: Assign x = np.array(...)

```python
x = np.array([10, 8, 13, 9, 11, 14, 6, 4, 12, 7, 5])
```

### Step 3: Assign y = np.array(...)

```python
y = np.array([[8.04, 6.95, 7.58, 8.81, 8.33, 9.96, 7.24, 4.26, 10.84, 4.82, 5.68], [9.14, 8.14, 8.74, 8.77, 9.26, 8.1, 6.13, 3.1, 9.13, 7.26, 4.74], [7.46, 6.77, 12.74, 7.11, 7.81, 8.84, 6.08, 5.39, 8.15, 6.42, 5.73], [8, 8, 8, 8, 8, 8, 8, 19, 8, 8, 8], [6.58, 5.76, 7.71, 8.84, 8.47, 7.04, 5.25, 12.5, 5.56, 7.91, 6.89]])
```

### Step 4: Assign r = compute_corr(...)

```python
r = compute_corr(x, y.T)
```

### Step 5: Assign r2 = np.array(...)

```python
r2 = np.array([np.corrcoef(x, y[i])[0, 1] for i in range(len(y))])
```

### Step 6: Call assert_allclose()

```python
assert_allclose(r, r2)
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, compute_corr, [1, 2], [])
```


## Complete Example

```python
# Workflow
"Test Anscombe's Quartett."
x = np.array([10, 8, 13, 9, 11, 14, 6, 4, 12, 7, 5])
y = np.array([[8.04, 6.95, 7.58, 8.81, 8.33, 9.96, 7.24, 4.26, 10.84, 4.82, 5.68], [9.14, 8.14, 8.74, 8.77, 9.26, 8.1, 6.13, 3.1, 9.13, 7.26, 4.74], [7.46, 6.77, 12.74, 7.11, 7.81, 8.84, 6.08, 5.39, 8.15, 6.42, 5.73], [8, 8, 8, 8, 8, 8, 8, 19, 8, 8, 8], [6.58, 5.76, 7.71, 8.84, 8.47, 7.04, 5.25, 12.5, 5.56, 7.91, 6.89]])
r = compute_corr(x, y.T)
r2 = np.array([np.corrcoef(x, y[i])[0, 1] for i in range(len(y))])
assert_allclose(r, r2)
pytest.raises(ValueError, compute_corr, [1, 2], [])
```

## Next Steps


---

*Source: test_numerics.py:105 | Complexity: Intermediate | Last updated: 2026-05-18*