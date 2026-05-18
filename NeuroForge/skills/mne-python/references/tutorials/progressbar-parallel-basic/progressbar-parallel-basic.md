# How To: Progressbar Parallel Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ProgressBar with parallel computing, basic version.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.parallel`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: capsys
```

## Step-by-Step Guide

### Step 1: 'Test ProgressBar with parallel computing, basic version.'

```python
'Test ProgressBar with parallel computing, basic version.'
```

**Verification:**
```python
assert capsys.readouterr().out == ''
```

### Step 2: Assign unknown = parallel_func(...)

```python
parallel, p_fun, _ = parallel_func(_identity, total=10, n_jobs=1, verbose=True)
```

**Verification:**
```python
assert out == list(range(10))
```

### Step 3: Assign cap = capsys.readouterr(...)

```python
cap = capsys.readouterr()
```

**Verification:**
```python
assert '100%' in out
```

### Step 4: Assign out = value

```python
out = cap.err
```

**Verification:**
```python
assert '100%' in out
```

### Step 5: Assign out = parallel(...)

```python
out = parallel((p_fun(x) for x in range(10)))
```


## Complete Example

```python
# Setup
# Fixtures: capsys

# Workflow
'Test ProgressBar with parallel computing, basic version.'
assert capsys.readouterr().out == ''
parallel, p_fun, _ = parallel_func(_identity, total=10, n_jobs=1, verbose=True)
with use_log_level(True):
    out = parallel((p_fun(x) for x in range(10)))
assert out == list(range(10))
cap = capsys.readouterr()
out = cap.err
assert '100%' in out
```

## Next Steps


---

*Source: test_progressbar.py:60 | Complexity: Intermediate | Last updated: 2026-05-18*