# How To: Average Forward Solution

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test averaging forward solutions.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `gc`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.datasets`
- `mne.forward`
- `mne.io`
- `mne.label`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test averaging forward solutions.'

```python
'Test averaging forward solutions.'
```

**Verification:**
```python
assert isinstance(fwd_copy, Forward)
```

### Step 2: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_meeg)
```

**Verification:**
```python
assert_array_equal(fwd['sol']['data'], fwd_copy['sol']['data'])
```

### Step 3: Call pytest.raises()

```python
pytest.raises(TypeError, average_forward_solutions, 1)
```

**Verification:**
```python
assert_array_equal(0.75 * fwd['sol']['data'], fwd_ave['sol']['data'])
```

### Step 4: Call pytest.raises()

```python
pytest.raises(ValueError, average_forward_solutions, [])
```

**Verification:**
```python
assert_forward_allclose(fwd, fwd_ave)
```

### Step 5: Call pytest.raises()

```python
pytest.raises(ValueError, average_forward_solutions, [fwd, fwd], [-1, 0])
```

### Step 6: Call pytest.raises()

```python
pytest.raises(ValueError, average_forward_solutions, [fwd, fwd], [0, 0])
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, average_forward_solutions, [fwd, fwd], [0, 0, 0])
```

### Step 8: Call pytest.raises()

```python
pytest.raises(TypeError, average_forward_solutions, [1, fwd])
```

### Step 9: Assign fwd_copy = average_forward_solutions(...)

```python
fwd_copy = average_forward_solutions([fwd])
```

**Verification:**
```python
assert isinstance(fwd_copy, Forward)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(fwd['sol']['data'], fwd_copy['sol']['data'])
```

### Step 11: Assign fname_copy = str(...)

```python
fname_copy = str(tmp_path / 'copy-fwd.fif')
```

### Step 12: Call write_forward_solution()

```python
write_forward_solution(fname_copy, fwd_copy, overwrite=True)
```

### Step 13: Assign cmd = value

```python
cmd = ('mne_average_forward_solutions', '--fwd', fname_meeg, '--fwd', fname_copy, '--out', fname_copy)
```

### Step 14: Call run_subprocess()

```python
run_subprocess(cmd)
```

### Step 15: Assign fwd_ave = average_forward_solutions(...)

```python
fwd_ave = average_forward_solutions([fwd, fwd_copy])
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(0.75 * fwd['sol']['data'], fwd_ave['sol']['data'])
```

### Step 17: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_meeg_grad)
```

### Step 18: Assign fwd_ave = average_forward_solutions(...)

```python
fwd_ave = average_forward_solutions([fwd, fwd])
```

### Step 19: Call assert_forward_allclose()

```python
assert_forward_allclose(fwd, fwd_ave)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test averaging forward solutions.'
fwd = read_forward_solution(fname_meeg)
pytest.raises(TypeError, average_forward_solutions, 1)
pytest.raises(ValueError, average_forward_solutions, [])
pytest.raises(ValueError, average_forward_solutions, [fwd, fwd], [-1, 0])
pytest.raises(ValueError, average_forward_solutions, [fwd, fwd], [0, 0])
pytest.raises(ValueError, average_forward_solutions, [fwd, fwd], [0, 0, 0])
pytest.raises(TypeError, average_forward_solutions, [1, fwd])
fwd_copy = average_forward_solutions([fwd])
assert isinstance(fwd_copy, Forward)
assert_array_equal(fwd['sol']['data'], fwd_copy['sol']['data'])
fwd_copy['sol']['data'] *= 0.5
fname_copy = str(tmp_path / 'copy-fwd.fif')
write_forward_solution(fname_copy, fwd_copy, overwrite=True)
cmd = ('mne_average_forward_solutions', '--fwd', fname_meeg, '--fwd', fname_copy, '--out', fname_copy)
run_subprocess(cmd)
fwd_ave = average_forward_solutions([fwd, fwd_copy])
assert_array_equal(0.75 * fwd['sol']['data'], fwd_ave['sol']['data'])
fwd = read_forward_solution(fname_meeg_grad)
fwd_ave = average_forward_solutions([fwd, fwd])
assert_forward_allclose(fwd, fwd_ave)
```

## Next Steps


---

*Source: test_forward.py:437 | Complexity: Advanced | Last updated: 2026-05-18*