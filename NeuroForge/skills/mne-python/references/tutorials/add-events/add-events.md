# How To: Add Events

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adding events to a Raw file.

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

### Step 1: 'Test adding events to a Raw file.'

```python
'Test adding events to a Raw file.'
```

**Verification:**
```python
assert_array_equal(new_events, np.concatenate((events, orig_events)))
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert_array_equal(new_events, events)
```

### Step 3: Assign events = np.array(...)

```python
events = np.array([[raw.first_samp, 0, 1]])
```

### Step 4: Call pytest.raises()

```python
pytest.raises(RuntimeError, raw.add_events, events, 'STI 014')
```

### Step 5: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

### Step 6: Assign orig_events = find_events(...)

```python
orig_events = find_events(raw, 'STI 014')
```

### Step 7: Assign events = np.array(...)

```python
events = np.array([raw.first_samp, 0, 1])
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, raw.add_events, events, 'STI 014')
```

### Step 9: Assign unknown = value

```python
events[0] = raw.first_samp + raw.n_times + 1
```

### Step 10: Assign events = value

```python
events = events[np.newaxis, :]
```

### Step 11: Call pytest.raises()

```python
pytest.raises(ValueError, raw.add_events, events, 'STI 014')
```

### Step 12: Assign unknown = value

```python
events[0, 0] = raw.first_samp - 1
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, raw.add_events, events, 'STI 014')
```

### Step 14: Assign unknown = value

```python
events[0, 0] = raw.first_samp + 1
```

### Step 15: Call pytest.raises()

```python
pytest.raises(ValueError, raw.add_events, events, 'STI FOO')
```

### Step 16: Call raw.add_events()

```python
raw.add_events(events, 'STI 014')
```

### Step 17: Assign new_events = find_events(...)

```python
new_events = find_events(raw, 'STI 014')
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(new_events, np.concatenate((events, orig_events)))
```

### Step 19: Call raw.add_events()

```python
raw.add_events(events, 'STI 014', replace=True)
```

### Step 20: Assign new_events = find_events(...)

```python
new_events = find_events(raw, 'STI 014')
```

### Step 21: Call assert_array_equal()

```python
assert_array_equal(new_events, events)
```


## Complete Example

```python
# Workflow
'Test adding events to a Raw file.'
raw = read_raw_fif(raw_fname)
events = np.array([[raw.first_samp, 0, 1]])
pytest.raises(RuntimeError, raw.add_events, events, 'STI 014')
raw = read_raw_fif(raw_fname, preload=True)
orig_events = find_events(raw, 'STI 014')
events = np.array([raw.first_samp, 0, 1])
pytest.raises(ValueError, raw.add_events, events, 'STI 014')
events[0] = raw.first_samp + raw.n_times + 1
events = events[np.newaxis, :]
pytest.raises(ValueError, raw.add_events, events, 'STI 014')
events[0, 0] = raw.first_samp - 1
pytest.raises(ValueError, raw.add_events, events, 'STI 014')
events[0, 0] = raw.first_samp + 1
pytest.raises(ValueError, raw.add_events, events, 'STI FOO')
raw.add_events(events, 'STI 014')
new_events = find_events(raw, 'STI 014')
assert_array_equal(new_events, np.concatenate((events, orig_events)))
raw.add_events(events, 'STI 014', replace=True)
new_events = find_events(raw, 'STI 014')
assert_array_equal(new_events, events)
```

## Next Steps


---

*Source: test_event.py:73 | Complexity: Advanced | Last updated: 2026-05-18*