# How To: Paramap Sequence Kwargs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test paramap sequence kwargs

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.utils.parallel`
- `dipy.utils.parallel`
- `dipy.utils.parallel`
- `dipy.utils.multiproc`


## Step-by-Step Guide

### Step 1: Assign my_array = np.arange(...)

```python
my_array = np.arange(10)
```

### Step 2: Assign kwargs_sequence = value

```python
kwargs_sequence = [{'n': i} for i in range(len(my_array))]
```

### Step 3: Assign my_list = list(...)

```python
my_list = list(my_array.ravel())
```

### Step 4: Call npt.assert_array_equal()

```python
npt.assert_array_equal(para.paramap(power_it, my_list, engine=engine, backend=backend, out_shape=my_array.shape, func_kwargs=kwargs_sequence), [power_it(ii, **kwargs) for ii, kwargs in zip(my_array, kwargs_sequence)])
```


## Complete Example

```python
# Workflow
my_array = np.arange(10)
kwargs_sequence = [{'n': i} for i in range(len(my_array))]
my_list = list(my_array.ravel())
for engine in ENGINES:
    for backend in ['threading', 'multiprocessing']:
        npt.assert_array_equal(para.paramap(power_it, my_list, engine=engine, backend=backend, out_shape=my_array.shape, func_kwargs=kwargs_sequence), [power_it(ii, **kwargs) for ii, kwargs in zip(my_array, kwargs_sequence)])
```

## Next Steps


---

*Source: test_parallel.py:45 | Complexity: Intermediate | Last updated: 2026-05-18*