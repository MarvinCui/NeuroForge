# How To: Discrete Source Space

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test setting up (and reading/writing) discrete source spaces.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.fixes`
- `mne.source_estimate`
- `mne.source_space`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test setting up (and reading/writing) discrete source spaces.'

```python
'Test setting up (and reading/writing) discrete source spaces.'
```

**Verification:**
```python
assert src_new.kind == 'discrete'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert_allclose(src[0]['rr'][v], src_new[0]['rr'], rtol=0.001, atol=1e-06)
```

### Step 3: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname)
```

**Verification:**
```python
assert_allclose(src[0]['nn'][v], src_new[0]['nn'], rtol=0.001, atol=1e-06)
```

### Step 4: Assign v = value

```python
v = src[0]['vertno']
```

**Verification:**
```python
assert repr(src_new).split('~')[0] == repr(src_c).split('~')[0]
```

### Step 5: Assign temp_name = value

```python
temp_name = tmp_path / 'temp-src.fif'
```

**Verification:**
```python
assert ' KiB' in repr(src_new)
```

### Step 6: Assign temp_pos = value

```python
temp_pos = tmp_path / 'temp-pos.txt'
```

**Verification:**
```python
assert src_new.kind == 'discrete'
```

### Step 7: Call np.savetxt()

```python
np.savetxt(str(temp_pos), np.c_[src[0]['rr'][v], src[0]['nn'][v]])
```

**Verification:**
```python
assert _get_src_type(src_new, None) == 'discrete'
```

### Step 8: Call run_subprocess()

```python
run_subprocess(['mne_volume_source_space', '--meters', '--pos', temp_pos, '--src', temp_name])
```

### Step 9: Assign src_c = read_source_spaces(...)

```python
src_c = read_source_spaces(temp_name)
```

### Step 10: Assign pos_dict = dict(...)

```python
pos_dict = dict(rr=src[0]['rr'][v], nn=src[0]['nn'][v])
```

### Step 11: Assign src_new = setup_volume_source_space(...)

```python
src_new = setup_volume_source_space(pos=pos_dict)
```

**Verification:**
```python
assert src_new.kind == 'discrete'
```

### Step 12: Call _compare_source_spaces()

```python
_compare_source_spaces(src_c, src_new, mode='approx')
```

### Step 13: Call assert_allclose()

```python
assert_allclose(src[0]['rr'][v], src_new[0]['rr'], rtol=0.001, atol=1e-06)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(src[0]['nn'][v], src_new[0]['nn'], rtol=0.001, atol=1e-06)
```

### Step 15: Call write_source_spaces()

```python
write_source_spaces(temp_name, src_c, overwrite=True)
```

### Step 16: Assign src_c2 = read_source_spaces(...)

```python
src_c2 = read_source_spaces(temp_name)
```

### Step 17: Call _compare_source_spaces()

```python
_compare_source_spaces(src_c, src_c2)
```

**Verification:**
```python
assert repr(src_new).split('~')[0] == repr(src_c).split('~')[0]
```

### Step 18: Call setup_volume_source_space()

```python
setup_volume_source_space('sample', pos=pos_dict, mri=fname_mri)
```

### Step 19: Call setup_volume_source_space()

```python
setup_volume_source_space(pos=dict(rr=[[0, 0, float('inf')]], nn=[[0, 1, 0]]))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test setting up (and reading/writing) discrete source spaces.'
pytest.importorskip('nibabel')
src = read_source_spaces(fname)
v = src[0]['vertno']
temp_name = tmp_path / 'temp-src.fif'
temp_pos = tmp_path / 'temp-pos.txt'
np.savetxt(str(temp_pos), np.c_[src[0]['rr'][v], src[0]['nn'][v]])
run_subprocess(['mne_volume_source_space', '--meters', '--pos', temp_pos, '--src', temp_name])
src_c = read_source_spaces(temp_name)
pos_dict = dict(rr=src[0]['rr'][v], nn=src[0]['nn'][v])
src_new = setup_volume_source_space(pos=pos_dict)
assert src_new.kind == 'discrete'
_compare_source_spaces(src_c, src_new, mode='approx')
assert_allclose(src[0]['rr'][v], src_new[0]['rr'], rtol=0.001, atol=1e-06)
assert_allclose(src[0]['nn'][v], src_new[0]['nn'], rtol=0.001, atol=1e-06)
write_source_spaces(temp_name, src_c, overwrite=True)
src_c2 = read_source_spaces(temp_name)
_compare_source_spaces(src_c, src_c2)
with pytest.raises(ValueError, match='Cannot create interpolation'):
    setup_volume_source_space('sample', pos=pos_dict, mri=fname_mri)
assert repr(src_new).split('~')[0] == repr(src_c).split('~')[0]
assert ' KiB' in repr(src_new)
assert src_new.kind == 'discrete'
assert _get_src_type(src_new, None) == 'discrete'
with pytest.raises(RuntimeError, match='finite'):
    setup_volume_source_space(pos=dict(rr=[[0, 0, float('inf')]], nn=[[0, 1, 0]]))
```

## Next Steps


---

*Source: test_source_space.py:276 | Complexity: Advanced | Last updated: 2026-05-18*