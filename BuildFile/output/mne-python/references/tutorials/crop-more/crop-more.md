# How To: Crop More

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test more cropping.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test more cropping.'

```python
'Test more cropping.'
```

**Verification:**
```python
assert len(raw.annotations) == 4
```

### Step 2: Assign raw = mne.io.read_raw_fif.crop.load_data(...)

```python
raw = mne.io.read_raw_fif(fif_fname).crop(0, 11).load_data()
```

**Verification:**
```python
assert_allclose(raw_concat.times, raw.times)
```

### Step 3: Assign unknown = np.random.RandomState.randn(...)

```python
raw._data[:] = np.random.RandomState(0).randn(*raw._data.shape)
```

**Verification:**
```python
assert_allclose(raw_concat[:][0], raw[:][0])
```

### Step 4: Assign onset = np.array(...)

```python
onset = np.array([0.47058824, 2.49773765, 6.67873287, 9.15837097])
```

**Verification:**
```python
assert raw_concat.first_samp == raw.first_samp
```

### Step 5: Assign duration = np.array(...)

```python
duration = np.array([0.89592767, 1.13574672, 1.09954739, 0.48868752])
```

**Verification:**
```python
assert_and_remove_boundary_annot(raw_concat, 2)
```

### Step 6: Assign annotations = mne.Annotations(...)

```python
annotations = mne.Annotations(onset, duration, 'BAD')
```

**Verification:**
```python
assert len(raw_concat.annotations) == 4
```

### Step 7: Call raw.set_annotations()

```python
raw.set_annotations(annotations)
```

**Verification:**
```python
assert_array_equal(raw_concat.annotations.description, raw.annotations.description)
```

### Step 8: Assign delta = value

```python
delta = 1.0 / raw.info['sfreq']
```

**Verification:**
```python
assert_allclose(raw.annotations.duration, duration)
```

### Step 9: Assign offset = value

```python
offset = raw.first_samp * delta
```

**Verification:**
```python
assert_allclose(raw_concat.annotations.duration, duration)
```

### Step 10: Assign raw_concat = mne.concatenate_raws(...)

```python
raw_concat = mne.concatenate_raws([raw.copy().crop(0, 4 - delta), raw.copy().crop(4, 8 - delta), raw.copy().crop(8, None)])
```

**Verification:**
```python
assert_allclose(raw.annotations.onset, onset + offset)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw_concat.times, raw.times)
```

**Verification:**
```python
assert_allclose(raw_concat.annotations.onset, onset + offset, atol=1.0 / raw.info['sfreq'])
```

### Step 12: Call assert_allclose()

```python
assert_allclose(raw_concat[:][0], raw[:][0])
```

**Verification:**
```python
assert raw_concat.first_samp == raw.first_samp
```

### Step 13: Call assert_and_remove_boundary_annot()

```python
assert_and_remove_boundary_annot(raw_concat, 2)
```

**Verification:**
```python
assert len(raw_concat.annotations) == 4
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(raw_concat.annotations.description, raw.annotations.description)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(raw.annotations.duration, duration)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(raw_concat.annotations.duration, duration)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(raw.annotations.onset, onset + offset)
```

### Step 18: Call assert_allclose()

```python
assert_allclose(raw_concat.annotations.onset, onset + offset, atol=1.0 / raw.info['sfreq'])
```


## Complete Example

```python
# Workflow
'Test more cropping.'
raw = mne.io.read_raw_fif(fif_fname).crop(0, 11).load_data()
raw._data[:] = np.random.RandomState(0).randn(*raw._data.shape)
onset = np.array([0.47058824, 2.49773765, 6.67873287, 9.15837097])
duration = np.array([0.89592767, 1.13574672, 1.09954739, 0.48868752])
annotations = mne.Annotations(onset, duration, 'BAD')
raw.set_annotations(annotations)
assert len(raw.annotations) == 4
delta = 1.0 / raw.info['sfreq']
offset = raw.first_samp * delta
raw_concat = mne.concatenate_raws([raw.copy().crop(0, 4 - delta), raw.copy().crop(4, 8 - delta), raw.copy().crop(8, None)])
assert_allclose(raw_concat.times, raw.times)
assert_allclose(raw_concat[:][0], raw[:][0])
assert raw_concat.first_samp == raw.first_samp
assert_and_remove_boundary_annot(raw_concat, 2)
assert len(raw_concat.annotations) == 4
assert_array_equal(raw_concat.annotations.description, raw.annotations.description)
assert_allclose(raw.annotations.duration, duration)
assert_allclose(raw_concat.annotations.duration, duration)
assert_allclose(raw.annotations.onset, onset + offset)
assert_allclose(raw_concat.annotations.onset, onset + offset, atol=1.0 / raw.info['sfreq'])
```

## Next Steps


---

*Source: test_annotations.py:366 | Complexity: Advanced | Last updated: 2026-05-18*