# How To: Parallel Func N Jobs None

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test n_jobs=None is same as n_jobs=1.

## Prerequisites

**Required Modules:**
- `multiprocessing`
- `os`
- `sys`
- `contextlib`
- `pytest`
- `mne.parallel`


## Step-by-Step Guide

### Step 1: 'Test n_jobs=None is same as n_jobs=1.'

```python
'Test n_jobs=None is same as n_jobs=1.'
```

**Verification:**
```python
assert parallel_none is parallel_one is list
```

### Step 2: Assign joblib = pytest.importorskip(...)

```python
joblib = pytest.importorskip('joblib')
```

**Verification:**
```python
assert n_jobs_none == n_jobs_one == 1
```

### Step 3: Assign unknown = parallel_func(...)

```python
parallel_none, p_fun_none, n_jobs_none = parallel_func(fun, n_jobs=None)
```

**Verification:**
```python
assert p_fun_none is p_fun_one is fun, 'fun should not be wrapped but is'
```

### Step 4: Assign unknown = parallel_func(...)

```python
parallel_one, p_fun_one, n_jobs_one = parallel_func(fun, n_jobs=1)
```

**Verification:**
```python
assert n_jobs == 2
```

### Step 5: Assign unknown = parallel_func(...)

```python
parallel, p_fun, n_jobs = parallel_func(fun, n_jobs=None)
```

**Verification:**
```python
assert parallel is not list
```


## Complete Example

```python
# Workflow
'Test n_jobs=None is same as n_jobs=1.'
joblib = pytest.importorskip('joblib')

def fun(x):
    return x * 2
parallel_none, p_fun_none, n_jobs_none = parallel_func(fun, n_jobs=None)
parallel_one, p_fun_one, n_jobs_one = parallel_func(fun, n_jobs=1)
assert parallel_none is parallel_one is list
assert n_jobs_none == n_jobs_one == 1
assert p_fun_none is p_fun_one is fun, 'fun should not be wrapped but is'
if sys.platform != 'win32':
    with joblib.parallel_config(backend='loky', n_jobs=2):
        parallel, p_fun, n_jobs = parallel_func(fun, n_jobs=None)
    assert n_jobs == 2
    assert parallel is not list
    assert fun is not p_fun, 'fun should be wrapped but is not'
```

## Next Steps


---

*Source: test_parallel.py:56 | Complexity: Intermediate | Last updated: 2026-05-18*