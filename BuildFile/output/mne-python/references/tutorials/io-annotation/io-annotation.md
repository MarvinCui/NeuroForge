# How To: Io Annotation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test CSV, TXT, and FIF input/output (which support ch_names).

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
# Fixtures: dummy_annotation_file, tmp_path, fmt, ch_names, with_extras
```

## Step-by-Step Guide

### Step 1: 'Test CSV, TXT, and FIF input/output (which support ch_names).'

```python
'Test CSV, TXT, and FIF input/output (which support ch_names).'
```

**Verification:**
```python
assert annot.orig_time == _ORIG_TIME
```

### Step 2: Assign annot = read_annotations(...)

```python
annot = read_annotations(dummy_annotation_file)
```

**Verification:**
```python
assert annot.orig_time == _ORIG_TIME
```

### Step 3: Assign kwargs = dict(...)

```python
kwargs = dict(orig_time=_ORIG_TIME)
```

### Step 4: Call _assert_annotations_equal()

```python
_assert_annotations_equal(annot, Annotations([0.0, 9.0], [1.0, 2.425], ['AA', 'BB'], **kwargs), tol=1e-06, comp_extras_as_str=fmt in ['csv', 'txt'])
```

### Step 5: Assign fname = value

```python
fname = tmp_path / f'annotations-annot.{fmt}'
```

### Step 6: Call annot.save()

```python
annot.save(fname)
```

### Step 7: Assign annot2 = read_annotations(...)

```python
annot2 = read_annotations(fname)
```

### Step 8: Call _assert_annotations_equal()

```python
_assert_annotations_equal(annot, annot2)
```

### Step 9: Assign annot._orig_time = None

```python
annot._orig_time = None
```

### Step 10: Call annot.save()

```python
annot.save(fname, overwrite=True)
```

### Step 11: Assign annot2 = read_annotations(...)

```python
annot2 = read_annotations(fname)
```

### Step 12: Call _assert_annotations_equal()

```python
_assert_annotations_equal(annot, annot2)
```

### Step 13: Call pytest.importorskip()

```python
pytest.importorskip('pandas')
```

### Step 14: Assign unknown = value

```python
kwargs['ch_names'] = ((), ('MEG0111', 'MEG2563'))
```

### Step 15: Assign unknown = value

```python
kwargs['extras'] = [{'foo1': 1, 'foo2': 1.1, 'foo3': 'a', 'foo4': None}, None]
```


## Complete Example

```python
# Setup
# Fixtures: dummy_annotation_file, tmp_path, fmt, ch_names, with_extras

# Workflow
'Test CSV, TXT, and FIF input/output (which support ch_names).'
if with_extras:
    pytest.importorskip('pandas')
annot = read_annotations(dummy_annotation_file)
assert annot.orig_time == _ORIG_TIME
kwargs = dict(orig_time=_ORIG_TIME)
if ch_names:
    kwargs['ch_names'] = ((), ('MEG0111', 'MEG2563'))
if with_extras:
    kwargs['extras'] = [{'foo1': 1, 'foo2': 1.1, 'foo3': 'a', 'foo4': None}, None]
_assert_annotations_equal(annot, Annotations([0.0, 9.0], [1.0, 2.425], ['AA', 'BB'], **kwargs), tol=1e-06, comp_extras_as_str=fmt in ['csv', 'txt'])
fname = tmp_path / f'annotations-annot.{fmt}'
annot.save(fname)
annot2 = read_annotations(fname)
_assert_annotations_equal(annot, annot2)
annot._orig_time = None
annot.save(fname, overwrite=True)
annot2 = read_annotations(fname)
_assert_annotations_equal(annot, annot2)
```

## Next Steps


---

*Source: test_annotations.py:1053 | Complexity: Advanced | Last updated: 2026-05-18*