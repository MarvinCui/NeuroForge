# How To: Loaded Namespace

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test loaded namespace

## Prerequisites

**Required Modules:**
- `psychopy`
- `psychopy.tests.utils`
- `pathlib`
- `esprima`


## Step-by-Step Guide

### Step 1: Assign exp = experiment.Experiment(...)

```python
exp = experiment.Experiment()
```

**Verification:**
```python
assert len(actualSet) == len(expectedSet)
```

### Step 2: Assign allRoutines = experiment.getAllStandaloneRoutines(...)

```python
allRoutines = experiment.getAllStandaloneRoutines(fetchIcons=False)
```

**Verification:**
```python
assert len(actualSet) == len(actualSet.intersection(expectedSet))
```

### Step 3: "\n        Case structure\n        ==============\n        file : str\n            Experiment file to load\n        expectedSet : Set[str]\n            The expected names in the user namespace after routines are loaded and added\n        names : List[str]\n            Name of each routine to be added after experiment is loaded, paired with tags\n        tags : List[str]\n            Type of each routine to be added after experiment is loaded, paired with names\n            Can be 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerValidationRoutine'\n        "

```python
"\n        Case structure\n        ==============\n        file : str\n            Experiment file to load\n        expectedSet : Set[str]\n            The expected names in the user namespace after routines are loaded and added\n        names : List[str]\n            Name of each routine to be added after experiment is loaded, paired with tags\n        tags : List[str]\n            Type of each routine to be added after experiment is loaded, paired with names\n            Can be 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerValidationRoutine'\n        "
```

### Step 4: Assign cases = value

```python
cases = [{'file': 'test_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance', 'counterbalance_2', 'counterbalance_3', 'counterbalance_4', 'counterbalance_5', 'calibration', 'calibration_2'}, 'names': ['counterbalance', 'counterbalance', 'calibration', 'calibration'], 'tags': ['CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance', 'counterbalance_2', 'counterbalance_3', 'calibration', 'counterbalance_4', 'calibration_2'}, 'names': ['calibration', 'counterbalance', 'calibration'], 'tags': ['EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_custom_missing.psyexp', 'expectedSet': {'trial', 'custom_2', 'counterbalance_2', 'counterbalance', 'counterbalance_3', 'calibration', 'calibration_2'}, 'names': ['counterbalance', 'counterbalance', 'calibration', 'calibration'], 'tags': ['CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_missing_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance_2', 'counterbalance', 'counterbalance_3'}, 'names': ['counterbalance', 'counterbalance'], 'tags': ['CounterbalanceRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_mix_exp.psyexp', 'expectedSet': {'trial', 'counterbalance', 'calibration', 'counterbalance_2', 'validation', 'counterbalance_3', 'calibration_2', 'validation_2'}, 'names': ['counterbalance', 'calibration', 'validation'], 'tags': ['CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerValidationRoutine']}, {'file': 'test_mix_missing.psyexp', 'expectedSet': {'trial', 'calibration_2', 'counterbalance_2', 'calibration', 'counterbalance', 'calibration_3', 'counterbalance_3'}, 'names': ['calibration_2', 'counterbalance_2', 'calibration', 'counterbalance'], 'tags': ['EyetrackerCalibrationRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'CounterbalanceRoutine']}, {'file': 'test_mix_name_calibration.psyexp', 'expectedSet': {'trial', 'calibration_2', 'custom_2', 'counterbalance_2', 'calibration', 'calibration_3', 'custom_3', 'custom'}, 'names': ['calibration', 'calibration', 'custom_2', 'custom'], 'tags': ['EyetrackerCalibrationRoutine', 'CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine']}]
```

### Step 5: Call exp.loadFromXML()

```python
exp.loadFromXML(Path(TESTS_DATA_PATH) / 'test_loaded_namespace' / case['file'])
```

### Step 6: Assign namespace = value

```python
namespace = exp.namespace
```

### Step 7: Assign actualSet = set(...)

```python
actualSet = set(namespace.user)
```

### Step 8: Assign expectedSet = value

```python
expectedSet = case['expectedSet']
```

### Step 9: Call print()

```python
print()
```

### Step 10: Call print()

```python
print(case['file'])
```

### Step 11: Call print()

```python
print(actualSet)
```

### Step 12: Call print()

```python
print(expectedSet)
```

### Step 13: Call print()

```python
print()
```

**Verification:**
```python
assert len(actualSet) == len(expectedSet)
```

### Step 14: Assign routine = unknown(...)

```python
routine = allRoutines[tag](exp=exp, name=name)
```

### Step 15: Assign rtGoodName, unknown.val = namespace.makeValid(...)

```python
rtGoodName = routine.params['name'].val = namespace.makeValid(routine.params['name'].val)
```

### Step 16: Call namespace.add()

```python
namespace.add(rtGoodName)
```

### Step 17: Call exp.addStandaloneRoutine()

```python
exp.addStandaloneRoutine(routineName=rtGoodName, routine=routine)
```


## Complete Example

```python
# Workflow
exp = experiment.Experiment()
allRoutines = experiment.getAllStandaloneRoutines(fetchIcons=False)
"\n        Case structure\n        ==============\n        file : str\n            Experiment file to load\n        expectedSet : Set[str]\n            The expected names in the user namespace after routines are loaded and added\n        names : List[str]\n            Name of each routine to be added after experiment is loaded, paired with tags\n        tags : List[str]\n            Type of each routine to be added after experiment is loaded, paired with names\n            Can be 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerValidationRoutine'\n        "
cases = [{'file': 'test_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance', 'counterbalance_2', 'counterbalance_3', 'counterbalance_4', 'counterbalance_5', 'calibration', 'calibration_2'}, 'names': ['counterbalance', 'counterbalance', 'calibration', 'calibration'], 'tags': ['CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance', 'counterbalance_2', 'counterbalance_3', 'calibration', 'counterbalance_4', 'calibration_2'}, 'names': ['calibration', 'counterbalance', 'calibration'], 'tags': ['EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_custom_missing.psyexp', 'expectedSet': {'trial', 'custom_2', 'counterbalance_2', 'counterbalance', 'counterbalance_3', 'calibration', 'calibration_2'}, 'names': ['counterbalance', 'counterbalance', 'calibration', 'calibration'], 'tags': ['CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_missing_counterbalance.psyexp', 'expectedSet': {'trial', 'counterbalance_2', 'counterbalance', 'counterbalance_3'}, 'names': ['counterbalance', 'counterbalance'], 'tags': ['CounterbalanceRoutine', 'EyetrackerCalibrationRoutine']}, {'file': 'test_mix_exp.psyexp', 'expectedSet': {'trial', 'counterbalance', 'calibration', 'counterbalance_2', 'validation', 'counterbalance_3', 'calibration_2', 'validation_2'}, 'names': ['counterbalance', 'calibration', 'validation'], 'tags': ['CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'EyetrackerValidationRoutine']}, {'file': 'test_mix_missing.psyexp', 'expectedSet': {'trial', 'calibration_2', 'counterbalance_2', 'calibration', 'counterbalance', 'calibration_3', 'counterbalance_3'}, 'names': ['calibration_2', 'counterbalance_2', 'calibration', 'counterbalance'], 'tags': ['EyetrackerCalibrationRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine', 'CounterbalanceRoutine']}, {'file': 'test_mix_name_calibration.psyexp', 'expectedSet': {'trial', 'calibration_2', 'custom_2', 'counterbalance_2', 'calibration', 'calibration_3', 'custom_3', 'custom'}, 'names': ['calibration', 'calibration', 'custom_2', 'custom'], 'tags': ['EyetrackerCalibrationRoutine', 'CounterbalanceRoutine', 'CounterbalanceRoutine', 'EyetrackerCalibrationRoutine']}]
for case in cases:
    exp.loadFromXML(Path(TESTS_DATA_PATH) / 'test_loaded_namespace' / case['file'])
    namespace = exp.namespace
    for name, tag in zip(case['names'], case['tags']):
        routine = allRoutines[tag](exp=exp, name=name)
        rtGoodName = routine.params['name'].val = namespace.makeValid(routine.params['name'].val)
        namespace.add(rtGoodName)
        exp.addStandaloneRoutine(routineName=rtGoodName, routine=routine)
    actualSet = set(namespace.user)
    expectedSet = case['expectedSet']
    print()
    print(case['file'])
    print(actualSet)
    print(expectedSet)
    print()
    assert len(actualSet) == len(expectedSet)
    assert len(actualSet) == len(actualSet.intersection(expectedSet))
```

## Next Steps


---

*Source: test_experiment.py:104 | Complexity: Advanced | Last updated: 2026-05-18*