# How To: Spectrum Reject By Annot

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test rejecting by annotation.

Cannot use raw_spectrum fixture here because we're testing reject_by_annotation in
.compute_psd() method.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `functools`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.spectrum`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas.testing`
- `mne.utils.dataframe`
- `matplotlib.pyplot`

**Setup Required:**
```python
# Fixtures: raw
```

## Step-by-Step Guide

### Step 1: "Test rejecting by annotation.\n\n    Cannot use raw_spectrum fixture here because we're testing reject_by_annotation in\n    .compute_psd() method.\n    "

```python
"Test rejecting by annotation.\n\n    Cannot use raw_spectrum fixture here because we're testing reject_by_annotation in\n    .compute_psd() method.\n    "
```

**Verification:**
```python
assert spect_no_annot == spect_benign_annot
```

### Step 2: Assign kw = dict(...)

```python
kw = dict(n_per_seg=512)
```

**Verification:**
```python
assert spect_no_annot == spect_ignored_annot
```

### Step 3: Assign spect_no_annot = raw.compute_psd(...)

```python
spect_no_annot = raw.compute_psd(**kw)
```

**Verification:**
```python
assert spect_no_annot != spect_reject_annot
```

### Step 4: Call raw.set_annotations()

```python
raw.set_annotations(Annotations([1, 5], [3, 3], ['test', 'test']))
```

### Step 5: Assign spect_benign_annot = raw.compute_psd(...)

```python
spect_benign_annot = raw.compute_psd(**kw)
```

### Step 6: Assign raw.annotations.description = np.array(...)

```python
raw.annotations.description = np.array(['bad_test', 'bad_test'])
```

### Step 7: Assign spect_reject_annot = raw.compute_psd(...)

```python
spect_reject_annot = raw.compute_psd(**kw)
```

### Step 8: Assign spect_ignored_annot = raw.compute_psd(...)

```python
spect_ignored_annot = raw.compute_psd(**kw, reject_by_annotation=False)
```

**Verification:**
```python
assert spect_no_annot == spect_benign_annot
```


## Complete Example

```python
# Setup
# Fixtures: raw

# Workflow
"Test rejecting by annotation.\n\n    Cannot use raw_spectrum fixture here because we're testing reject_by_annotation in\n    .compute_psd() method.\n    "
kw = dict(n_per_seg=512)
spect_no_annot = raw.compute_psd(**kw)
raw.set_annotations(Annotations([1, 5], [3, 3], ['test', 'test']))
spect_benign_annot = raw.compute_psd(**kw)
raw.annotations.description = np.array(['bad_test', 'bad_test'])
spect_reject_annot = raw.compute_psd(**kw)
spect_ignored_annot = raw.compute_psd(**kw, reject_by_annotation=False)
assert spect_no_annot == spect_benign_annot
assert spect_no_annot == spect_ignored_annot
assert spect_no_annot != spect_reject_annot
```

## Next Steps


---

*Source: test_spectrum.py:293 | Complexity: Advanced | Last updated: 2026-05-18*