# How To: Future Trials

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test future trials

## Prerequisites

**Required Modules:**
- `threading`
- `psychopy`
- `psychopy.hardware`
- `psychopy.tests`
- `pathlib`
- `json`
- `asyncio`
- `time`
- `psychopy.hardware.keyboard`
- `psychopy.visual`


## Step-by-Step Guide

### Step 1: Call runInLiaison()

```python
runInLiaison(self.server, self.protocol, 'session', 'addExperiment', 'testFutureTrials/testFutureTrials.psyexp', 'testFutureTrials')
```

**Verification:**
```python
assert i < 24, 'Timed out waiting for a non-None result from getFutureTrial'
```

### Step 2: Call time.sleep()

```python
time.sleep(1)
```

**Verification:**
```python
assert all(keysPresent), 'Trial object missing key(s): {}'.format((expectedKeys[i] for i, val in enumerate(keysPresent) if not val))
```

### Step 3: Call threading.Thread.start()

```python
threading.Thread(target=_thread).start()
```

**Verification:**
```python
assert resp['type'] == 'trial_data', f"First non-None result from getFutureTrial doesn't look like a Trial object: {resp}"
```

### Step 4: Call runInLiaison()

```python
runInLiaison(self.server, self.protocol, 'session', 'runExperiment', 'testFutureTrials')
```

### Step 5: Assign resp = None

```python
resp = None
```

### Step 6: Assign i = 0

```python
i = 0
```

**Verification:**
```python
assert i < 24, 'Timed out waiting for a non-None result from getFutureTrial'
```

### Step 7: Assign expectedKeys = value

```python
expectedKeys = ('type', 'thisN', 'thisRepN', 'thisTrialN', 'thisIndex', 'data')
```

### Step 8: Assign keysPresent = value

```python
keysPresent = [key in resp for key in expectedKeys]
```

**Verification:**
```python
assert all(keysPresent), 'Trial object missing key(s): {}'.format((expectedKeys[i] for i, val in enumerate(keysPresent) if not val))
```

### Step 9: Call runInLiaison()

```python
runInLiaison(self.server, self.protocol, 'session', 'getFutureTrial', '1', 'True')
```

### Step 10: Assign resp = json.loads(...)

```python
resp = json.loads(self.protocol.messages[-1]['result'])
```

### Step 11: Call time.sleep()

```python
time.sleep(0.1)
```


## Complete Example

```python
# Workflow
runInLiaison(self.server, self.protocol, 'session', 'addExperiment', 'testFutureTrials/testFutureTrials.psyexp', 'testFutureTrials')
time.sleep(1)

def _thread():
    resp = None
    i = 0
    while resp is None and i < 24:
        runInLiaison(self.server, self.protocol, 'session', 'getFutureTrial', '1', 'True')
        resp = json.loads(self.protocol.messages[-1]['result'])
        time.sleep(0.1)
        i += 1
    assert i < 24, 'Timed out waiting for a non-None result from getFutureTrial'
    expectedKeys = ('type', 'thisN', 'thisRepN', 'thisTrialN', 'thisIndex', 'data')
    keysPresent = [key in resp for key in expectedKeys]
    assert all(keysPresent), 'Trial object missing key(s): {}'.format((expectedKeys[i] for i, val in enumerate(keysPresent) if not val))
    assert resp['type'] == 'trial_data', f"First non-None result from getFutureTrial doesn't look like a Trial object: {resp}"
threading.Thread(target=_thread).start()
runInLiaison(self.server, self.protocol, 'session', 'runExperiment', 'testFutureTrials')
```

## Next Steps


---

*Source: test_Liaison.py:93 | Complexity: Advanced | Last updated: 2026-05-18*