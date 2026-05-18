# How To: Multipleregressdesign

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test MultipleRegressDesign

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `nipype.interfaces.fsl.model`
- `nipype.interfaces.fsl`
- `pathlib`
- `pipeline`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign designer = pe.Node(...)

```python
designer = pe.Node(fsl.MultipleRegressDesign(), name='designer', base_dir=str(tmpdir))
```

**Verification:**
```python
assert Path(outputs['design_' + ftype]).exists()
```

### Step 2: Assign designer.inputs.regressors = dict(...)

```python
designer.inputs.regressors = dict(voice_stenght=[1, 1, 1], age=[0.2, 0.4, 0.5], BMI=[1, -1, 2])
```

**Verification:**
```python
assert Path(outputs[outfile]).read_text() == expected_content[outfile]
```

### Step 3: Assign con1 = value

```python
con1 = ['voice_and_age', 'T', ['age', 'voice_stenght'], [0.5, 0.5]]
```

### Step 4: Assign con2 = value

```python
con2 = ['just_BMI', 'T', ['BMI'], [1]]
```

### Step 5: Assign designer.inputs.contrasts = value

```python
designer.inputs.contrasts = [con1, con2, ['con3', 'F', [con1, con2]], ['con4', 'F', [con2]]]
```

### Step 6: Assign res = designer.run(...)

```python
res = designer.run()
```

### Step 7: Assign outputs = res.outputs.get_traitsfree(...)

```python
outputs = res.outputs.get_traitsfree()
```

### Step 8: Assign expected_content = value

```python
expected_content = {}
```

### Step 9: Assign unknown = '/NumWaves       3\n/NumPoints      3\n/PPheights      3.000000e+00 5.000000e-01 1.000000e+00\n\n/Matrix\n1.000000e+00 2.000000e-01 1.000000e+00\n-1.000000e+00 4.000000e-01 1.000000e+00\n2.000000e+00 5.000000e-01 1.000000e+00\n'

```python
expected_content['design_mat'] = '/NumWaves       3\n/NumPoints      3\n/PPheights      3.000000e+00 5.000000e-01 1.000000e+00\n\n/Matrix\n1.000000e+00 2.000000e-01 1.000000e+00\n-1.000000e+00 4.000000e-01 1.000000e+00\n2.000000e+00 5.000000e-01 1.000000e+00\n'
```

### Step 10: Assign unknown = '/ContrastName1   voice_and_age\n/ContrastName2   just_BMI\n/NumWaves       3\n/NumContrasts   2\n/PPheights          1.000000e+00 1.000000e+00\n/RequiredEffect     100.000 100.000\n\n/Matrix\n0.000000e+00 5.000000e-01 5.000000e-01\n1.000000e+00 0.000000e+00 0.000000e+00\n'

```python
expected_content['design_con'] = '/ContrastName1   voice_and_age\n/ContrastName2   just_BMI\n/NumWaves       3\n/NumContrasts   2\n/PPheights          1.000000e+00 1.000000e+00\n/RequiredEffect     100.000 100.000\n\n/Matrix\n0.000000e+00 5.000000e-01 5.000000e-01\n1.000000e+00 0.000000e+00 0.000000e+00\n'
```

### Step 11: Assign unknown = '/NumWaves       2\n/NumContrasts   2\n\n/Matrix\n1 1\n0 1\n'

```python
expected_content['design_fts'] = '/NumWaves       2\n/NumContrasts   2\n\n/Matrix\n1 1\n0 1\n'
```

### Step 12: Assign unknown = '/NumWaves       1\n/NumPoints      3\n\n/Matrix\n1\n1\n1\n'

```python
expected_content['design_grp'] = '/NumWaves       1\n/NumPoints      3\n\n/Matrix\n1\n1\n1\n'
```

**Verification:**
```python
assert Path(outputs['design_' + ftype]).exists()
```

### Step 13: Assign outfile = value

```python
outfile = 'design_' + ftype
```

**Verification:**
```python
assert Path(outputs[outfile]).read_text() == expected_content[outfile]
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
designer = pe.Node(fsl.MultipleRegressDesign(), name='designer', base_dir=str(tmpdir))
designer.inputs.regressors = dict(voice_stenght=[1, 1, 1], age=[0.2, 0.4, 0.5], BMI=[1, -1, 2])
con1 = ['voice_and_age', 'T', ['age', 'voice_stenght'], [0.5, 0.5]]
con2 = ['just_BMI', 'T', ['BMI'], [1]]
designer.inputs.contrasts = [con1, con2, ['con3', 'F', [con1, con2]], ['con4', 'F', [con2]]]
res = designer.run()
outputs = res.outputs.get_traitsfree()
for ftype in ['mat', 'con', 'fts', 'grp']:
    assert Path(outputs['design_' + ftype]).exists()
expected_content = {}
expected_content['design_mat'] = '/NumWaves       3\n/NumPoints      3\n/PPheights      3.000000e+00 5.000000e-01 1.000000e+00\n\n/Matrix\n1.000000e+00 2.000000e-01 1.000000e+00\n-1.000000e+00 4.000000e-01 1.000000e+00\n2.000000e+00 5.000000e-01 1.000000e+00\n'
expected_content['design_con'] = '/ContrastName1   voice_and_age\n/ContrastName2   just_BMI\n/NumWaves       3\n/NumContrasts   2\n/PPheights          1.000000e+00 1.000000e+00\n/RequiredEffect     100.000 100.000\n\n/Matrix\n0.000000e+00 5.000000e-01 5.000000e-01\n1.000000e+00 0.000000e+00 0.000000e+00\n'
expected_content['design_fts'] = '/NumWaves       2\n/NumContrasts   2\n\n/Matrix\n1 1\n0 1\n'
expected_content['design_grp'] = '/NumWaves       1\n/NumPoints      3\n\n/Matrix\n1\n1\n1\n'
for ftype in ['mat', 'con', 'fts', 'grp']:
    outfile = 'design_' + ftype
    assert Path(outputs[outfile]).read_text() == expected_content[outfile]
```

## Next Steps


---

*Source: test_model.py:12 | Complexity: Advanced | Last updated: 2026-05-18*