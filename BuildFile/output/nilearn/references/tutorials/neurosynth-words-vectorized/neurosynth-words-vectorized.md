# How To: Neurosynth Words Vectorized

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test neurosynth_words_vectorized.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test neurosynth_words_vectorized.'

```python
'Test neurosynth_words_vectorized.'
```

**Verification:**
```python
assert freq.shape == (n_im, n_im)
```

### Step 2: Assign n_im = 5

```python
n_im = 5
```

**Verification:**
```python
assert (freq.sum(axis=0) == np.ones(n_im)).all()
```

### Step 3: Assign words_files = value

```python
words_files = [tmp_path / f'words_for_image_{i}.json' for i in range(n_im)]
```

### Step 4: Assign words = value

```python
words = [str(i) for i in range(n_im)]
```

### Step 5: Assign unknown = neurovault.neurosynth_words_vectorized(...)

```python
freq, _ = neurovault.neurosynth_words_vectorized(words_files)
```

**Verification:**
```python
assert freq.shape == (n_im, n_im)
```

### Step 6: Assign word_weights = np.zeros(...)

```python
word_weights = np.zeros(n_im)
```

### Step 7: Assign unknown = 1

```python
word_weights[i] = 1
```

### Step 8: Assign words_dict = value

```python
words_dict = {'data': {'values': dict(zip(words, word_weights, strict=False))}}
```

### Step 9: Call words_file.write()

```python
words_file.write(json.dumps(words_dict).encode('utf-8'))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test neurosynth_words_vectorized.'
n_im = 5
words_files = [tmp_path / f'words_for_image_{i}.json' for i in range(n_im)]
words = [str(i) for i in range(n_im)]
for i, file_name in enumerate(words_files):
    word_weights = np.zeros(n_im)
    word_weights[i] = 1
    words_dict = {'data': {'values': dict(zip(words, word_weights, strict=False))}}
    with file_name.open('wb') as words_file:
        words_file.write(json.dumps(words_dict).encode('utf-8'))
freq, _ = neurovault.neurosynth_words_vectorized(words_files)
assert freq.shape == (n_im, n_im)
assert (freq.sum(axis=0) == np.ones(n_im)).all()
```

## Next Steps


---

*Source: test_neurovault.py:573 | Complexity: Advanced | Last updated: 2026-05-18*