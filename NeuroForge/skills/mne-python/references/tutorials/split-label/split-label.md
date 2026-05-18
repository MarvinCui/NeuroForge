# How To: Split Label

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test splitting labels.

## Prerequisites

**Required Modules:**
- `glob`
- `os`
- `pickle`
- `shutil`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.label`
- `mne.source_estimate`
- `mne.source_space`
- `mne.surface`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test splitting labels.'

```python
'Test splitting labels.'
```

**Verification:**
```python
assert_equal(post.name, parts[0])
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert_equal(ant.name, parts[1])
```

### Step 3: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert_labels_equal(lingual_reconst, lingual)
```

### Step 4: Assign aparc = read_labels_from_annot(...)

```python
aparc = read_labels_from_annot('fsaverage', 'aparc', 'lh', regexp='lingual', subjects_dir=subjects_dir)
```

**Verification:**
```python
assert_labels_equal(post1, post)
```

### Step 5: Assign lingual = value

```python
lingual = aparc[0]
```

**Verification:**
```python
assert_labels_equal(ant1, ant)
```

### Step 6: Call pytest.raises()

```python
pytest.raises(ValueError, lingual.split, 'bad_input_string')
```

**Verification:**
```python
assert_array_equal(antmost.vertices, fs_vert)
```

### Step 7: Assign parts = value

```python
parts = ('lingual_post', 'lingual_ant')
```

**Verification:**
```python
assert_equal(antmost.name, 'lingual_div40-lh')
```

### Step 8: Assign unknown = split_label(...)

```python
post, ant = split_label(lingual, parts, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert_equal([len(label.vertices) for label in DMN_sublabels], [16181, 7022, 5965, 5300, 823] + [1] * 23)
```

### Step 9: Call assert_equal()

```python
assert_equal(post.name, parts[0])
```

### Step 10: Call assert_equal()

```python
assert_equal(ant.name, parts[1])
```

### Step 11: Assign lingual_reconst = value

```python
lingual_reconst = post + ant
```

### Step 12: Assign lingual_reconst.name = value

```python
lingual_reconst.name = lingual.name
```

### Step 13: Assign lingual_reconst.comment = value

```python
lingual_reconst.comment = lingual.comment
```

### Step 14: Assign lingual_reconst.color = value

```python
lingual_reconst.color = lingual.color
```

### Step 15: Call assert_labels_equal()

```python
assert_labels_equal(lingual_reconst, lingual)
```

### Step 16: Assign unknown = lingual.split(...)

```python
post1, ant1 = lingual.split(parts, subjects_dir=subjects_dir)
```

### Step 17: Call assert_labels_equal()

```python
assert_labels_equal(post1, post)
```

### Step 18: Call assert_labels_equal()

```python
assert_labels_equal(ant1, ant)
```

### Step 19: Assign antmost = value

```python
antmost = split_label(lingual, 40, None, subjects_dir, True)[-1]
```

### Step 20: Assign fs_vert = value

```python
fs_vert = [210, 4401, 7405, 12079, 16276, 18956, 26356, 32713, 32716, 32719, 36047, 36050, 42797, 42798, 42799, 59281, 59282, 59283, 71864, 71865, 71866, 71874, 71883, 79901, 79903, 79910, 103024, 107849, 107850, 122928, 139356, 139357, 139373, 139374, 139375, 139376, 139377, 139378, 139381, 149117, 149118, 149120, 149127]
```

### Step 21: Call assert_array_equal()

```python
assert_array_equal(antmost.vertices, fs_vert)
```

### Step 22: Call assert_equal()

```python
assert_equal(antmost.name, 'lingual_div40-lh')
```

### Step 23: Assign label_default_mode = read_label(...)

```python
label_default_mode = read_label(subjects_dir / 'fsaverage' / 'label' / 'lh.7Networks_7.label')
```

### Step 24: Assign DMN_sublabels = label_default_mode.split(...)

```python
DMN_sublabels = label_default_mode.split(parts='contiguous', subject='fsaverage', subjects_dir=subjects_dir)
```

### Step 25: Call assert_equal()

```python
assert_equal([len(label.vertices) for label in DMN_sublabels], [16181, 7022, 5965, 5300, 823] + [1] * 23)
```


## Complete Example

```python
# Workflow
'Test splitting labels.'
pytest.importorskip('nibabel')
pytest.importorskip('sklearn')
aparc = read_labels_from_annot('fsaverage', 'aparc', 'lh', regexp='lingual', subjects_dir=subjects_dir)
lingual = aparc[0]
pytest.raises(ValueError, lingual.split, 'bad_input_string')
parts = ('lingual_post', 'lingual_ant')
post, ant = split_label(lingual, parts, subjects_dir=subjects_dir)
assert_equal(post.name, parts[0])
assert_equal(ant.name, parts[1])
lingual_reconst = post + ant
lingual_reconst.name = lingual.name
lingual_reconst.comment = lingual.comment
lingual_reconst.color = lingual.color
assert_labels_equal(lingual_reconst, lingual)
post1, ant1 = lingual.split(parts, subjects_dir=subjects_dir)
assert_labels_equal(post1, post)
assert_labels_equal(ant1, ant)
antmost = split_label(lingual, 40, None, subjects_dir, True)[-1]
fs_vert = [210, 4401, 7405, 12079, 16276, 18956, 26356, 32713, 32716, 32719, 36047, 36050, 42797, 42798, 42799, 59281, 59282, 59283, 71864, 71865, 71866, 71874, 71883, 79901, 79903, 79910, 103024, 107849, 107850, 122928, 139356, 139357, 139373, 139374, 139375, 139376, 139377, 139378, 139381, 149117, 149118, 149120, 149127]
assert_array_equal(antmost.vertices, fs_vert)
assert_equal(antmost.name, 'lingual_div40-lh')
label_default_mode = read_label(subjects_dir / 'fsaverage' / 'label' / 'lh.7Networks_7.label')
DMN_sublabels = label_default_mode.split(parts='contiguous', subject='fsaverage', subjects_dir=subjects_dir)
assert_equal([len(label.vertices) for label in DMN_sublabels], [16181, 7022, 5965, 5300, 823] + [1] * 23)
```

## Next Steps


---

*Source: test_label.py:739 | Complexity: Advanced | Last updated: 2026-05-18*