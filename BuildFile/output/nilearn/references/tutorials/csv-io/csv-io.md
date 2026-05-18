# How To: Csv Io

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test csv io

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level.design_matrix`
- `_testing`

**Setup Required:**
```python
# Fixtures: tmp_path, frame_times
```

## Step-by-Step Guide

### Step 1: Assign DM = make_first_level_design_matrix(...)

```python
DM = make_first_level_design_matrix(frame_times, events=modulated_event_paradigm(), hrf_model='glover', drift_model='polynomial', drift_order=3)
```

**Verification:**
```python
assert_almost_equal(matrix, matrix_)
```

### Step 2: Assign path = value

```python
path = tmp_path / 'design_matrix.csv'
```

**Verification:**
```python
assert names == names_
```

### Step 3: Call DM.to_csv()

```python
DM.to_csv(path)
```

### Step 4: Assign DM2 = pd.read_csv(...)

```python
DM2 = pd.read_csv(path, index_col=0)
```

### Step 5: Assign unknown = check_design_matrix(...)

```python
_, matrix, names = check_design_matrix(DM)
```

### Step 6: Assign unknown = check_design_matrix(...)

```python
_, matrix_, names_ = check_design_matrix(DM2)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(matrix, matrix_)
```

**Verification:**
```python
assert names == names_
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, frame_times

# Workflow
DM = make_first_level_design_matrix(frame_times, events=modulated_event_paradigm(), hrf_model='glover', drift_model='polynomial', drift_order=3)
path = tmp_path / 'design_matrix.csv'
DM.to_csv(path)
DM2 = pd.read_csv(path, index_col=0)
_, matrix, names = check_design_matrix(DM)
_, matrix_, names_ = check_design_matrix(DM2)
assert_almost_equal(matrix, matrix_)
assert names == names_
```

## Next Steps


---

*Source: test_design_matrix.py:420 | Complexity: Intermediate | Last updated: 2026-05-18*