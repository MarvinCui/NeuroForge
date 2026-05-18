# How To: Read Write Head Pos

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading and writing head position quaternion parameters.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.interpolate`
- `scipy.spatial.distance`
- `mne`
- `mne._fiff.constants`
- `mne.chpi`
- `mne.datasets`
- `mne.forward._compute_forward`
- `mne.io`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `scipy.signal`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading and writing head position quaternion parameters.'

```python
'Test reading and writing head position quaternion parameters.'
```

**Verification:**
```python
assert_allclose(head_pos_orig, head_pos, atol=0.001)
```

### Step 2: Assign temp_name = value

```python
temp_name = tmp_path / 'temp.pos'
```

### Step 3: Assign head_pos_rand = np.random.RandomState.randn(...)

```python
head_pos_rand = np.random.RandomState(0).randn(20, 10)
```

### Step 4: Assign head_pos_read = read_head_pos(...)

```python
head_pos_read = read_head_pos(pos_fname)
```

### Step 5: Call pytest.raises()

```python
pytest.raises(TypeError, write_head_pos, 0, head_pos_read)
```

### Step 6: Call pytest.raises()

```python
pytest.raises(ValueError, write_head_pos, temp_name, 'foo')
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, write_head_pos, temp_name, head_pos_read[:, :9])
```

### Step 8: Call pytest.raises()

```python
pytest.raises(TypeError, read_head_pos, 0)
```

### Step 9: Call pytest.raises()

```python
pytest.raises(OSError, read_head_pos, '101')
```

### Step 10: Call write_head_pos()

```python
write_head_pos(temp_name, head_pos_orig)
```

### Step 11: Assign head_pos = read_head_pos(...)

```python
head_pos = read_head_pos(temp_name)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(head_pos_orig, head_pos, atol=0.001)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading and writing head position quaternion parameters.'
temp_name = tmp_path / 'temp.pos'
head_pos_rand = np.random.RandomState(0).randn(20, 10)
head_pos_read = read_head_pos(pos_fname)
for head_pos_orig in (head_pos_rand, head_pos_read):
    write_head_pos(temp_name, head_pos_orig)
    head_pos = read_head_pos(temp_name)
    assert_allclose(head_pos_orig, head_pos, atol=0.001)
pytest.raises(TypeError, write_head_pos, 0, head_pos_read)
pytest.raises(ValueError, write_head_pos, temp_name, 'foo')
pytest.raises(ValueError, write_head_pos, temp_name, head_pos_read[:, :9])
pytest.raises(TypeError, read_head_pos, 0)
pytest.raises(OSError, read_head_pos, '101')
```

## Next Steps


---

*Source: test_chpi.py:143 | Complexity: Advanced | Last updated: 2026-05-18*