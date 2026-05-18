# How To: Evoked Proj

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test SSP proj operations.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.evoked`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test SSP proj operations.'

```python
'Test SSP proj operations.'
```

**Verification:**
```python
assert all((p['active'] == proj for p in ave.info['projs']))
```

### Step 2: Assign ave = read_evokeds(...)

```python
ave = read_evokeds(fname, condition=0, proj=False)
```

**Verification:**
```python
assert len(ave.info['projs']) == n_proj - 1
```

### Step 3: Assign data = ave.data.copy(...)

```python
data = ave.data.copy()
```

**Verification:**
```python
assert len(ave.info['projs']) == n_proj
```

### Step 4: Call ave.apply_proj()

```python
ave.apply_proj()
```

**Verification:**
```python
assert len(ave.info['projs']) == n_proj - 1
```

### Step 5: Call assert_allclose()

```python
assert_allclose(np.dot(ave._projector, data), ave.data)
```

**Verification:**
```python
assert_allclose(np.dot(ave._projector, data), ave.data)
```

### Step 6: Assign ave = read_evokeds(...)

```python
ave = read_evokeds(fname, condition=0, proj=proj)
```

**Verification:**
```python
assert all((p['active'] == proj for p in ave.info['projs']))
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, ave.add_proj, [], {'remove_existing': True})
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, ave.del_proj, 0)
```

### Step 9: Assign projs = deepcopy(...)

```python
projs = deepcopy(ave.info['projs'])
```

### Step 10: Assign n_proj = len(...)

```python
n_proj = len(ave.info['projs'])
```

### Step 11: Call ave.del_proj()

```python
ave.del_proj(0)
```

**Verification:**
```python
assert len(ave.info['projs']) == n_proj - 1
```

### Step 12: Call ave.add_proj()

```python
ave.add_proj(projs, remove_existing=False)
```

**Verification:**
```python
assert len(ave.info['projs']) == n_proj
```

### Step 13: Call ave.add_proj()

```python
ave.add_proj(projs[:-1], remove_existing=True)
```

**Verification:**
```python
assert len(ave.info['projs']) == n_proj - 1
```


## Complete Example

```python
# Workflow
'Test SSP proj operations.'
for proj in [True, False]:
    ave = read_evokeds(fname, condition=0, proj=proj)
    assert all((p['active'] == proj for p in ave.info['projs']))
    if proj:
        pytest.raises(ValueError, ave.add_proj, [], {'remove_existing': True})
        pytest.raises(ValueError, ave.del_proj, 0)
    else:
        projs = deepcopy(ave.info['projs'])
        n_proj = len(ave.info['projs'])
        ave.del_proj(0)
        assert len(ave.info['projs']) == n_proj - 1
        ave.add_proj(projs, remove_existing=False)
        assert len(ave.info['projs']) == n_proj
        ave.add_proj(projs[:-1], remove_existing=True)
        assert len(ave.info['projs']) == n_proj - 1
ave = read_evokeds(fname, condition=0, proj=False)
data = ave.data.copy()
ave.apply_proj()
assert_allclose(np.dot(ave._projector, data), ave.data)
```

## Next Steps


---

*Source: test_evoked.py:491 | Complexity: Advanced | Last updated: 2026-05-18*