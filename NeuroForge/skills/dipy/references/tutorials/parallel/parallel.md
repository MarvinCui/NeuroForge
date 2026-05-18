# How To: Parallel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test parallel

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.denoise.gibbs`


## Step-by-Step Guide

### Step 1: Assign input_2d = image_gibbs.copy(...)

```python
input_2d = image_gibbs.copy()
```

**Verification:**
```python
assert_array_almost_equal(output_3d_parallel, output_3d_no_parallel)
```

### Step 2: Assign input_3d = np.stack(...)

```python
input_3d = np.stack([input_2d, input_2d], axis=2)
```

**Verification:**
```python
assert_array_almost_equal(output_4d_parallel, output_4d_no_parallel)
```

### Step 3: Assign input_4d = np.stack(...)

```python
input_4d = np.stack([input_3d, input_3d], axis=3)
```

**Verification:**
```python
assert_array_almost_equal(output_4d_all_cpu, output_4d_no_parallel)
```

### Step 4: Assign output_3d_parallel = gibbs_removal(...)

```python
output_3d_parallel = gibbs_removal(input_3d, inplace=False, num_processes=2)
```

### Step 5: Assign output_3d_no_parallel = gibbs_removal(...)

```python
output_3d_no_parallel = gibbs_removal(input_3d, inplace=False, num_processes=1)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(output_3d_parallel, output_3d_no_parallel)
```

### Step 7: Assign output_4d_parallel = gibbs_removal(...)

```python
output_4d_parallel = gibbs_removal(input_4d, inplace=False, num_processes=2)
```

### Step 8: Assign output_4d_no_parallel = gibbs_removal(...)

```python
output_4d_no_parallel = gibbs_removal(input_4d, inplace=False, num_processes=1)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(output_4d_parallel, output_4d_no_parallel)
```

### Step 10: Assign output_4d_all_cpu = gibbs_removal(...)

```python
output_4d_all_cpu = gibbs_removal(input_4d, inplace=False, num_processes=None)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(output_4d_all_cpu, output_4d_no_parallel)
```


## Complete Example

```python
# Workflow
input_2d = image_gibbs.copy()
input_3d = np.stack([input_2d, input_2d], axis=2)
input_4d = np.stack([input_3d, input_3d], axis=3)
output_3d_parallel = gibbs_removal(input_3d, inplace=False, num_processes=2)
output_3d_no_parallel = gibbs_removal(input_3d, inplace=False, num_processes=1)
assert_array_almost_equal(output_3d_parallel, output_3d_no_parallel)
output_4d_parallel = gibbs_removal(input_4d, inplace=False, num_processes=2)
output_4d_no_parallel = gibbs_removal(input_4d, inplace=False, num_processes=1)
assert_array_almost_equal(output_4d_parallel, output_4d_no_parallel)
output_4d_all_cpu = gibbs_removal(input_4d, inplace=False, num_processes=None)
assert_array_almost_equal(output_4d_all_cpu, output_4d_no_parallel)
```

## Next Steps


---

*Source: test_gibbs.py:46 | Complexity: Advanced | Last updated: 2026-05-18*