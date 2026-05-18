# How To: Si Units

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that our scalings actually produce SI units.

## Prerequisites

**Required Modules:**
- `copy`
- `pytest`
- `numpy.testing`
- `mne.defaults`
- `mne.io.base`


## Step-by-Step Guide

### Step 1: 'Test that our scalings actually produce SI units.'

```python
'Test that our scalings actually produce SI units.'
```

**Verification:**
```python
assert 'csd_bad' not in scalings
```

### Step 2: Assign scalings = _handle_default(...)

```python
scalings = _handle_default('scalings', None)
```

**Verification:**
```python
assert set(scalings) == set(units)
```

### Step 3: Assign units = _handle_default(...)

```python
units = _handle_default('units', None)
```

**Verification:**
```python
assert_allclose(scale, want_scale, rtol=1e-12)
```

### Step 4: Assign unknown = 100000.0

```python
scalings['csd_bad'] = 100000.0
```

### Step 5: Assign unknown = 'V/m²'

```python
units['csd_bad'] = 'V/m²'
```

**Verification:**
```python
assert set(scalings) == set(units)
```

### Step 6: Assign want_scale = _get_scaling(...)

```python
want_scale = _get_scaling(key, units[key])
```

### Step 7: Call assert_allclose()

```python
assert_allclose(scale, want_scale, rtol=1e-12)
```

### Step 8: Assign want_scale = _get_scaling(...)

```python
want_scale = _get_scaling(key, units[key])
```


## Complete Example

```python
# Workflow
'Test that our scalings actually produce SI units.'
scalings = _handle_default('scalings', None)
units = _handle_default('units', None)
assert 'csd_bad' not in scalings
scalings['csd_bad'] = 100000.0
units['csd_bad'] = 'V/m²'
assert set(scalings) == set(units)
for key, scale in scalings.items():
    if key == 'csd_bad':
        with pytest.raises(KeyError, match='is not a channel type'):
            want_scale = _get_scaling(key, units[key])
    else:
        want_scale = _get_scaling(key, units[key])
        assert_allclose(scale, want_scale, rtol=1e-12)
```

## Next Steps


---

*Source: test_defaults.py:31 | Complexity: Advanced | Last updated: 2026-05-18*