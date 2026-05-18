# How To: Events As Path

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test events as path

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level.design_matrix`
- `_testing`

**Setup Required:**
```python
# Fixtures: n_frames, tmp_path
```

## Step-by-Step Guide

### Step 1: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

### Step 2: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, n_frames - 1, n_frames)
```

### Step 3: Assign events_file = value

```python
events_file = tmp_path / 'design.csv'
```

### Step 4: Call events.to_csv()

```python
events.to_csv(events_file)
```

### Step 5: Call make_first_level_design_matrix()

```python
make_first_level_design_matrix(frame_times, events=events_file)
```

### Step 6: Call make_first_level_design_matrix()

```python
make_first_level_design_matrix(frame_times, events=str(events_file))
```

### Step 7: Assign events_file = value

```python
events_file = tmp_path / 'design.tsv'
```

### Step 8: Call events.to_csv()

```python
events.to_csv(events_file, sep='\t')
```

### Step 9: Call make_first_level_design_matrix()

```python
make_first_level_design_matrix(frame_times, events=events_file)
```

### Step 10: Call make_first_level_design_matrix()

```python
make_first_level_design_matrix(frame_times, events=str(events_file))
```


## Complete Example

```python
# Setup
# Fixtures: n_frames, tmp_path

# Workflow
events = basic_paradigm()
frame_times = np.linspace(0, n_frames - 1, n_frames)
events_file = tmp_path / 'design.csv'
events.to_csv(events_file)
make_first_level_design_matrix(frame_times, events=events_file)
make_first_level_design_matrix(frame_times, events=str(events_file))
events_file = tmp_path / 'design.tsv'
events.to_csv(events_file, sep='\t')
make_first_level_design_matrix(frame_times, events=events_file)
make_first_level_design_matrix(frame_times, events=str(events_file))
```

## Next Steps


---

*Source: test_design_matrix.py:395 | Complexity: Advanced | Last updated: 2026-05-18*