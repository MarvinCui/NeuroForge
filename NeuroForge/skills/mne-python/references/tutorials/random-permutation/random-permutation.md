# How To: Random Permutation

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test random permutation function.

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

### Step 1: 'Test random permutation function.'

```python
'Test random permutation function.'
```

**Verification:**
```python
assert_array_equal(python_randperm, matlab_randperm - 1)
```

### Step 2: Assign n_samples = 10

```python
n_samples = 10
```

### Step 3: Assign random_state = 42

```python
random_state = 42
```

### Step 4: Assign python_randperm = random_permutation(...)

```python
python_randperm = random_permutation(n_samples, random_state)
```

### Step 5: Assign matlab_randperm = np.array(...)

```python
matlab_randperm = np.array([7, 6, 5, 1, 4, 9, 10, 3, 8, 2])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(python_randperm, matlab_randperm - 1)
```


## Complete Example

```python
# Workflow
'Test random permutation function.'
n_samples = 10
random_state = 42
python_randperm = random_permutation(n_samples, random_state)
matlab_randperm = np.array([7, 6, 5, 1, 4, 9, 10, 3, 8, 2])
assert_array_equal(python_randperm, matlab_randperm - 1)
```

## Next Steps


---

*Source: test_numerics.py:215 | Complexity: Intermediate | Last updated: 2026-05-18*