# How To: Nibabel Bench

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, unittest, workflow, integration

## Overview

Workflow: test nibabel bench

## Prerequisites

**Required Modules:**
- `pathlib`
- `unittest`
- `importlib.resources`
- `unittest`
- `pytest`
- `nibabel`


## Step-by-Step Guide

### Step 1: Assign config_path = value

```python
config_path = files('nibabel') / 'benchmarks/pytest.benchmark.ini'
```

**Verification:**
```python
assert args == ()
```

### Step 2: Assign expected_args = value

```python
expected_args = ['-c', str(config_path), '--pyargs', 'nibabel']
```

**Verification:**
```python
assert kwargs == {'args': expected_args}
```

### Step 3: Assign unknown = value

```python
args, kwargs = pytest_main.call_args
```

**Verification:**
```python
assert args == ()
```

### Step 4: Assign unknown = value

```python
args, kwargs = pytest_main.call_args
```

**Verification:**
```python
assert kwargs == {'args': expected_args}
```

### Step 5: Call nib.bench()

```python
nib.bench(verbose=0)
```

### Step 6: Call nib.bench()

```python
nib.bench(verbose=0, extra_argv=[])
```


## Complete Example

```python
# Workflow
config_path = files('nibabel') / 'benchmarks/pytest.benchmark.ini'
if not isinstance(config_path, pathlib.Path):
    raise unittest.SkipTest('Package is not unpacked; could get temp path')
expected_args = ['-c', str(config_path), '--pyargs', 'nibabel']
with mock.patch('pytest.main') as pytest_main:
    nib.bench(verbose=0)
args, kwargs = pytest_main.call_args
assert args == ()
assert kwargs == {'args': expected_args}
with mock.patch('pytest.main') as pytest_main:
    nib.bench(verbose=0, extra_argv=[])
args, kwargs = pytest_main.call_args
assert args == ()
assert kwargs == {'args': expected_args}
```

## Next Steps


---

*Source: test_init.py:42 | Complexity: Intermediate | Last updated: 2026-05-18*