# How To: Create Second Level Design

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test create second level design

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level.design_matrix`
- `_testing`


## Step-by-Step Guide

### Step 1: Assign subjects_label = value

```python
subjects_label = ['02', '01']
```

**Verification:**
```python
assert_array_equal(design, expected_design)
```

### Step 2: Assign regressors = value

```python
regressors = [['01', 0.1], ['02', 0.75]]
```

**Verification:**
```python
assert len(design.columns) == 2
```

### Step 3: Assign regressors = pd.DataFrame(...)

```python
regressors = pd.DataFrame(regressors, columns=['subject_label', 'f1'])
```

**Verification:**
```python
assert len(design) == 2
```

### Step 4: Assign design = make_second_level_design_matrix(...)

```python
design = make_second_level_design_matrix(subjects_label, regressors)
```

### Step 5: Assign expected_design = np.array(...)

```python
expected_design = np.array([[0.75, 1.0], [0.1, 1.0]])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(design, expected_design)
```

**Verification:**
```python
assert len(design.columns) == 2
```


## Complete Example

```python
# Workflow
subjects_label = ['02', '01']
regressors = [['01', 0.1], ['02', 0.75]]
regressors = pd.DataFrame(regressors, columns=['subject_label', 'f1'])
design = make_second_level_design_matrix(subjects_label, regressors)
expected_design = np.array([[0.75, 1.0], [0.1, 1.0]])
assert_array_equal(design, expected_design)
assert len(design.columns) == 2
assert len(design) == 2
```

## Next Steps


---

*Source: test_design_matrix.py:458 | Complexity: Intermediate | Last updated: 2026-05-18*