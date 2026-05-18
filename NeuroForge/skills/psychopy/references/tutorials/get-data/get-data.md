# How To: Get Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get data

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `pytest`
- `pandas`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual.window`
- `psychopy.visual.form`
- `psychopy.visual.textbox2.textbox2`
- `psychopy.visual.slider`
- `psychopy.tests`
- `shutil`
- `tempfile`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign self.survey = Form(...)

```python
self.survey = Form(self.win, items=self.questions, size=(1.0, 0.3), pos=(0.0, 0.0), autoLog=False)
```

**Verification:**
```python
assert Qs == ['What is your gender?', 'How much you like running', 'How much you like cake', 'How much you like programming']
```

### Step 2: Assign data = self.survey.getData(...)

```python
data = self.survey.getData()
```

**Verification:**
```python
assert all([item['response'] is None for item in data])
```

### Step 3: Assign Qs = value

```python
Qs = [this['itemText'] for this in data]
```

**Verification:**
```python
assert all([item['rt'] is None for item in data])
```

### Step 4: Assign indices = value

```python
indices = [item['index'] for item in data]
```

**Verification:**
```python
assert list(indices) == list(range(4))
```


## Complete Example

```python
# Workflow
self.survey = Form(self.win, items=self.questions, size=(1.0, 0.3), pos=(0.0, 0.0), autoLog=False)
data = self.survey.getData()
Qs = [this['itemText'] for this in data]
indices = [item['index'] for item in data]
assert Qs == ['What is your gender?', 'How much you like running', 'How much you like cake', 'How much you like programming']
assert all([item['response'] is None for item in data])
assert all([item['rt'] is None for item in data])
assert list(indices) == list(range(4))
```

## Next Steps


---

*Source: test_form.py:391 | Complexity: Intermediate | Last updated: 2026-05-18*