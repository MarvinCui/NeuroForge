# How To: Coherence Analysis

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that the coherence analyzer works

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `tempfile`
- `numpy`
- `pytest`
- `nipype.testing`
- `nipype.interfaces.nitime`
- `nitime.analysis`
- `nitime.timeseries`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Test that the coherence analyzer works'

```python
'Test that the coherence analyzer works'
```

**Verification:**
```python
assert o.outputs.coherence_array.shape == (31, 31)
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert (CA._csv2ts().data == T.data).all()
```

### Step 3: Assign CA = nitime.CoherenceAnalyzer(...)

```python
CA = nitime.CoherenceAnalyzer()
```

**Verification:**
```python
assert (o.outputs.coherence_array == coh).all()
```

### Step 4: Assign CA.inputs.TR = 1.89

```python
CA.inputs.TR = 1.89
```

### Step 5: Assign CA.inputs.in_file = example_data(...)

```python
CA.inputs.in_file = example_data('fmri_timeseries.csv')
```

### Step 6: Assign tmp_csv = value

```python
tmp_csv = tempfile.mkstemp(suffix='.csv')[1]
```

### Step 7: Assign CA.inputs.output_csv_file = tmp_csv

```python
CA.inputs.output_csv_file = tmp_csv
```

### Step 8: Assign o = CA.run(...)

```python
o = CA.run()
```

**Verification:**
```python
assert o.outputs.coherence_array.shape == (31, 31)
```

### Step 9: Assign TR = 1.89

```python
TR = 1.89
```

### Step 10: Assign data_rec = np.genfromtxt(...)

```python
data_rec = np.genfromtxt(example_data('fmri_timeseries.csv'), delimiter=',', names=True)
```

### Step 11: Assign roi_names = np.array(...)

```python
roi_names = np.array(data_rec.dtype.names)
```

### Step 12: Assign n_samples = value

```python
n_samples = data_rec.shape[0]
```

### Step 13: Assign data = np.zeros(...)

```python
data = np.zeros((len(roi_names), n_samples))
```

### Step 14: Assign T = ts.TimeSeries(...)

```python
T = ts.TimeSeries(data, sampling_interval=TR)
```

**Verification:**
```python
assert (CA._csv2ts().data == T.data).all()
```

### Step 15: Assign unknown = roi_names

```python
T.metadata['roi'] = roi_names
```

### Step 16: Assign C = nta.CoherenceAnalyzer(...)

```python
C = nta.CoherenceAnalyzer(T, method=dict(this_method='welch', NFFT=CA.inputs.NFFT, n_overlap=CA.inputs.n_overlap))
```

### Step 17: Assign freq_idx = value

```python
freq_idx = np.where((C.frequencies > CA.inputs.frequency_range[0]) * (C.frequencies < CA.inputs.frequency_range[1]))[0]
```

### Step 18: Assign coh = np.mean(...)

```python
coh = np.mean(C.coherence[:, :, freq_idx], -1)
```

**Verification:**
```python
assert (o.outputs.coherence_array == coh).all()
```

### Step 19: Assign tmp_png = value

```python
tmp_png = tempfile.mkstemp(suffix='.png')[1]
```

### Step 20: Assign CA.inputs.output_figure_file = tmp_png

```python
CA.inputs.output_figure_file = tmp_png
```

### Step 21: Assign unknown = value

```python
data[n_idx] = data_rec[roi]
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test that the coherence analyzer works'
import nitime.analysis as nta
import nitime.timeseries as ts
tmpdir.chdir()
CA = nitime.CoherenceAnalyzer()
CA.inputs.TR = 1.89
CA.inputs.in_file = example_data('fmri_timeseries.csv')
if display_available:
    tmp_png = tempfile.mkstemp(suffix='.png')[1]
    CA.inputs.output_figure_file = tmp_png
tmp_csv = tempfile.mkstemp(suffix='.csv')[1]
CA.inputs.output_csv_file = tmp_csv
o = CA.run()
assert o.outputs.coherence_array.shape == (31, 31)
TR = 1.89
data_rec = np.genfromtxt(example_data('fmri_timeseries.csv'), delimiter=',', names=True)
roi_names = np.array(data_rec.dtype.names)
n_samples = data_rec.shape[0]
data = np.zeros((len(roi_names), n_samples))
for n_idx, roi in enumerate(roi_names):
    data[n_idx] = data_rec[roi]
T = ts.TimeSeries(data, sampling_interval=TR)
assert (CA._csv2ts().data == T.data).all()
T.metadata['roi'] = roi_names
C = nta.CoherenceAnalyzer(T, method=dict(this_method='welch', NFFT=CA.inputs.NFFT, n_overlap=CA.inputs.n_overlap))
freq_idx = np.where((C.frequencies > CA.inputs.frequency_range[0]) * (C.frequencies < CA.inputs.frequency_range[1]))[0]
coh = np.mean(C.coherence[:, :, freq_idx], -1)
assert (o.outputs.coherence_array == coh).all()
```

## Next Steps


---

*Source: test_nitime.py:33 | Complexity: Advanced | Last updated: 2026-05-18*