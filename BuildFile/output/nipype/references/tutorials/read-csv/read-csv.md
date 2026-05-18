# How To: Read Csv

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that reading the data from csv file gives you back a reasonable
time-series object

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `numpy`
- `pytest`
- `nipype.testing`
- `nipype.interfaces.nitime`
- `nitime.analysis`
- `nitime.timeseries`


## Step-by-Step Guide

### Step 1: 'Test that reading the data from csv file gives you back a reasonable\n    time-series object'

```python
'Test that reading the data from csv file gives you back a reasonable\n    time-series object'
```

**Verification:**
```python
assert data[0][0] == 10125.9
```

### Step 2: Assign CA = nitime.CoherenceAnalyzer(...)

```python
CA = nitime.CoherenceAnalyzer()
```

**Verification:**
```python
assert roi_names[0] == 'WM'
```

### Step 3: Assign CA.inputs.TR = 1.89

```python
CA.inputs.TR = 1.89
```

### Step 4: Assign CA.inputs.in_file = example_data(...)

```python
CA.inputs.in_file = example_data('fmri_timeseries_nolabels.csv')
```

### Step 5: Assign CA.inputs.in_file = example_data(...)

```python
CA.inputs.in_file = example_data('fmri_timeseries.csv')
```

### Step 6: Assign unknown = CA._read_csv(...)

```python
data, roi_names = CA._read_csv()
```

**Verification:**
```python
assert data[0][0] == 10125.9
```

### Step 7: Call CA._read_csv()

```python
CA._read_csv()
```


## Complete Example

```python
# Workflow
'Test that reading the data from csv file gives you back a reasonable\n    time-series object'
CA = nitime.CoherenceAnalyzer()
CA.inputs.TR = 1.89
CA.inputs.in_file = example_data('fmri_timeseries_nolabels.csv')
with pytest.raises(ValueError):
    CA._read_csv()
CA.inputs.in_file = example_data('fmri_timeseries.csv')
data, roi_names = CA._read_csv()
assert data[0][0] == 10125.9
assert roi_names[0] == 'WM'
```

## Next Steps


---

*Source: test_nitime.py:17 | Complexity: Intermediate | Last updated: 2026-05-18*