# How To: Nlmeans 4D 3Dsigma And Threads

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test 4D data with threading using classic method.

## Prerequisites

**Required Modules:**
- `time`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.denoise.denspeed`
- `dipy.denoise.nlmeans`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.omp`


## Step-by-Step Guide

### Step 1: 'Test 4D data with threading using classic method.'

```python
'Test 4D data with threading using classic method.'
```

**Verification:**
```python
assert_array_almost_equal(new_data, new_data2)
```

### Step 2: Assign data = np.ones(...)

```python
data = np.ones((50, 50, 50, 5))
```

**Verification:**
```python
assert_greater(duration_1core, duration_all_core)
```

### Step 3: Assign sigma = 1.0

```python
sigma = 1.0
```

### Step 4: Assign mask = np.zeros(...)

```python
mask = np.zeros(data.shape[:3])
```

### Step 5: Assign unknown = 1

```python
mask[:] = 1
```

### Step 6: Call print()

```python
print('1 core')
```

### Step 7: Assign t = time(...)

```python
t = time()
```

### Step 8: Assign new_data = nlmeans(...)

```python
new_data = nlmeans(data, sigma, mask=mask, num_threads=1, method='classic')
```

### Step 9: Assign duration_1core = value

```python
duration_1core = time() - t
```

### Step 10: Call print()

```python
print(duration_1core)
```

### Step 11: Call print()

```python
print(f'All cores {cpu_count()}')
```

### Step 12: Assign t = time(...)

```python
t = time()
```

### Step 13: Assign new_data2 = nlmeans(...)

```python
new_data2 = nlmeans(data, sigma, mask=mask, num_threads=None, method='classic')
```

### Step 14: Assign duration_all_core = value

```python
duration_all_core = time() - t
```

### Step 15: Call print()

```python
print(duration_all_core)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(new_data, new_data2)
```

### Step 17: Call assert_greater()

```python
assert_greater(duration_1core, duration_all_core)
```


## Complete Example

```python
# Workflow
'Test 4D data with threading using classic method.'
data = np.ones((50, 50, 50, 5))
sigma = 1.0
mask = np.zeros(data.shape[:3])
mask[:] = 1
print('1 core')
t = time()
new_data = nlmeans(data, sigma, mask=mask, num_threads=1, method='classic')
duration_1core = time() - t
print(duration_1core)
print(f'All cores {cpu_count()}')
t = time()
new_data2 = nlmeans(data, sigma, mask=mask, num_threads=None, method='classic')
duration_all_core = time() - t
print(duration_all_core)
assert_array_almost_equal(new_data, new_data2)
if cpu_count() > 2:
    assert_greater(duration_1core, duration_all_core)
```

## Next Steps


---

*Source: test_nlmeans.py:127 | Complexity: Advanced | Last updated: 2026-05-18*