# How To: Annotation Omit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test raw.get_data with annotations.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `collections`
- `datetime`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: first_samp
```

## Step-by-Step Guide

### Step 1: 'Test raw.get_data with annotations.'

```python
'Test raw.get_data with annotations.'
```

**Verification:**
```python
assert_allclose(raw.get_data(reject_by_annotation=None), expected)
```

### Step 2: Assign data = np.concatenate(...)

```python
data = np.concatenate([np.ones((1, 1000)), 2 * np.ones((1, 1000))], -1)
```

**Verification:**
```python
assert_allclose(raw.get_data(reject_by_annotation='nan'), expected)
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(1, 1000.0, 'eeg')
```

**Verification:**
```python
assert_allclose(got, expected)
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, first_samp=first_samp)
```

**Verification:**
```python
assert_allclose(raw.get_data(reject_by_annotation='omit'), expected)
```

### Step 5: Call raw.set_annotations()

```python
raw.set_annotations(Annotations([0.5], [1], ['bad']))
```

**Verification:**
```python
assert_allclose(got, expected)
```

### Step 6: Assign expected = value

```python
expected = raw[0][0]
```

### Step 7: Call assert_allclose()

```python
assert_allclose(raw.get_data(reject_by_annotation=None), expected)
```

### Step 8: Assign unknown = value

```python
expected[0, 500:1500] = np.nan
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw.get_data(reject_by_annotation='nan'), expected)
```

### Step 10: Assign got = np.concatenate(...)

```python
got = np.concatenate([raw.get_data(start=start, stop=stop, reject_by_annotation='nan') for start, stop in ((0, 1000), (1000, 2000))], -1)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(got, expected)
```

### Step 12: Assign expected = value

```python
expected = expected[:, np.isfinite(expected[0])]
```

### Step 13: Call assert_allclose()

```python
assert_allclose(raw.get_data(reject_by_annotation='omit'), expected)
```

### Step 14: Assign got = np.concatenate(...)

```python
got = np.concatenate([raw.get_data(start=start, stop=stop, reject_by_annotation='omit') for start, stop in ((0, 1000), (1000, 2000))], -1)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(got, expected)
```

### Step 16: Call pytest.raises()

```python
pytest.raises(ValueError, raw.get_data, reject_by_annotation='foo')
```


## Complete Example

```python
# Setup
# Fixtures: first_samp

# Workflow
'Test raw.get_data with annotations.'
data = np.concatenate([np.ones((1, 1000)), 2 * np.ones((1, 1000))], -1)
info = create_info(1, 1000.0, 'eeg')
raw = RawArray(data, info, first_samp=first_samp)
raw.set_annotations(Annotations([0.5], [1], ['bad']))
expected = raw[0][0]
assert_allclose(raw.get_data(reject_by_annotation=None), expected)
expected[0, 500:1500] = np.nan
assert_allclose(raw.get_data(reject_by_annotation='nan'), expected)
got = np.concatenate([raw.get_data(start=start, stop=stop, reject_by_annotation='nan') for start, stop in ((0, 1000), (1000, 2000))], -1)
assert_allclose(got, expected)
expected = expected[:, np.isfinite(expected[0])]
assert_allclose(raw.get_data(reject_by_annotation='omit'), expected)
got = np.concatenate([raw.get_data(start=start, stop=stop, reject_by_annotation='omit') for start, stop in ((0, 1000), (1000, 2000))], -1)
assert_allclose(got, expected)
pytest.raises(ValueError, raw.get_data, reject_by_annotation='foo')
```

## Next Steps


---

*Source: test_annotations.py:583 | Complexity: Advanced | Last updated: 2026-05-18*