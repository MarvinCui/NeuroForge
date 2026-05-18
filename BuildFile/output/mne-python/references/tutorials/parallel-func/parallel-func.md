# How To: Parallel Func

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test Parallel wrapping.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `multiprocessing`
- `os`
- `sys`
- `contextlib`
- `pytest`
- `mne.parallel`

**Setup Required:**
```python
# Fixtures: n_jobs
```

## Step-by-Step Guide

### Step 1: 'Test Parallel wrapping.'

```python
'Test Parallel wrapping.'
```

**Verification:**
```python
assert got_jobs == want_jobs
```

### Step 2: Assign joblib = pytest.importorskip(...)

```python
joblib = pytest.importorskip('joblib')
```

**Verification:**
```python
assert got_jobs == want_jobs
```

### Step 3: Call pytest.skip()

```python
pytest.skip('MNE_FORCE_SERIAL is set')
```

### Step 4: Assign unknown = n_jobs.split(...)

```python
backend, n_jobs = n_jobs.split()
```

### Step 5: Assign n_jobs, want_jobs = int(...)

```python
n_jobs = want_jobs = int(n_jobs)
```

### Step 6: Assign ctx = func(...)

```python
ctx = func(backend, n_jobs=n_jobs)
```

### Step 7: Assign n_jobs = None

```python
n_jobs = None
```

### Step 8: Assign ctx = nullcontext(...)

```python
ctx = nullcontext()
```

### Step 9: Assign unknown = parallel_func(...)

```python
parallel, p_fun, got_jobs = parallel_func(fun, n_jobs, verbose='debug')
```

### Step 10: Assign func = value

```python
func = joblib.parallel_config
```

### Step 11: Assign want_jobs = value

```python
want_jobs = multiprocessing.cpu_count() + 1 + n_jobs
```

### Step 12: Assign want_jobs = 1

```python
want_jobs = 1
```

### Step 13: Assign func = value

```python
func = joblib.parallel_backend
```


## Complete Example

```python
# Setup
# Fixtures: n_jobs

# Workflow
'Test Parallel wrapping.'
joblib = pytest.importorskip('joblib')
if os.getenv('MNE_FORCE_SERIAL', '').lower() in ('true', '1'):
    pytest.skip('MNE_FORCE_SERIAL is set')

def fun(x):
    return x * 2
if isinstance(n_jobs, str):
    backend, n_jobs = n_jobs.split()
    n_jobs = want_jobs = int(n_jobs)
    try:
        func = joblib.parallel_config
    except AttributeError:
        func = joblib.parallel_backend
    ctx = func(backend, n_jobs=n_jobs)
    n_jobs = None
else:
    ctx = nullcontext()
    if n_jobs is not None and n_jobs < 0:
        want_jobs = multiprocessing.cpu_count() + 1 + n_jobs
    else:
        want_jobs = 1
with ctx:
    parallel, p_fun, got_jobs = parallel_func(fun, n_jobs, verbose='debug')
assert got_jobs == want_jobs
```

## Next Steps


---

*Source: test_parallel.py:26 | Complexity: Advanced | Last updated: 2026-05-18*