# How To: Egi Coord Frame

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that EGI coordinate frame is changed to head.

## Prerequisites

**Required Modules:**
- `os`
- `copy`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.egi.egi`
- `mne.io.tests.test_raw`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that EGI coordinate frame is changed to head.'

```python
'Test that EGI coordinate frame is changed to head.'
```

**Verification:**
```python
assert d['kind'] == FIFF.FIFFV_POINT_CARDINAL
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('defusedxml')
```

**Verification:**
```python
assert d['ident'] == want
```

### Step 3: Assign info = value

```python
info = read_raw_egi(egi_mff_fname).info
```

**Verification:**
```python
assert 0.05 < -loc[0] < 0.1, 'LPA'
```

### Step 4: Assign want_idents = value

```python
want_idents = (FIFF.FIFFV_POINT_LPA, FIFF.FIFFV_POINT_NASION, FIFF.FIFFV_POINT_RPA)
```

**Verification:**
```python
assert_allclose(loc[1:], 0, atol=1e-07, err_msg='LPA')
```

### Step 5: Assign d = value

```python
d = info['dig'][ii]
```

**Verification:**
```python
assert 0.05 < loc[1] < 0.11, 'Nasion'
```

### Step 6: Assign loc = value

```python
loc = d['r']
```

**Verification:**
```python
assert_allclose(loc[::2], 0, atol=1e-07, err_msg='Nasion')
```

### Step 7: Call assert_allclose()

```python
assert_allclose(loc[1:], 0, atol=1e-07, err_msg='LPA')
```

**Verification:**
```python
assert ii == 2
```

### Step 8: Call assert_allclose()

```python
assert_allclose(loc[::2], 0, atol=1e-07, err_msg='Nasion')
```

**Verification:**
```python
assert 0.05 < loc[0] < 0.1, 'RPA'
```

### Step 9: Call assert_allclose()

```python
assert_allclose(loc[1:], 0, atol=1e-07, err_msg='RPA')
```

**Verification:**
```python
assert_allclose(loc[1:], 0, atol=1e-07, err_msg='RPA')
```


## Complete Example

```python
# Workflow
'Test that EGI coordinate frame is changed to head.'
pytest.importorskip('defusedxml')
info = read_raw_egi(egi_mff_fname).info
want_idents = (FIFF.FIFFV_POINT_LPA, FIFF.FIFFV_POINT_NASION, FIFF.FIFFV_POINT_RPA)
for ii, want in enumerate(want_idents):
    d = info['dig'][ii]
    assert d['kind'] == FIFF.FIFFV_POINT_CARDINAL
    assert d['ident'] == want
    loc = d['r']
    if ii == 0:
        assert 0.05 < -loc[0] < 0.1, 'LPA'
        assert_allclose(loc[1:], 0, atol=1e-07, err_msg='LPA')
    elif ii == 1:
        assert 0.05 < loc[1] < 0.11, 'Nasion'
        assert_allclose(loc[::2], 0, atol=1e-07, err_msg='Nasion')
    else:
        assert ii == 2
        assert 0.05 < loc[0] < 0.1, 'RPA'
        assert_allclose(loc[1:], 0, atol=1e-07, err_msg='RPA')
for d in info['dig'][3:]:
    assert d['kind'] == FIFF.FIFFV_POINT_EEG
```

## Next Steps


---

*Source: test_egi.py:505 | Complexity: Advanced | Last updated: 2026-05-18*