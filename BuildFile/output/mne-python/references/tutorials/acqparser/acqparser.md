# How To: Acqparser

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test AcqParserFIF.

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test AcqParserFIF.'

```python
'Test AcqParserFIF.'
```

**Verification:**
```python
assert repr(acqp)
```

### Step 2: Call pytest.raises()

```python
pytest.raises(ValueError, AcqParserFIF, {'acq_pars': ''})
```

**Verification:**
```python
assert acqp.compat
```

### Step 3: Call pytest.raises()

```python
pytest.raises(ValueError, AcqParserFIF, {'acq_pars': 'baaa'})
```

**Verification:**
```python
assert_equal(len(acqp.categories), 6)
```

### Step 4: Call pytest.raises()

```python
pytest.raises(ValueError, AcqParserFIF, {'acq_pars': 'ERFVersion\n1'})
```

**Verification:**
```python
assert_equal(len(acqp._categories), 17)
```

### Step 5: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=False)
```

**Verification:**
```python
assert_equal(len(acqp.events), 6)
```

### Step 6: Assign acqp = AcqParserFIF(...)

```python
acqp = AcqParserFIF(raw.info)
```

**Verification:**
```python
assert_equal(len(acqp._events), 17)
```

### Step 7: Call assert_equal()

```python
assert_equal(len(acqp.categories), 6)
```

**Verification:**
```python
assert acqp['Surprise visual']
```

### Step 8: Call assert_equal()

```python
assert_equal(len(acqp._categories), 17)
```

**Verification:**
```python
assert acqp is raw.acqparser
```

### Step 9: Call assert_equal()

```python
assert_equal(len(acqp.events), 6)
```

**Verification:**
```python
assert repr(acqp)
```

### Step 10: Call assert_equal()

```python
assert_equal(len(acqp._events), 17)
```

**Verification:**
```python
assert not acqp.compat
```

### Step 11: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw_elekta, preload=False)
```

**Verification:**
```python
assert_equal(len(acqp), 7)
```

### Step 12: Assign acqp = value

```python
acqp = raw.acqparser
```

**Verification:**
```python
assert_equal(len(acqp.categories), 7)
```

### Step 13: Call pytest.raises()

```python
pytest.raises(KeyError, acqp.__getitem__, 'does not exist')
```

**Verification:**
```python
assert_equal(len(acqp._categories), 32)
```

### Step 14: Call pytest.raises()

```python
pytest.raises(KeyError, acqp.get_condition, raw, 'foo')
```

**Verification:**
```python
assert_equal(len(acqp.events), 6)
```

### Step 15: Call pytest.raises()

```python
pytest.raises(TypeError, acqp.__getitem__, 0)
```

**Verification:**
```python
assert_equal(len(acqp._events), 32)
```

### Step 16: Call assert_equal()

```python
assert_equal(len(acqp), 7)
```

**Verification:**
```python
assert acqp['Test event 5']
```

### Step 17: Call assert_equal()

```python
assert_equal(len(acqp.categories), 7)
```

### Step 18: Call assert_equal()

```python
assert_equal(len(acqp._categories), 32)
```

### Step 19: Call assert_equal()

```python
assert_equal(len(acqp.events), 6)
```

### Step 20: Call assert_equal()

```python
assert_equal(len(acqp._events), 32)
```

**Verification:**
```python
assert acqp['Test event 5']
```


## Complete Example

```python
# Workflow
'Test AcqParserFIF.'
pytest.raises(ValueError, AcqParserFIF, {'acq_pars': ''})
pytest.raises(ValueError, AcqParserFIF, {'acq_pars': 'baaa'})
pytest.raises(ValueError, AcqParserFIF, {'acq_pars': 'ERFVersion\n1'})
raw = read_raw_fif(raw_fname, preload=False)
acqp = AcqParserFIF(raw.info)
assert repr(acqp)
assert acqp.compat
assert_equal(len(acqp.categories), 6)
assert_equal(len(acqp._categories), 17)
assert_equal(len(acqp.events), 6)
assert_equal(len(acqp._events), 17)
assert acqp['Surprise visual']
raw = read_raw_fif(fname_raw_elekta, preload=False)
acqp = raw.acqparser
assert acqp is raw.acqparser
assert repr(acqp)
assert not acqp.compat
pytest.raises(KeyError, acqp.__getitem__, 'does not exist')
pytest.raises(KeyError, acqp.get_condition, raw, 'foo')
pytest.raises(TypeError, acqp.__getitem__, 0)
assert_equal(len(acqp), 7)
assert_equal(len(acqp.categories), 7)
assert_equal(len(acqp._categories), 32)
assert_equal(len(acqp.events), 6)
assert_equal(len(acqp._events), 32)
assert acqp['Test event 5']
```

## Next Steps


---

*Source: test_event.py:528 | Complexity: Advanced | Last updated: 2026-05-18*